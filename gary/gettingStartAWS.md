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
  - crontab -l (리스트)
  - crontab -e (수정)
  - timezone을 재설정 했을 경우 cron 을 재시작 해줘야 한다. sudo service cron restart

- TimeZone 설정.
  - 처음 인스턴스를 생성하면 UTC 시간대로 설정되어 있음. 이를 한국 시간대로 변경.
  - ls /usr/share/zoneinfo 에서 표준 시간대 파일을 찾음 or timedatectl list-timezone
  - 한국의 경우 sudo timedatectl set-timezone Asia/Seoul  

- RDS 생성
  - 관계형 db service
  - 그냥 생성하고 security group에 inbound 수정한후 연결하면 됨.
  - 초기에 mysql의 collation은 default로 latin이다. (빡침)
    - AWS console에서 parameter Group을 생성 -> charset을 전부다 utf8로 바꾼 그룹을 생성한다.
    - instance를 선택하고 instance Action에서 modify -> parameter Group을 변경된걸로 설정.
    - instance Action에서 reboot해줘야함.
    - 테이블도 새로 생성해야함.
