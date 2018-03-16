## python memory Profile
  - 도구 설치
    - pyrasite
      - docs
        - http://pyrasite.readthedocs.io/en/latest/
      - pip로 설치
        - pip install pyrasite
      - git clone으로 설치
        - git clone https://github.com/lmacken/pyrasite.git
        - python setup.py build install
      - 설치되는 명령어들
        - pyrasite - python파일을 타겟 process에 붙어서 돌려준다.
        - pyrasite-shell - 타켓 process에 붙어서 interactive한 shell을 제공한다.
        - pyrasite-memory-viewer - 타켓 process의 memory를 gui로 보여줌(잘 안됨..)
        - pyrasite-gui - gui도구인데 시도 안해 봄.
      - 설치되는 payload들
        - pyrasite를 설치하면 기본적으로 제공되는 payload(python파일들)들이 있다. (직접 작성하지 않아도 바로 테스트 가능)
        - dump_memory.py
          - pyrasite \<pid\> dump_memory.py 로 바로 실행이 가능하다.
        - 추가적인 payload는 https://github.com/lmacken/pyrasite/tree/master/pyrasite/payloads 에서 확인 가능.
     - meliae
        - 개발자 블로그
          - http://jam-bazaar.blogspot.kr/
        - 사실 pyrasite설치 될때 같이 설치 되어야 하지만 뭔가 잘 설치가 잘 안되서 직접 설치함.
        - Cython이 없어서 오류가 났던걸로 기억된다.
        - pip로 설치
          - pip install Cython
          - pip install meliae
        - 소스로 설치
          - wget https://launchpad.net/meliae/trunk/0.4/+download/meliae-0.4.0.tar.gz
          - tar -xzvf meliae-0.4.0.tar.gz
          - cd meliae-0.4.0
          - python setup.py build install

  - 사용법 및 트러블 슈팅.
    - 기본적으로 pyrasite-shell을 통해서 process에 연결한 다음 meliae로 memory분석을 진행했다.
    - pyrasite-shell \<pid\>
    - meliae loader를 통해서 리턴된 객체가 가지는 함수들은 아래의 github에서 확인할 수 있음.
      - https://github.com/isaacl/meliae/blob/master/meliae/loader.py#L201
    - 메모리를 분석할때 사용한 python 코드들.
    ```python
    import os
    from pprint import pformat as pf
    from pprint import pprint as pp
    from meliae import scanner, loader

    path = '/home1/irteamsu/memory_dump/%d-objects.json' % os.getpid() # 현재 프로세스의 pid로 파일이름을 생성했음.
    scanner.dump_all_objects(path) # path에 해당하는 파일에 데이터가 기록됨.

    om = loader.load(path)
    s = om.summarize(); s
    s.by_size()

    om.compute_referrers()
    om[s.summaries[0].max_address] # om[memory_address] 메모리 주소로dict를 접근하면 해당 메모리 주소에 있는 객체를 리턴해준다.

    strs = om.get_all('str') # str객체를 전부다 가져온다 list를 리턴함.
    strs[0].p # 해당객체가 어떤 객체로 부터 참조되고 있는지 parents를 가져옴.
    strs[0].c # 해당 객체가 가지고 있는 child객체를 가져옴.
    for ss in strs:  # 전체 str오브젝트를 출력해봄.
      pp(ss)
    ```


      - 응용 함수
  
    
    ```python
    # file pointer, parent, depth를 넘김으로써 특정 객체의 모든 child를 순회하면서 depth룰 tap으로 표현하여 파일에 써준다.
    # *주의  reference cycle이 존재할 시 무한루프가 생길수 있음.
    def pp_c(fp, par, depth): 
    prefix = '\n' + ('  ' * depth)
    fp.write(prefix)
    fp.write(pf(par).replace('\n', prefix))
    for cc in par.c:
        pp_c(fp, cc, depth + 1)
    ```

  - 트러블 슈팅.
    - pyrasite-shell로 연결해서 python shell명령어를 날리는데 process와 통신하는데 timeout이 기본적으로 짧게 설정되어 있음.
      그래서 조금이라도 긴 작업이 돌면(meliae로 분석해야 할 메모리가 크다거나..) 바로 timeout에러가 발생하는데 이는 export PYRASITE_IPC_TIMEOUT=60이렇게 환경 변수를 지정함으로써
      해결할수 있을것 처럼 github에 소스가 작성되어 있다. 하지만 pip로 받을수 있는 최신 버전은 해당 환경변수가 적용이 안된 버전이므로 git clone으로 설치하여 source를 수정하거나 해야 한다.
       - https://github.com/lmacken/pyrasite/blob/bc40e72776b025ce02982b680a6d2a3682a992e2/pyrasite/main.py#L95
       - 위와 같은 소스가 있긴 하지만 pip로 설치되는 버전에는 적용이 되어 있지 않다.
       - https://github.com/lmacken/pyrasite/blob/bc40e72776b025ce02982b680a6d2a3682a992e2/pyrasite/ipc.py#L67
       - 여기에서 그냥 timeout이 5로 잡혀있는거를 마음대로 늘려서 사용하면 된다. 직접 할때에는 240으로 주고 시도했음.
    - 한번 pyrasite-shell을 붙고 난 이후 종료하고 다시 붙게되면 memory를 dump떳을때 이전 작업에 사용되던 meliae object들이 남아있어서 제대로 분석이 불가능할 수 있다.
