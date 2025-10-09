# References and Borrowing 🫠 

A **reference** is like a pointer in that it’s an address we can follow to access the data stored at that address; that data is owned by some other variable. 

Unlike a pointer, a reference is **guaranteed** to point to a valid value of a particular type for the life of that reference.

```rust
fn main() {
    let s = String::from("hello");
    let s_ref = &s;  // this is the reference to the data that s is storing
}
```

The **ampersands** represent references, and they allow you to refer to some value without taking ownership** of it.

**👉 Dereferencing** -  The opposite of referencing by using `&` is dereferencing, which is accomplished with the dereference operator, `*.`

The `&s` syntax lets us create a reference that refers to the value of `s` but does not own it. Because the reference does not own it, the value it points to will not be dropped when the reference stops being used.

**👉 Borrowing** - the action of **creating a reference** borrowing.

Just like variables, references are also **immutable by default**.

## 👉 Mutable References

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);  // passing mutable reference - giving power to change the data
}

fn change(some_string: &mut String) { // receiving mutable reference to a String data
    some_string.push_str(", world");
}
```

Mutable references have **one big restriction**: if you have a mutable reference to a value, you can have **no other references** to that value.

Rust enforces a similar rule for combining mutable and immutable references.

```rust
let mut s = String::from("hello");

let r1 = &s; // no problem
let r2 = &s; // no problem
let r3 = &mut s; // BIG PROBLEM

println!("{r1}, {r2}, and {r3}");
// Does not compile
```

We also **cannot have a mutable reference** while we have an **immutable** one to the same value.

```rust
let mut s = String::from("hello");

let r1 = &s; // no problem
let r2 = &s; // no problem
println!("{r1} and {r2}");
// Variables r1 and r2 will not be used after this point.

let r3 = &mut s; // no problem
println!("{r3}");
```

## 👉 Dangling References

**👉 Dangling pointer** — A pointer that references a location in memory that may have been given to someone else—by freeing some memory while preserving a pointer to that memory.

Rust never let this happens through references.

## 👉 The Rules of References

Let’s recap what we’ve discussed about references:

1. At any given time, you can have either one mutable reference or any number of immutable references.
2. References must always be valid.

---
### 🥳 Over
---