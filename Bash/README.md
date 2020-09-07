# Bash

GNU Bourne-Again SHell, an POSIX(file system standard) compliant shell thingy. `sh` is a earlier verison 

*The language with literally multiple ways to do everything xO*

Alternatives include zsh shell which is default *interactive* shell after Catalina(you can still run bash scripts with bash with a shebang)

## Defining a Bash Script

```bash
#!/bin/bash
echo Hello World, arg $1
```

Call with `./scriptname.sh test` as that uses the shebang

*Can just run in bash without permission with `bash scriptname.sh` or `. scriptname.sh`*

## Variables

```bash
var1='soap' #no spaces
var1=soap

echo $var1 		# => soap
echo ${var1}	# => soap
echo var1 		# => var1
```

Make var avaliable to all subprocesses

```bash
export name=value 
```

#### String Interpolation

```bash
"$var1".txt #basically $(echo $var1).txt
```

## Print

printf has more standard behavior doing stuff like newlines

```bash
echo "Hello"
printf "Hello\n"
```

## Evaluate

```bash
$( echo $1 ) 
echo $(echo hi) # => hi
```

^generally better(newer and ez nesting without esacpes\)

```bash
echo `echo 1`  # => 1
```

#### Find Length

```bash
test=pets.com
echo ${#test} 	# => 8 (b/c its length 8)
```

## Functions

We supply the arguments directly after the function name. Within the function they are accessible as **$1, $2, etc**. 

```bash
print_something () { #create ft
    echo Hello $1 #access arguments
    return 5
}
#OR
function print_something() {
    echo Hello $1 #access arguments
    5
    return #empty return will return output of last command 
}

print_something Mars # call ft
print_something Jupiter
echo The previous function has a return value of $? #$? is last return value 
```

*Export with ` export -f myfun` so usable by subshells*

#### Special Parameters

| Symbol | Equivalent                                                   | Example            |
| ------ | ------------------------------------------------------------ | ------------------ |
| $@     | "\$1 " "\$2"                                                 | `for INPUT in "$@" |
| $*     | "\$1c\$2c..." where c is the first value of the IFS variable |                    |

## Conditionals

`man test` for info about conditionals

```bash
FILE=/etc/resolv.conf
if [ -f "$FILE" ]; then
    echo "$FILE exists."
else 
    echo "$FILE does not exist."
fi

if [ ! -f "$FILE" ]; then
    echo "$FILE does not exist."
fi
```

`man test` for a shit ton more about `[ ]`, p.s never forget the spaces

## Controls

```bash
for i in $( ls ); do
	echo item: $i
done

while [  $COUNTER -lt 10 ]; do
    echo The counter is $COUNTER
    let COUNTER=COUNTER+1 
done

COUNTER=20
until [  $COUNTER -lt 10 ]; do
    echo COUNTER $COUNTER
    let COUNTER-=1
done
```

## Exit

`exit [n]` will close shell with exit status of `[n]`