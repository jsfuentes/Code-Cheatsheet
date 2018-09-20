# Git

Git is literally just a directory, rm -rf .git to delete the git project

`git --help command`

## Remotes

#### Add remote

`git remote add origin [github url]`

#### Selecting branch to push from and to

```bash
git push origin develop:master
git push <remote> <local branch name>:<remote branch to push into>
```

#### Reset to remote branch

`git checkout -B master origin/master` //-B resets if it already exists

## Stash

`git stash` - Takes dirty changes and saves them without committing

```bash
git stash list
> stash@{0}: WIP on master: 049d078 added the index file
> stash@{1}: WIP on master: c264051 Revert "added file_size"
> stash@{2}: WIP on master: 21d80a5 added number to log
```

`git stash apply stash@{2}` 

## Rebase

- only rebase commits you have locally 
- could also rebase all your branch commits to occur at end of current master to avoid a merge commit

`git rebase master`, rebases current branch to master one 

#### Merge master in your branch before push

`git pull --rebase origin master`

#### Squash many commits to one

`git rebase -i <COMMIT_TO_IGNORE>`
1. Squash all but top
2. quit-save to rebase

## Other

#### Delete branch locally

`git branch -d <branchname>` 

#### Checkout specific file

`git checkout <branch_name> -- <paths>`

#### Remove all Untracked files and build products

`git clean -fd` //remove everything that isnt ignored by .gitignore
`git clean -fdx` //remove all untracked files including those ignored by .gitignore
`git clean -fdX` //only remove files ignored by git

## Git grep

`git grep [string]` find all lines tracked by the git repo with the given string

`git grep -n -C 3 TeachApp` 

Modifiers:

- `-n` : show line numbers
- `-C 5`: show 5 context lines before and after 