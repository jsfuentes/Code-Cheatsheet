# Bash_Profile

`.bash_profile` is run on start up of login terminal

`.bashrc` is run on terminal nonlogin startup

For zsh(default after Catalina), `.zprofile` and `.zshrc` instead

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

## 12/2024 

- For adding to Warp

```bash
# Simple Shortcuts
alias fin='find . -iname'
alias ga='git add'
alias gl='git log'
alias gb='git branch'
alias gbv='git branch -v -a'
alias gd='git diff'
alias gds='git diff --staged'
alias gc='git commit'
alias gp='git push'
alias gss='git show --stat --oneline'
alias gs='git status'
alias ll='ls -lAG'
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# To Dirs
alias note='cd ~/Documents/CodeCheatsheet'

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

base_clone () {
    lang=$1
    CapName="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})$name:1}"-Base
    gitUrl=https://github.com/jsfuentes/"$CapName".git
    echo [1/2] Cloning $CapName from $gitUrl
    git clone $gitUrl
    echo [2/2] COMPLETE!
}
```



## Zprofile

Assuming you installed oh my zsh

```zsh
alias emacs="emacs -nw"
alias gs="git status"

alias sig='cd ~/Projects/Sigma'
alias sigcs='cd ~/Projects/Sigma/client && yarn dev'
alias sigss='cd ~/Projects/Sigma/server && yarn dev'
alias sigpis='cd ~/Projects/Sigma/plugin_iframe && yarn dev'
alias sigps='cd ~/Projects/Sigma/plugin && yarn watch'

alias note='cd ~/Documents/CodeCheatsheet'
alias pyrun='pipenv run python'

# added by Anaconda2 5.0.0 installer
export PATH="/anaconda2/bin:$PATH"

#terraform and ngrok
export PATH="/Users/jfuentes/MyTools/:$PATH"

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm

# Setting PATH for Python 3.7
# The original version is saved in .bash_profile.pysave
export PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"

# Have pipenv store the venv in the project like node_modules
export PIPENV_VENV_IN_PROJECT=1
```

#### Functions

```bash
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

base_clone () {
    lang=$1
    CapName="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})$name:1}"-Base
    gitUrl=https://github.com/jsfuentes/"$CapName".git
    echo [1/2] Cloning $CapName from $gitUrl
    git clone $gitUrl
    echo [2/2] COMPLETE!
}
```

## Project Specific

```bash
alias mapb='cd ~/Projects/Mappening-Backend'
alias mapf='cd ~/Projects/Mappening-Frontend'
alias mapd='cd ~/Projects/Mappening-Deployment'
alias est='cd ~/Projects/ecstatic'
alias estb='cd ~/Projects/ecstatic-botpress'
```

## My Bash_Profile

```bash
# All these are added by .zshrc oh my zsh
alias fin='find . -iname'
alias ga='git add'
alias gl='git log'
alias gb='git branch'
alias gbv='git branch -v -a'
alias gd='git diff'
alias gds='git diff --staged'
alias gc='git commit'
alias gp='git push'
alias gss='git show --stat --oneline'
alias ll='ls -lAG'
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# My extras
alias gs='git status'
alias note='cd ~/Documents/CodeCheatsheet'
alias pyrun='poetry run python'

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

#terraform and ngrok
export PATH="/Users/jfuentes/MyTools/:$PATH"

# Run `download_gitignore python` to create gitignore
download_gitignore () {
    name=$1
    CapName="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})${name:1}".gitignore
    gitUrl=https://raw.githubusercontent.com/github/gitignore/main/"$CapName"
    echo "[1/2] Fetching .gitignore for $name from $gitUrl"
    curl $gitUrl > .gitignore
    printf "\n# My Additions\n.DS_STORE\n*~*" >> .gitignore
    echo "[2/2] COMPLETE!  Your new .gitignore is outputted below:"
    echo $(cat .gitignore)
}

# Run `base_clone react_phoenix` to create templated react
base_clone () {
    name=$1
    echo $1
    CapName="$(tr '[:lower:]' '[:upper:]' <<< ${name:0:1})${name:1}"-Base
    echo $CapName
    gitUrl=https://github.com/jsfuentes/"$CapName".git
    echo "[1/2] Cloning $CapName from $gitUrl"
    git clone $gitUrl
    echo "[2/2] COMPLETE!"
}


# not sure what this does...
test -e "${HOME}/.iterm2_shell_integration.bash" && source "${HOME}/.iterm2_shell_integration.bash"

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



