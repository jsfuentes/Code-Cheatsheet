# Ownership

Ownership prevents null ptrs and data races

1. Each value in Rust has an owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value is dropped.
4. Values can be moved between variables

*Slices* let you reference a contiguous sequence of elements in a [collection](https://doc.rust-lang.org/book/ch08-00-common-collections.html) rather than the whole collection

```rust
let x = 5;
let y = x;

println!("x = {x}, y = {y}"); //works fine, cuz on stack so fast

//different cuz on heap
let s1 = String::from("hello");
let s2 = s1;

println!("{s1}, world!"); //invalid bc since strings stored as ptr, rust auto declares s1 invalid

//instead
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {s1}, s2 = {s2}");
```

- calling functions auto pass ownership so no longer valid

```rust
fn main() {
    let s1 = gives_ownership();
    let s2 = String::from("hello");
    let s3 = takes_and_gives_back(s2);
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {
    let some_string = String::from("yours");
    some_string
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String {
    a_string
}
```

## References And Borrowing

- *references* allow you to refer to some value without taking ownership of it
- We call the action of creating a reference *borrowing*. As in real life, if a person owns something, you can borrow it from them. When you’re done, you have to give it back

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

- Cant change

  ```rust
  fn main() {
      let s = String::from("hello");
  
      change(&s);
  }
  
  fn change(some_string: &String) {
      some_string.push_str(", world"); 
  }// ERRORRRRR
  ```

- To change make mut

  - Mutable references have one big restriction: if you have a mutable reference to a value, you can have no other references(either mut or not) to that value.

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

- note ref scope goes from init to last time its used so

```rust
//will fail    
let mut s = String::from("hello");
let r1 = &s; // no problem
let r2 = &s; // no problem
let r3 = &mut s; // BIG PROBLEM
println!("{}, {}, and {}", r1, r2, r3);

//fine
let mut s = String::from("hello");
let r1 = &s; // no problem
let r2 = &s; // no problem
println!("{r1} and {r2}"); // variables r1 and r2 will not be used after this point
let r3 = &mut s; // no problem
println!("{r3}");
```

- rust will catch dangling ptrs

- ```rust
  //will fail
  fn main() {
      let reference_to_nothing = dangle();
  }
  
  fn dangle() -> &String {
      let s = String::from("hello");
  
      &s
  }
  ```

- 

