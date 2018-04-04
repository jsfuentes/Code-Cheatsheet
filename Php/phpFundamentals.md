# PHP Fundamentals

## Running
See setup and AMP notes

## Basics

```php
<?php
  //code here
?>
<div> body </div>
```

- dynamically typed language
- All variable names begin with a $ followed byletters digits or underscores

#### Functions
- Function names are not case sensitive
- & in function def is pass by reference
- javascript scoping for functions not {}
- global declaration `global $x` makes it Avaliable everywhere
``` php
<?php
function increment(&$num) {
  // this $num is the actual parameter below
  $num++;
    print('$num in function: ' . "$num");
}
?>
```

#### Strings
- double quotes allows interpolation
`"Passwd:$password[Joe]"`

- Explode is like split in python `$ar = explode(":",$str);`
- Implode is like join  `$str = implode("^",$ar")`


#### Arrays
Basically dictionaries
```php
<?php
$ar = array("key1"=>"value 1", 67=>3, "a"=>10, 4=>"Hi");
$x = array();
$my_array[2] = 2006; // this is literally declaring an array
$my_array = array("Hello",2,TRUE);

$usernames = array_keys($ar);
$passwds= array_values($ar);
?>
```

*Functions to call on arrays*
- unset //entry or entire array
- count OR sizeof
- is_array

#### Control
- if and then like C++
```php
<?php
  foreach($array as $value) {}
  foreach($array as $key => $value){}
?>
```

#### Printing
- echo //no return type
- print //return true always
- if you use (), only one argument
- should do `$s." ".$t`

#### Big Project Functions
- isset($x)
- gettype($x)

## Includes

`include("filename")`

- check<a name="hi"></a>

## ERRORS
Do not put a space between #!/usr/local/bin/php
 <?php ?>
