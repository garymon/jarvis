## 파이썬 개발환경 설정하기

- 파이썬 설치
  - 파이썬2
    - window : msi파일 다운 후 설치 [링크]([https://www.python.org/ftp/python/2.7.10/python-2.7.10.msi)
    - Linux : 기본적으로 설치되어 있다. python -V 버전확인
  - 파이썬3
    - mac : 설치 패키지 다운로드 해서 설치 3.6.0[링크](https://www.python.org/ftp/python/3.6.0/python-3.6.0-macosx10.6.pkg)



- pip 설치
  - 파이썬2
    - window
      1. setuptool.exe를 다운 [요기](https://pypi.python.org/pypi/setuptools)
      2. 설치하면 easy_install 이 설치됨.
      3. easy_install pip로 pip 설치.
    - Linux
      1. distribute.zip을 다운 [요기](https://pypi.python.org/pypi/distribute)
      2. unzip distribute.zip 해서 풀고
      3. python setup.py install로 easy_install 설치
      4. easy_install pip로 pip설치
  - 파이썬3
    - Linux
      - [get-pip.py](https://bootstrap.pypa.io/get-pip.py) 다운
      - python3 get-pip.py 실행
      - pip3로 실행한다.


- virtualenv 설치 및 설정
  - 파이썬2
    - pip virtualenv로 설치
    - virtualenv {env name}으로 환경 셋팅
    - . ./env name/bin/activate로 activation함.
  - 파이썬3
    - 파이썬3은 venv를 내장하고 있다.
    - python3 -m venv {env name}
    - 파이썬2와 실행방법 동일

- pip를 이용해서 필요한 package들을 requirements.txt로 뽑기
  - [pip | pip3] freeze > requirements.txt로 리스트를 만듦.


- requirements.txt로 필요 패키지 설치하기.
  - [pip | pip3] install -r requirements.txt로 필요 패키지 설치.
