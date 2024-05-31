# Git

Git stores everything in a directory, `rm -rf .git` to delete the git project

`git --help command`

## Changing History

#### Reflog

Saves every instance of head changes

```bash
git reflog
git checkout -b after-commit HEAD@{1}
```

#### Get specific file from past

```bash
git checkout <treeish> -- /path/to/dir/orfile.js
```

#### Rebase

- rewrites history, if commits not local can mess things up
- could also rebase all your branch commits to occur at end of current master to **avoid a merge commit**

`git rebase master`, rebases current branch to master one 

#### Merge master in your branch before push

`git pull --rebase origin master`

#### Squash many commits to one

`git rebase -i <COMMIT_TO_IGNORE>`

1. `S`quash all but top
2. quit-save to rebase

### Stash

`git stash` - Takes dirty changes and saves them without committing

`git stash pop` - Reapply last saved changes

```bash
git stash list
> stash@{0}: WIP on master: 049d078 added the index file
> stash@{1}: WIP on master: c264051 Revert "added file_size"
> stash@{2}: WIP on master: 21d80a5 added number to log
```

`git stash apply stash@{2}` 

#### Undoing Last Commit

`git reset --hard HEAD~1` => don't keep changes

`git reset --soft HEAD~1` => undo commit, but keep working changes

`git revert <commit to undo>` =>Commit a commit undoing last commit

## Remotes

`git remote -v`  => List origins

#### Add remote

`git remote add origin [github url]`

#### Selecting branch to push from and to

```bash
git push origin develop:master
git push <remote> <local branch name>:<remote branch to push into>
```

#### Reset to remote branch

`git checkout -B master origin/master` //-B resets if it already exists

## Other

##### List Branches By Last Modified

```bash
for k in $(git branch | perl -pe s/^..//); do echo -e $(git show --pretty=format:"%Cgreen%ci %Cblue%cr%Creset" $k -- | head -n 1)\\t$k; done | sort -r
```

#### Tagging

`git tag -a v1.4 -m "my version 1.4"`

#### Delete branches

`git branch -d <branchname>` 

`git remote prune origin`  //remove all branches not in origin

#### Stop tracking file

`git rm --cached <file>`

#### Remove all Untracked files and build products

`git clean -fd` //remove everything untracked besides what is  ignored by .gitignore
`git clean -fdx` //remove all untracked files including those ignored by .gitignore
`git clean -fdX` //only remove files ignored by .gitignore

### Find commit that broke it

```bash
git bisect start
git bisect bad #current version is bad
git bisect good v2.6.13
#Starts wizard and checks out midpoint
git bisect bad #depending on if good or bad
git bisect good
```

#### [Did you just change the case in Mac OSX? That will cause git issues](https://stackoverflow.com/questions/13805750/git-fails-to-detect-renaming)

## Git grep

`git grep [string]` find all lines tracked by the git repo with the given string

`git grep -n -C 3 TeachApp` 

Modifiers:

- `-n` : show line numbers
- `-C 5`: show 5 context lines before and after 
- `-i`: ignore case

## Git Ignore

```
node_modules/ #any node_modules anywhere
/node_modules #only at route
*/node_modules #in any subdir
```

## Git LFS(Large File Store)

Basically, lets you use large files in github by using fileptrs

### Setup

1) `brew install git-lfs`

2) Track like `git lfs track "*.psd"` or have `.gitattributes`

.gitattributes

```
*.jpg filter=lfs diff=lfs merge=lfs -text
*.jpeg filter=lfs diff=lfs merge=lfs -text
*.png filter=lfs diff=lfs merge=lfs -text
*.gif filter=lfs diff=lfs merge=lfs -text
*.mp4 filter=lfs diff=lfs merge=lfs -text
*.mov filter=lfs diff=lfs merge=lfs -text
*.flv filter=lfs diff=lfs merge=lfs -text
*.webm filter=lfs diff=lfs merge=lfs -text
```

Thats it, just use normal workflow 

### Other people

3) `git lfs install` to get huge assets

4) `git lfs pull` to get lfs

