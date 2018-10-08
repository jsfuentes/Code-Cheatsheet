# Grep

Searches input files selecting line to match patterns with 

grep [opts] \[re] [file]

```bash
grep jorge test.txt 
#same as 
grep "jorge" test.txt
```

Use `\` to escape characters 

### Search Directory

```bash
grep -r "\"Help.*me\"" .
```

Count number of lines with the word test in it

```bash
grep -r phone . | wc -l
```

## Some Options

-o	=> only print matching part of line

-n	=> output line number too 

-r	=> search subdirs

-i	=> case insensitive

-v 	=> select non-matching lines

-E 	=> Use extended grep 

### Extended Grep

Allows you to do stuff like specific or ranges of repetitions



```bash
grep -E "a{4}" #4 a's 
grep -E ">[0-9]{10,16}<" #10-16 digit number between > and < 
```

## Other Options

https://beyondgrep.com/feature-comparison/

ack, ag, git grep, ripgrep