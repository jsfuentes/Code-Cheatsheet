# Bash_Profile

`.bash_profile` is run on start up of login terminal

`.bashrc` is run on terminal nonlogin startup

http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html

tldr: 

equivalent on mac, but add 

```
if [ -f ~/.bashrc ]; then
   source ~/.bashrc
fi
```

to bashprofile and then use .bashrc and don't worry about it

## Basics

- In ~
- Make your own commands with `alias ll='ls -lAG'`
- Load in current shell with `source ~/.bash_profile`

## My Bash_Profile

```bash
alias ngrok='~/MyTools/ngrok'
alias note='cd ~/Documents/CodeCheatsheet'
alias fin='find . -iname'
alias ll='ls -lGa'

alias gs='git status'
alias gc='git commit'
alias ga='git add .'
alias gl='git log'
alias gb='git branch'
alias gd='git diff'
alias gss='git show --stat --oneline'

alias pyrun='pipenv run python'

LSCOLORS='GxFxcxdxxxegedaxagacad'
export LSCOLORS

function parse_git_branch () {
git branch 2> /dev/null | sed -e '/^*/d' -e 's/* (.*)/ (\1)/'
}

GREEN="[\033[0;32m]"
NO_COLOUR="[\033[0m]"
PURPLE="[\033[0;35m]"
CYAN="[\033[0;96m]"
SKY_BLUE="[\033[3;94m]"
YELLOW="[\033[0;93m]"
PS1="SKY_BLUE[ \u@\h \W/ YELLOW$(parse_git_branch)SKY_BLUE ]NO_COLOUR ~ "

export PIPENV_VENV_IN_PROJECT=1 

download_gitignore () {
    name=$1
    CapName="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})${name:1}".gitignore
    gitUrl=https://raw.githubusercontent.com/github/gitignore/master/"$CapName"
    echo [1/2] Fetching .gitignore for $name from $gitUrl
    curl $gitUrl > .gitignore
    echo [2/2] COMPLETE!  Your new .gitignore is outputted below:
    echo $(cat .gitignore)
}

```

## Project Specific

```bash
alias mapb='cd ~/Projects/Mappening-Backend'
alias mapf='cd ~/Projects/Mappening-Frontend'
alias mapd='cd ~/Projects/Mappening-Deployment'
```

## Pro

```bash
alias ard='arc diff origin/master'

function sbtp() {
 if [ -n "1" ]
 then
     sbt -Dprojects="1" "project 1" shell
 else
    sbt
 fi
}

```



