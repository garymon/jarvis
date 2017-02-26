### mongo db 설치하기
- Ubuntu 14.04
  커맨드 실행 순서
  1. 최신 버전의 mongo를 받기 위해서 승인 절차
    - sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
  2. mongo repo 추가
    - echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
  3. repo update
    - sudo apt-get update
  4. mongo 설치
    - sudo apt-get install mongodb (2.4 버전)
    - sudo apt-get install -y mongodb-org (3.4 버전)
      - **3.0+ 버전은 64비트 cpu에서만 동작이 가능하므로 32bit system에서는 mongodb-org package를 찾을수 없다**
  5. 서비스 실행 확인
    - sudo service mongodb [status / stop / start]
