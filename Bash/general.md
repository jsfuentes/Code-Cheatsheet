# Find

recursively descends the directory tree for each path listed, evaluating an expression

*wont follow soft links* 

### Find file with word in them

```bash
find . -iname [word]
find . -iname local # => ./Projects/local
```

#### Find some string in all files in cur dir

```bash
find . -type f -print0 | xargs -0 
# OR
grep "some string"
```

## Pbcopy

 `pbcopy < atom.sh`

## Word Count(wc)

`wc -l [filename]`

#### Find number of lines in a directory

`find . -name '*' | xargs cat | wc -l` 

## XARGS

`cat [filename] | xargs wc -l` => `wc -l [filename]` 

`xargs [utility] \[utility args]`

reads from the standard input
​     and executes utility