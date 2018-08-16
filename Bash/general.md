# Bash_profile

- In ~
- Make your own commands with `alias ll='ls -lAG'`
- Reload with `source ~/.bash_profile`

# Find

#### Find some string in all files in cur dir

```bash
find . -type f -print0 | xargs -0 grep "some string"
```

## Pbcopy

 `pbcopy < atom.sh`

