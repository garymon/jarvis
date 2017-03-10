## bash shell 작성

##### interpreter 정의
  * #!/bin/bash
    * #!는 두바이트의 매직 넘버, 실행 가능한 쉘 스크립트라는 것을 나타냄.
    * #!뒤에 오는 것은 경로명. 명령어들을 해석할 프로그램의 위치.

##### command line param
  * $번호 식으로 받음
  * $# = 파라미터 개수 ./my.sh param1 -> $# == 1
  * $1 = 첫번째 파라미터 ./my.sh param1 -> $1 == param1

##### 기본 명령어
  * if
  ```
  if [{condition}];
  then
      ## if true command
  else
      ## if flase
  fi
  ```
  * switch
  ```
  case {variable} in
      case1)
          ## if case1 command
          ;;
      case2)
          ## if case2 command
          ;;
      *)
          ## default command
          ;;
  esac
  ```
