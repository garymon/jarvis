## GPG
 * 태그나 커밋에 secret key를 이용해 서명하는 기능

## 방법
 1. key 생성
  * gpg --gen-key
 2. key export
  * gpg --list-keys에서 보이는 pub key의 id를 가지고
  * gpg --armor --export <id> 를 입력
  * -----BEGIN PGP PUBLIC KEY BLOCK-----부터 -----END PGP PUBLIC KEY BLOCK----- 까지 복사
 3. git 계정에 key add
  * https://github.com/settings/keys 에서 add GPG key에 붙여넣기
 4. commit 에 -S 옵션으로 signing 추가.
  

  refer : 
   * https://help.github.com/articles/generating-a-new-gpg-key/
   * https://help.github.com/articles/adding-a-new-gpg-key-to-your-github-account/
