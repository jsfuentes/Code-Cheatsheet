# Bash_Profile

`.bash_profile` is run on start up of terminal

## Refresh it

`source .bash_profile` -  **load**s given functions file into the current shell 

## My Bash_Profile

alias ard='arc diff origin/master'
alias fin='find . -iname'
alias gs='git status'
alias gc='git commit'
alias ga='git add .'
alias gl='git log'
alias gb='git branch'
alias gd='git diff'
alias gss='git show --stat --oneline'
alias ll='ls -lGa'
LSCOLORS='GxFxcxdxxxegedaxagacad'
export LSCOLORS

function parse_git_branch () {
git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

export PATH=${PATH}:${HOME}/base/phacility/arcanist/bin
export PATH="/usr/local/sbin:$PATH"
export PATH="/Users/jfuentes/Library/Python/2.7/bin:$PATH"

GREEN="\[\033[0;32m\]"
NO_COLOUR="\[\033[0m\]"
PURPLE="\[\033[0;35m\]"
CYAN="\[\033[0;96m\]"
SKY_BLUE="\[\033[3;94m\]"
YELLOW="\[\033[0;93m\]"
PS1="$SKY_BLUE[ \u@\h \W/ $YELLOW\$(parse_git_branch)$SKY_BLUE ]$NO_COLOUR ~ "

export NVM_DIR="/Users/jfuentes/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm

function sbtp() {
 if [ -n "$1" ]
 then
     sbt -Dprojects="$1" "project $1" shell
 else
    sbt
 fi
}
export GPG_TTY=$(tty)

test -e "${HOME}/.iterm2_shell_integration.bash" && source "${HOME}/.iterm2_shell_integration.bash"