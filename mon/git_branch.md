Branch 관련된 명령어 모음
-------------
>#### remote에 있는 branch 목록 보기
~~~~
$ git branch -r
~~~

>#### local에 있는 branch 목록 보기
~~~
$ git branch -l
~~~

>#### local, remote에 있는 모든 branch 목록 보기
~~~
$ git branch -a
~~~


>#### local에 새로운 branch 만들기
~~~
$ git checkout -b master
(또는 git branch master)
~~~


>#### local에 만들었던 branch 삭제하기
~~~
$ git checkout master
(삭제 대상이 아닌 다른 branch로 이동 필요)
$ git branch -D master
~~~

>#### local에 있는 branch를 remote로 저장하기
~~~
$ git push origin origin:refs/heads/new-feature
또는
$ git push origin deveolp
~~~


>#### remote에 있었던 branch 를 local로 다운받기
~~~
$ git checkout develop
~~~


>#### remote에 있던 branch 삭제
~~~
$ git push origin :heads/develop
~~~
