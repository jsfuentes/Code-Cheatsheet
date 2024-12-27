# Graphite

- Add stacks so you can create incremental PRs building off same base
- bidirectional sync with Github

## Usage

Anything not recognized is passthroughed to git

```bash
gt ls #see workflow
gt bt #go to top of branch
```

- Suggested workflow - Create changes then create branch then add changes to branch

```bash
gt add .
gt create -m "Add css styling" #generate new branch on top of stack
#ORRRR
gt c -am "commit messsage"
```

- Submission

```bash
gt ss --no-edit #stack submit, submit a PR for each stack 
```

- Need to make changes to part of stack

```bash
gt bco #move down to correct branch in the stack
# can amend current commit or add new commit on the branch, doesnt really matter for graphite
gt add .
gt modify #modify current commit
#Graphite restacks other PRs
gt ss #Update stack and PRs
gt s #CLI Open for stack submit
```

- Frequently rebasing

```bash
gt sync #syncing with the repo
gt restack #to restack all your stacks after sync
```

## Other

```bash
gt rename
```

