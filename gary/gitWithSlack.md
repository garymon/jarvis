## Git과 Slack 연동.

1. 일단 아래의 repo를 clone해서 git-slack-hook 파일을 받는다.
https://github.com/chriseldredge/git-slack-hook
2. 적용할 repo에 .git/hooks/에 post-receive라는 이름으로 복사함
  만약 적용할 repo가 비어있다면 /hooks 라는 폴더를 생성 후 post-receive를 적용.

3. https://my.slack.com/services/new/incoming-webhook
  에 접속해서 post할 채널을 고르고 Add Incoming Webhooks를 하면 webhook을 위한 url을 리턴함.

4. 3에서 받은 url을 적용할 repo에서 git config hooks.slack.webhook-url {url} 을 설정하고 push하면 끝.


추가적인 설정들
git config hooks.slack.username 'git'
git config hooks.slack.icon-url 'https://example.com/icon.png'
git config hooks.slack.icon-emoji ':twisted_rightwards_arrows:'
git config hooks.slack.repo-nice-name 'My Awesome Repository'
git config hooks.slack.show-only-last-commit true
git config hooks.slack.show-full-commit true
