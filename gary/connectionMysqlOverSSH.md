### AWS에 띄워진 MySql에 연결하기.

배경 : aws에 접근하기 위해서는 기본적으로 pem파일이 있어야함.
일반적인 mysql -h 커맨드로는 커넥션을 맺기가 불가능 하다.

- MysqlWorkbench를 이용하기
  - mysql workbench에 connection method에 standard TCO/IP over ssh라는 방법을 제공한다.
  - ssh hostname(hostname:port), ssh username을 입력하고 ssh연결에 필요한 pem파일을 선택해준다.
  - ssh 연결 후 mysql은 localhost인 127.0.0.1, port=3306, username, password를 입력해서 연결 테스트를 해보면 성공!

- Mysql Command를 이용
  - 모르게따.. 아래 명령어로 하면 된다는데 잘안됨.
  - mysql -u root -p -h {hostname} --ssl-ca={pem file} --ssl-verify-server-cert
  - 원인
    - default로 mysql을 설치하고 service를 띄우면 원격에서 접근하는것 자체를 막아놈
  - 해결
    - vi /etc/mysql/my.cnf에 bind-address=127.0.0.1을 주석처리.
    - sudo service mysql restart 서비스 재시작.
  - 위의 커맨드로 연결하면 연결 성공!
