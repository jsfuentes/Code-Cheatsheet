# PHP

## Running

See setup and AMP notes, need the server

## Basics

```php
<?php
  //code here
  $my_name = "JJ";
  print($my_name);
	print "Hi"
?>
<div> body </div>
```

- dynamically typed language
- All **variable** names begin with a `$` followed by letters digits or underscores

#### Printing

- echo //no return type
- print //return true always
- if you use (), only one argument
- should do `$s." ".$t`

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
```php
<?php 
  "Passwd:$password[Joe]" #double quotes allow interpolation
  $name = 'j' . 'f' #concatination
  $str = implode("^",$ar") #join in python
  $ar = explode(":",$str); #split in python
?>
```


#### Arrays
Basically dictionaries that if not set use numeric indexes
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
- if and then like C++, switch statement
#### Loops

- while, for

```php
<?php
  foreach($array as $value) {}
  foreach($array as $key => $value){}
  for ($i = 0; $i < 10; $i++) {
    //
  }
?>
```

#### Big Project Functions

- isset($x)
- gettype($x)

## Includes

`include("filename")`

- check<a name="hi"></a>

## ERRORS
Do not put a space between #!/usr/local/bin/php
 <?php ?>
