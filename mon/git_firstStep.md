Git 시작 세팅
-------------

>#### remote 저장소 clone
~~~~
$ git clone URL
~~~~

>#### 현재 파일 or 수정이 필요한지 status checkout
~~~~
$ git status
~~~~
* 아래 untracked 부분은 현재 브랜치를 추적하지 않는다는 것임
~~~~
junui-MacBook-Pro:jarvis jun$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	mon/git_branch.md
	mon/git_firstStep.md
nothing added to commit but untracked files present (use "git add" to track)
~~~~

>#### New add file 은 add해줘야함
~~~~
$ git add 'New added file'
~~~~
* 아래 커맨드와 같이 add 후..
~~~~
Junui-MacBook-Pro:jarvis jun$ git add mon/git_firstStep.md
Junui-MacBook-Pro:jarvis jun$ git add mon/git_branch.md
Junui-MacBook-Pro:jarvis jun$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
	new file:   mon/git_branch.md
	new file:   mon/git_firstStep.md
~~~~

>#### Tracked 파일의 modified file stage 하기
~~~~
$ git add 'Modified file'
~~~~
