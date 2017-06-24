# terminal setting
### prompt
* install git aware prompt
```
mkdir ~/.bash
cd ~/.bash
git clone https://github.com/GwiYeong/git-aware-prompt.git
```
* setting .bash_profile
```
export GITAWAREPROMPT=~/.bash/git-aware-prompt
source "${GITAWAREPROMPT}/main.sh"

export PS1=" \[\033[01;32m\]\u@\h\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \[$txtcyn\]\$git_branch\[$txtred\]\$git_dirty\[$txtrst\]\$ "
export CLICOLOR=1
export LSCOLORS=ExFxCxDxBxegedabagacad
alias ls='ls -lGH'
alias ll="ls -al"
```
