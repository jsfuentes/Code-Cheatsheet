## Understand Machine

`top` see mem usage 

`du -sh` to see size of dir

`du -h --max-depth=1 | sort -hr` to see size of dirs/files in folder

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

`xargs [utility] [utility args]`

reads from the standard input
​     and executes utility



