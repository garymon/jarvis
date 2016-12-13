## Slack에 Api로 글 post하기

1. https://my.slack.com/apps/A0F7XDUAZ-incoming-webhooks
에 접근해서 incoming-webhook을 생성한다.
2. 생성된 webhook-url로 post로 데이터를 날린다 {text:"message"}

message에 포함할수 있는 옵션들

- "username": "post user 이름",
- "icon_emoji": "아이콘 ",
- "channel": "#other-channel" default가 아닌 다른 채널에 post,


-끝-
