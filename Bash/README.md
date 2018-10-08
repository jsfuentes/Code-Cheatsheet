## Bash

GNU Bourne-Again SHell, an POSIX(file system thingy) compliant shell thingy. `sh` is a earlier verison 

## Defining a Bash Script

```bash
#!/bin/bash
echo Hello World, arg $1
```

Call with `./scriptname.sh test` as that uses the shebang

*Can just run in bash without permission with `bash scriptname.sh` or `. scriptname.sh`*

## Variables

```bash
var1='global 1' #no spaces

echo $var1 		# => global 1
echo ${var1}	# => global 1
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

## Functions

. We supply the arguments directly after the function name. Within the function they are accessible as **$1, $2, etc**. 

```bash
print_something () { #create ft
echo Hello $1 #access arguments
return 5
}
print_something Mars # call ft
print_something Jupiter
echo The previous function has a return value of $? #$? is last return value 
```

## Conditionals

`man test` for info about conditionals

```bash
if [ $1 -gt 100 ]
then
    echo Hey that\'s a large number.
    pwd
fi
```

`man test` for a shit ton more 

## Evaluate In Place

Two ways: 

```bash
$( echo $1 ) 
```

^generally better(newer and ez nesting without esacpes\)

```bash
echo `echo 1`  # => 1
```