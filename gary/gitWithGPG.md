## GPG
 * 태그나 커밋에 secret key를 이용해 서명하는 기능
 * 현재 몇몇 유명한 오픈소스 프로젝트(e.g apache project)에서는 signing된 커밋만을 merge해주는 정책을 적용하고 있다.
 
## 방법
 1. key 생성
  * gpg --gen-key
 2. key export
  * gpg --list-keys에서 보이는 pub key의 id를 가지고
  * gpg --armor --export <id> 를 입력
  * -----BEGIN PGP PUBLIC KEY BLOCK-----부터 -----END PGP PUBLIC KEY BLOCK----- 까지 복사
 3. git 계정에 key add
  * https://github.com/settings/keys 에서 add GPG key에 붙여넣기
 4. git config에 signingkey 추가.
  * git config user.signingkey <id>
  * git config --global user.signingkey <id>
 5. commit 에 -S 옵션으로 signing 추가.
  
## 이슈
 * mac 에서 초기 commit -S로 커밋을 할 때 아래와 같은 에러가 발생.
 ```
 error: gpg failed to sign the data
 fatal: failed to write commit object
 ```
 * 해결방법
 ```
 brew upgrade gnupg  # This has a make step which takes a while
brew link --overwrite gnupg
brew install pinentry-mac
echo "pinentry-program /usr/local/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf
killall gpg-agent
echo "test" | gpg --clearsign  # on linux it's gpg2 but brew stays as gpg
git config --global gpg.program gpg  # perhaps you had this already? On linux maybe gpg2
 ```

  refer : 
   * https://help.github.com/articles/generating-a-new-gpg-key/
   * https://help.github.com/articles/adding-a-new-gpg-key-to-your-github-account/
   * https://help.github.com/articles/telling-git-about-your-gpg-key/
   * https://help.github.com/articles/signing-commits-using-gpg/
   * https://stackoverflow.com/questions/39494631/gpg-failed-to-sign-the-data-fatal-failed-to-write-commit-object-git-2-10-0
