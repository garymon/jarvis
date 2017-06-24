# Install Homebrew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
# terminal setting
### prompt
* install git prompt
```
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh -o ~/.git-prompt.sh
```
* setting .bash_profile
```
source ~/.git-completion.bash
source ~/.git-prompt.sh

DEFAULT="\[\033[00m\]"
MAGENTA="\[\033[0;35m\]"
YELLOW="\[\033[0;33m\]"
BLUE="\[\033[34m\]"
LIGHT_BLUE="\[\033[01;34m\]"
LIGHT_GRAY="\[\033[0;37m\]"
CYAN="\[\033[0;36m\]"
GREEN="\[\033[0;32m\]"
GREEN_BOLD="\[\033[01;32m\]"
export LS_OPTIONS='--color=auto'
export CLICOLOR='Yes'
export LSCOLORS=gxfxbEaEBxxEhEhBaDaCaD

export GIT_PS1_SHOWCOLORHINTS=1
export GIT_PS1_SHOWDIRTYSTATE=true
export GIT_PS1_SHOWUPSTREAM="auto verbose legacy name"
export PROMPT_COMMAND='__git_ps1 "$GREEN[Gary] $CYAN\t $GREEN_BOLD\u@\h$DEFAULT $LIGHT_BLUE\w$DEFAULT" "\\\$ "'
export CLICOLOR=1
export LSCOLORS=ExFxCxDxBxegedabagacad
alias ls='ls -lGH'
alias ll="ls -al"
```
