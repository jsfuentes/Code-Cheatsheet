# Java

- Everything is an object yay!!
- Most similar to C++

## Running

FirstJavaProgram.java (*Same filename as class*)

```java
import java.util.Date;

public class Hello {
	public static void main(String[] args) {
		Date now = new Date();
		System.out.println("Hello World: " + now);
	}
}
```

```bash
javac FirstJavaProgram.java
java FirstJavaProgram
```

## Java App Structure

App must have one class 

Every file can have any # of classes, but must have one public class that is the filename, public class main is the entry point

```java
import java.util.Arrays;

public class UTXO implements Comparable<UTXO> {
    private byte[] txHash;
    private int index;

    //constructor
    public UTXO(byte[] txHash, int index) {
        this.txHash = Arrays.copyOf(txHash, txHash.length);
        this.index = index;
    }
}
```

Must compile all classes used with javac individually, but dont need to import as it will link automatically b/c names 

## Data Types

byte(8) | short(16) | int(32) | long(64) | float(32) | double(64) | char(16) | Boolean(1)

#### Type Conversions

```java
String str = String.valueOf(value);
int i = Integer.parseInt(str);
double d = Double.parseDouble(str);
int i = (int) numeric expres­sion;
```

## Blocks

C++ if, else if, else, while, do while, for, switch

```java
for ( var : collection ) {
	//statements
}
```

## Data Structures

Builtin Array:

- [] syntax, fixed size, store obj & primitatives(int), `.length`

ArrayList:

- only store objects(Integers), access with functions(.get())
- dynamic size, `.size()`, generics

```java
import java.util.*;//all
import java.util.ArrayList;
ArrayList<String> arr = new ArrayList<String>();
for (int i = 0; i < arr.size(); i++) {
  System.out.println("Index " + i + " : "+ arr[i]); 
}

import java.util.HashMap; 
HashMap<String, Integer> map = new HashMap<>(); 
Set<String> hash_Set = new HashSet<String>(); //HashSet, LInkedHashSet, or TreeSet
```

.add(item)

.get(i)

.size()

.remove(i)

.set(i, val)

## Object Methods

#### Equals

Default will check object reference is equal, can override equal to be different, essential for Java data structures like HashMaps which will use this equals

#### Comparator & Comparable

```java
import java.io.*; 
import java.util.*; 

class Movie implements Comparable<Movie> 
{ 
    private String name; 
    private int year; 
 
    public int compareTo(Movie m) 
    { 
        return this.year - m.year; 
    } 
 
    public Movie(String nm, int yr) 
    { 
        this.name = nm; 
        this.year = yr; 
    } 
 
    public String getName()   {  return name; } 
    public int getYear()      {  return year;  } 
} 
 
// Class to compare Movies by name 
class NameCompare implements Comparator<Movie> 
{ 
    public int compare(Movie m1, Movie m2) 
    { 
        return m1.getName().compareTo(m2.getName()); 
    } 
} 

class Main 
{ 
    public static void main(String[] args) 
    { 
        ArrayList<Movie> list = new ArrayList<Movie>(); 
        //add elements
        NameCompare nameCompare = new NameCompare(); 
        Collections.sort(list, nameCompare); //by name
        Collections.sort(list); // by default year
    } 
} 
```

