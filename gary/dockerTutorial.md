## Docker Tutorial
### 0. Introduce
  * 오픈소스 컨테이너 가상화 플랫폼
  * 3가지의 구성 요소
    * Docker 이미지
      * 읽기 전용 템플릿.
      * 시스템을 원하는대로 구성해서 이미지화 해놓을수 있으며 같은 환경을 바로 구성할수 있다.
    * Docker 컨테이너
      * 독립적이고 안전한 어플리케이션 구동 환경
      * 실행, 시작, 정지, 이동, 삭제가 가능
    * Docker 레지스트리
      * 이미지를 보관.
      * 공개 또는 비공개로 이미지를 업로드 다운로드 가능.


### 1. Intall
  * Docker
    * Linux
      * 설치 스크립트를 받아서 실행
      * sudo wget -qO- https://get.docker.com/ | sh
    * Mac
      * https://docs.docker.com/docker-for-mac/install/#download-docker-for-mac
    * Window
      * https://docs.docker.com/docker-for-windows/install/#download-docker-for-windows
  * Docker Tool Box
    * https://www.docker.com/products/docker-toolbox

### 2. Common Command
  * Image 검색
    * `docker search ubuntu`
  * Image 받기
    * `docker pull ubuntu`
    * docker hub에서 ubuntu이미지를 가져온다
  * 받은 Image 확인
    * `docker images`
  * 컨테이너 생성/ 실행
    * `docker run -i -t --name test-ubuntu ubuntu /bin/bash`
      * -i : interactive모드
      * -t : tty 모드, 실행된 Bash Shell에 입력 및 출력이 가능
      * -v : 호스트와 공유할 디렉토리 지정, -v /root/data:/data => 호스트의 /root/data를 docker 컨테이너의 /data 디렉터리에 연결
      * --name : 컨테이너 이름(docker 명령어에서 컨테이너id대신 사용)
      * ubuntu : 대상 이미지
      * /bin/bash : 컨테이너 생성이 완료되면 실행할 파일
  * 현재 컨테이너 목록
    * `docker ps`
      * -a : 죽은 컨테이너까지 포함해서 출력
  * 종료된 컨테이너 다시 실행
    * `docker start 컨테이너id`
  * 컨테이너를 재부팅
    * `docker restart 컨테이너id`
  * 재실행 된 컨테이너로 접속
    * `docker attach 컨테이너id`
    * Ctrl+P, Ctrl+Q를 차례대로 입력하면 컨테이너를 정지하지 않고, 컨테이너에서 빠져나옴
  * docker 컨테이너 외부에서 명령어 실행
    * `docker exec 컨테이너id 명령 매개변수`
    * 컨테이너가 종료된 상황에서는 사용 불가
  * 컨테이너 정지
    * `docker stop 컨테이너id`
  * 컨테이너 삭제
    * `docker rm 컨테이너id`
  * 이미지 삭제
    * `docker rmi 이미지이름:태그`

### 3. Dockerfile 생성
  * example
    * FROM: 어떤 이미지를 기반으로 할지 설정. 기존에 만들어진 이미지를 기반으로 생성. <이미지 이름>:<태그> 형식으로 설정.
    * MAINTAINER: 메인테이너 정보.
    * RUN: Shell 스크립트 혹은 명령을 실행.
      * 이미지 생성 중에는 사용자 입력을 받을 수 없다. apt-get install 명령에서 -y 옵션을 사용해야함.(yum install도 동일).
    * VOLUME: 호스트와 공유할 디렉터리 목록.
    * CMD: 컨테이너가 시작되었을 때 실행할 실행 파일 또는 스크립트.
    * WORKDIR: CMD에서 설정한 실행 파일이 실행될 디렉터리.
    * EXPOSE: 호스트와 연결할 포트 번호입니다.


```

FROM ubuntu:14.04
MAINTAINER Foo Bar <foo@bar.com>

RUN apt-get update
RUN apt-get install -y nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN chown -R www-data:www-data /var/lib/nginx

VOLUME ["/data", "/etc/nginx/site-enabled", "/var/log/nginx"]

WORKDIR /etc/nginx

CMD ["nginx"]

EXPOSE 80
EXPOSE 443

```

  * build
    * `docker build 옵션 dockerFile경로`
      * --tag : 이미지이름:태그

### 4. 기타 명령어
  * history조회
    * `docker history 이미지이름:태그`
      * docker 이미지의 히스토리를 조회
  * 컨테이너에서 파일 꺼내기
    * `docker cp 컨테이너이름:경로 호스트경로`
      * docker cp hello-nginx:/etc/nginx/nginx.conf ./
  * 변경 사항을 이미지 파일로 생성
    * `docker commit -a "Foo Bar <foo@bar.com>" -m "add hello.txt" hello-nginx hello:0.2`
      * -a : 커밋한 사용자
      * -m : 커밋 메세지
      * hello-nginx : 컨테이너 이름
      * hello:0.2 : 이미지이름:태그
        * docker hub에 올리기 위해서는 대상repository명:tag로 commit한다.
        * jgy0726/test:ubuntu-git

  * 변경 사항 조회
    * `docker diff 컨테이너 이름`
      * A는 추가된 파일, C는 변경된 파일, D는 삭제된 파일.
  * 이미지와 컨테이너의 세부정보 조회
    * `docker inspect 이미지/컨테이너이름`
  * 컨테이너 연결
    * `sudo docker run --name web -d -p 80:80 --link db:db nginx`
      * -d : daemon
      * -p : port forwarding
      * --link : 컨테이너이름:별칭
        * 추후 web컨테이너에서 db로 접근 가능
        * mongodb예시 : mongodb://db:27017/exampledb
### 5. docker 저장소 구축
  * `docker -d --insecure-registry localhost:5000`
    * localhost:5000에 docker데몬을 실행
    * 데몬이 아닌 서비스 형태로 실행하기 위해서는 /etc/init.d/docker파일의 DOCKER_OPTS를 수정
      * DOCKER_OPTS=--insecure-registry localhost:5000
      * docker재실행 : service docker restart
  * `docker pull registry:latest`
    * docker registry이미지를 받은후
  * `docker run -d -p 5000:5000 --name hello-registry -v /tmp/registry:/tmp/registry` 로 registry컨테이너 실행
  * 이미지 올리기
    * `docker tag hello:0.1 localhost:5000/hello:0.1`
      * docker tag <이미지 이름>:<태그> <Docker 레지스트리 URL>/<이미지 이름>:<태그> 형식
    * `docker push localhost:5000/hello:0.1`
      * docker push <Docker 레지스트리 URL>/<이미지 이름>:<태그>
  * 이미지 받기
    * docker pull 192.168.0.39:5000/hello:0.1
  * 이미지 삭제
    * docker rmi 192.168.0.39:5000/hello:0.1

### 6. Docker Hub 저장소 사용
  * 로그인
    * docker login
  * 이미지 올리기
    * docker push <Docker Hub 사용자 계정>/<레포지토리 명>:<태그>
      * 태그를 지정하지 않으면 latest로 올라감


  출처 [http://pyrasis.com/Docker/Docker-HOWTO](http://pyrasis.com/Docker/Docker-HOWTO)
