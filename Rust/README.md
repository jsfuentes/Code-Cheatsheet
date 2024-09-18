# Rust

- Designed to write fast, correct code for large scale maintable systems and embeddable into other languages
- Safety and control
- Safe by design, can't have seg fault, null ptrs, and dangling ptrs, or parallel dat race
- Enums with match, structs, tuples, options, traits that can be implemented or put in generics
- Default immutable and no shared memory, its all opt in with mut and unsafe blocks for everything not allowed
- Rust can talk to C, basically directly with ft calls

```rust
fn main() {
    println!("Hello World!");
}
```

```bash
rustc hello.rs
./hello
```

## Basics Variables and Types?

- rust infers types

```rust
//Can specify types, but optional
let x: i32 = 42; //i32 good for everything, long in C, int in Java, and dfault
let b: f64 = 3.14; // 64-bit float
let c: bool = true; 
let d: char = 'z'; 
let e: &str = "Hello"; // String slice
let mut s = String::from("hello"); //String object that is mutable
s.push_str(", world!");

let pair: (char, i32) = ('a', 17)
pair.0; //a
pair.1 //17
let (_, r) = slice.split_at(middle)
```

### Lists

```rust
let mut numbers: Vec<i32> = Vec::new();
numbers.push(1);
numbers.push(2);
numbers.push(3);

let first = numbers[0]; // Access element
let length = numbers.len(); // Get length

let x = vec![1,2,3,4,5,6,7,8].iter().map(|x| x + 3).fold(0, |x,y| x + y);
```

### Control

```rust
// Loop
loop {
    println!("This will loop forever");
    break; // Exit the loop
}

// While loop
while x < 5 {
    println!("x is {}", x);
    x += 1;
}

while let Some(value) = some_option.take() {
    // Process value
}

// For loop
for i in 0..5 {
    println!("i is {}", i);
}

match some_value {
    1 => println!("One"),
    2 => println!("Two"),
    _ => println!("Something else"),
}

//let else
let PATTERN = EXPRESSION else {
    // Diverging code block
};

let Ok(count) = u64::from_str(count_str) else {
        panic!("Can't parse integer");
}; //count set
```

### Functions

```rust
fn greet(name: &str) -> String {
    format!("Hello, {}!", name)
}

fn main() {
    let message = greet("Alice");
    println!("{}", message);
}
```

### Struct and Enum

```rust
// Struct
struct Point {
    x: i32,
    y: i32,
}

let origin = Point { x: 0, y: 0 };

// Enum
enum Color {
    Red,
    Green,
    Blue,
}

let favorite_color = Color::Blue;
```

### Error Handling

````rust
// Using Result
fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err("Division by zero".to_string())
    } else {
        Ok(a / b)
    }
}

match divide(10.0, 2.0) {
    Ok(result) => println!("Result: {}", result),
    Err(error) => println!("Error: {}", error),
}
````

## Traits and Generic Types

```rust
trait Printable {
    fn print(&self);
}

impl Printable for i32 {
    fn print(&self) {
        println!("{}", self);
    }
}

fn print_any<T: Printable>(value: T) {
    value.print();
}
```

## Ownership and Borrowing

```rust
let s = String::from("hello");
takes_ownership(s); // s is moved here and then dropped

let x = 5;
let y = &x; // y is a reference to x

let mut z = 5;
let r = &mut z; // r is mutable reference to z
*r += 1;
```

## Concurrency

Threads can communiate by channel

```rust
use std::thread;
use std::time::Duration;

fn main() {
    let handle = thread::spawn(|| {
        println!("Hello from spawn");
    });

    handle.join().unwrap();

    thread::sleep(Duration::from_secs(2));
    println!("Main thread ends");
}
```

## Modules and Crates

```rust
mod utils {
    pub fn greet(name: &str) -> String {
        format!("Hello, {}!", name)
    }
}

fn main() {
    let name = "Alice";
    let greeting = utils::greet(name);
    println!("{}", greeting);
}
```

