### Line Message Api 사용하기

#### [documents](https://devdocs.line.me/en/)


기본적으로 제공되는 대표 API는
- webHooks
  - 실시간 사용자가 보낸 메세지의 noti를 받을수 있다.
- Reply Message API
  - 사용자가 보낸 메세지에 응답을 한다.
- Push Message API
  - 사용자에게 메세지를 보낸다.

* 전제조건
 - Line Official계정을 등록하고 해당 계정에 대한 action에 대해서만 api를 사용할수 있다.

 ### webHooks

 사용자가 해당 official 계정을 친구로 등록하거나 메세지를 보냈을때 trigger되며, HTTPS POST request가  webhook URL(official계정 admin페이지 -> bot 설정 -> Line Developer)[링크](https://developers.line.me/ba/u9db1e00cd5830e883407c61815f2d760/bot) 으로 호출된다. 해당 request를 받아서 처리하면 됨.


### HTTPS 서버를 위한 SSL 인증서 발급...

letscrypt로 무료 SSL인증서 발급하기
 - 소스 다운
   - git clone https://github.com/letsencrypt/letsencrypt
 - 의존성 설치
   - ./letsencrypt-auto --help
   - 이때 Ubuntu 14.04에서 no module named zlib 라는 오류가 발생(빡침)
    - 해결법
     - sudo apt-get install zlib1g-dev 로 설치
     - sudo apt-get install libssl-dev 로 설치
     - 파이썬 새로 설치

     ```
     - wget https://www.python.org/ftp/python/2.7.9/Python-2.7.9.tgz 로 파이썬 새로 받음
     - tar xzf Python-2.7.9.tgz
     - cd Python-2.7.9
     - ./configure --prefix /usr --enable-ipv6
     - make install
     ```
 - 인증서 발급
   - ./letsencrypt-auto certonly --manual


### AWS에 SSL인증서 설치. - 아마존 AWS에서는 사용 불가능 하다

```
amazonaws.com happens to be on the blacklist Let's Encrypt uses for high-risk domain names (i.e. phishing targets, etc.).
```
AWS Certificate Manager를 통해 가능.
** 하지만 SSL인증서를 받기 위해서는 domain이 필요하다
  - amazonaws.com 도메인으로는 신청 불가능 함!!!.
  - 도메인을 사던가 해라

~~포기~~
