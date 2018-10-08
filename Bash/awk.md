# Awk

- File manipulation
- Reads from std in and writes to std out
- Basically does the operation between `{...}` on every line

## Identity Op

```bash 
cat README.md | awk '{print $0}'
OR
awk '{print $0}' README.md
```

## Variables

$0 - WHOLE LINE

\$1, \$2, \$3 - index for line split by whitespace 

$NF - last field

$(NF-2)

NR is row number

## Change Field Seperator

Splits on colon for \$1, \$2, \$3

```bash
awk '{print $2}' logs.txt | awk 'BEGIN{FS=":"}{print $1}' | sed 's/\[//'
```

##### Get Text between two text

```bash
awk -v FS="(<a>|</a>)" '{print $2}'
```



## If

```bash
awk '{if ($(NF-2) == "200") {print $0}}' logs.txt
```

## Culumulative

```bash
awk '{a+=$(NF-2); print "Total so far:", a}' logs.txt

#only care about final state
awk '{a+=$(NF-2)}END{print "Total:", a}' logs.txt
```

## Other Examples

```bash
awk '{print NR ") " $1 " -> " $(NF-2)}' logs.txt
```

