## AWS 시작하기

Free Tier

- https://aws.amazon.com/ko/free/ 에 접속해서 계정 생성 및 로그인.
- EC2 생성
  - 프리티어용 t2.micro
  - 1 Core vCPU (up to 3.3 GHz), 1 GiB Memory RAM, 8 GB Storage
  - pem키 다운로드

- 접근 방법
  - 최초 EC2인스턴스를 생성하면 inbound ssh 트래픽에 대해서 default로 막고 있다.
  - EC2 콘솔에서 인스턴스의 Security Group에 접근해서 Create Security Group
  - Inbound 탭에서 Type을 SSH로 설정하고 source를 특정 ip로 주거나 any(0.0.0.0)로 준다.
  - ssh -i "my.pem" username@public-dns 명령어로 접근함.
  - deafult username
    - Amazone Linux : ec2-user
    - RHEL5 : root, ec2-user
    - Ubuntu : Ubuntu
    - Fedora : fedora, ec2-user
    - SUSE Linux : root, ec2-user



- 초기 필요 패키지 설치 (ubuntu 기준)
  - git
    - sudo apt-get install git
  - python
    - prerequisite
      - sudo apt-get install build-essential checkinstall
      - sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
    - python download
      - wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.
    - unzip and install
      - tar xzf Python-2.7.12.tgz
      - sudo ./configure (unzip한 python 디렉토리에서 해야함. 각종 파일들이 생성됨)
      - sudo make altinstall
      - python --version
    - pip 설치
      - sudo apt-get install python-pip
    - virtualenv 설치
      - sudo pip install virtualenv
  - java
    - sudo add-apt-repository ppa:webupd8team/java
    - sudo apt-get update
    - sudo apt-get install oracle-java8-installer

- Ubuntu Cron 설정
  - sudo vi /etc/crontab
  - sudo service cron reload

- TimeZone 설정.
  - 처음 인스턴스를 생성하면 UTC 시간대로 설정되어 있음. 이를 한국 시간대로 변경.
  - ls /usr/share/zoneinfo 에서 표준 시간대 파일을 찾음 or timedatectl list-timezone
  - 한국의 경우 sudo timedatectl set-timezone Asia/Seoul   
