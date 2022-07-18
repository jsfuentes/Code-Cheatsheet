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

| Flag   | Does                                    |
| ------ | --------------------------------------- |
| -o     | only print matching part of line        |
| -n     | output line #s too                      |
| -r     | search recursively subdirs              |
| -i     | case insensitive                        |
| -v     | select the non-matching lines           |
| -E     | Use extended grep(see below)            |
| -F     | Fixed string matching(faster if not re) |
| -C [n] | n lines shown b4 and after match        |

### Extended Grep

Allows you to do stuff like specific or ranges of repetitions

##### Not

```bash
grep -E "1[^2]" #1 followed by not two
```

##### Range

```bash
grep -E "a{4}" #4 a's 
grep -E ">[0-9]{10,16}<" #10-16 digit number between > and < 
```

##### Or

```bash
grep -E '(^| )ABC( |$)' file1 #ABC surrounded by a space or ending
```

## Other Tools

https://beyondgrep.com/feature-comparison/

ack, ag, git grep, ripgrep