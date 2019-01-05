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

## Pipe to File

cat file.txt > output.txt #override

cat file.txt >> output.txt #append

## Understand Machine

`top` see mem usage 

`du -sh` to see size of dir

`tail ` get end of file, `tail -f` to open buffer and show end of file updating

`head` get start of file

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



