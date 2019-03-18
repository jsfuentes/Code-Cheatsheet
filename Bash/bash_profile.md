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
alias fin='find . -iname'
alias ga='git add'
alias gs='git status'
alias gl='git log'
alias gb='git branch'
alias gbv='git branch -v -a'
alias gd='git diff'
alias gc='git commit'
alias gshowstat='git show --stat --oneline'
alias ll='ls -lAG'

alias note='cd ~/Documents/CodeCheatsheet'
alias pyrun='pipenv run python'

LSCOLORS='GxFxcxdxxxegedaxagacad'
export LSCOLORS
function parse_git_branch () {
git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export -f parse_git_branch

GREEN="\[\033[0;32m\]"
NO_COLOUR="\[\033[0m\]"
PURPLE="\[\033[0;35m\]"
CYAN="\[\033[0;96m\]"
SKY_BLUE="\[\033[3;94m\]"
YELLOW="\[\033[0;93m\]"
PS1="$SKY_BLUE[ \u@\h \W/ $YELLOW\$(parse_git_branch)$SKY_BLUE ]$NO_COLOUR ~ "

# added by Anaconda2 5.0.0 installer
export PATH="/anaconda2/bin:$PATH"

#terraform
export PATH="/Users/jfuentes/MyTools/:$PATH"

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi

# Setting PATH for Python 3.7
# The original version is saved in .bash_profile.pysave
export PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"

export PIPENV_VENV_IN_PROJECT=1 

download_gitignore () {
    name=$1
    CapName="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})${name:1}".gitignore
    gitUrl=https://raw.githubusercontent.com/github/gitignore/master/"$CapName"
    echo [1/2] Fetching .gitignore for $name from $gitUrl
    curl $gitUrl > .gitignore
    printf "\n# My Additions\n.DS_STORE\n*~*" >> .gitignore
    echo [2/2] COMPLETE!  Your new .gitignore is outputted below:
    echo $(cat .gitignore)
}

test -e "${HOME}/.iterm2_shell_integration.bash" && source "${HOME}/.iterm2_shell_integration.bash"

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



