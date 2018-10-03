## Bash

## Defining a Bash Script

```bash
#!/bin/bash
echo Hello World, arg $1
```

Call with `./scriptname.sh test`

## Variables

```bash
var1='global 1' #no spaces

echo $var1 # => global 1
echo var1 # => var1
```

Make var avaliable to all subprocesses

```bash
export name=value 
```

#### String Interpolation

```bash
"$var1"_template.txt
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

```bash
if [ $1 -gt 100 ]
then
    echo Hey that\'s a large number.
    pwd
fi
```

`man test` for a shit ton more 

## Print

printf has more standard behavior doing stuff like newlines

```bash
echo "Hello"
printf "Hello\n"
```

## Evaluate

```bash
$( echo $1 )
```

