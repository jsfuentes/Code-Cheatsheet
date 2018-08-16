# Git

Git is literally just a directory, rm -rf .git to delete the git project

### Rebase(rewrite history with new base)

- only rebase commits you have locally 
- could also rebase all your branch commits to occur at end of current master to avoid a merge commit

`git rebase master`, rebases current branch to master one 

### Merge master in your branch before push

git pull --rebase origin master

### Squash many commits to one

`git rebase -i <COMMIT_TO_IGNORE>`
1. Squash all but top
2. quit-save to rebase

### Checkout specific file

`git checkout <branch_name> -- <paths>`

### Remove all Untracked files and build products

`git clean -fd`
`git clean -fdx` //also remove build products and display_errors
`git clean -fdX` //only remove thsoe from git

### Add remote

`git remote add origin [github url]`

### Selecting branch to push from and to

```bash
git push origin develop:master
git push <remote> <local branch name>:<remote branch to push into>
```

### Reset to remote branch

`git checkout -B master origin/master` //-B resets if it already exists

