# What is Ownership? 🤔

**Ownership** is a set of rules that govern how a Rust program manages **memory**. 

Rust uses a different approach for memory safety and management: memory is managed through a system of ownership with a **set of rules that the compiler checks**.

If any of the rules are violated, the program won’t compile.

## 👉 Ownership Rules

1. **Each value** in Rust has an owner.
2. There can only be **one owner** at a time.
3. When the owner goes **out of scope**, the value will be dropped.

### 👉 Variable Scope
---

A scope is the **range within a program** for which an item is valid.

```rust
{                      // s is not valid here, since it's not yet declared
    let s = "hello";   // s is valid from this point forward

    // do stuff with s
}                      // this scope is now over, and s is no longer valid
```

## 👉 The String Type

String literals (`"hello world"`) are convenient, but they’re **immutable**.

Rust has a second string type - `String`.

**String type** manages data allocated on the **heap** and as such is able to store an amount of text that is **unknown** to us at compile time. 

This type of string can be **mutated**.

```rust
let mut s = String::from("hello");

s.push_str(", world!"); // push_str() appends a literal to a String

println!("{s}"); // this will print `hello, world!`
```

The double colon `::` operator allows us to namespace this particular from function under the String.

## 👉 Memory and Allocation

In string literals we know the contents at compile time, so the text is **hardcoded directly** into the final executable.

With the `String` type, in order to support a mutable, growable piece of text, we need to **allocate** an amount of memory on the **heap**, unknown at compile time, to hold the contents, and then we need to **deallocate** or free the memory also.

**👉 Allocation in rust** - When we call `String::from`, its implementation requests the memory it needs. 

**👉 Deallocation in rust** - The memory is automatically returned once the variable that owns it goes out of scope.

***👉 Drop*** - When a variable goes **out of scope**, Rust calls a special function for us. This function is called **drop**, and it’s where the author of `String` can put the code to **return the memory**. Rust calls drop automatically at the closing curly bracket.

### 👉 Variables and Data Interacting with Move
----

A `String` is made up of three parts: 

- **A pointer to the memory** - that holds the contents of the string in heap.
- **A length** - Memory, in bytes, the contents of the `String` are currently using.
- **A capacity** - Total amount of memory, in bytes, that the `String` has received from the allocator.

```rust
let s1 = String::from("hello");
let s2 = s1;
```

When we assign `s1` to `s2`, the `String` data is copied, meaning **we copy the pointer, the length, and the capacity that are on the stack**. We do not copy the data on the heap that the pointer refers to.

When `s2` and `s1` go out of scope, they will both try to **free the same memory**. This is known as a ***double free error*** and is one of the memory safety bugs. Freeing memory twice can lead to memory corruption, which can potentially lead to security vulnerabilities.

To ensure memory safety, after the line `let s2 = s1;`, Rust considers s1 as no longer valid. Therefore, Rust doesn’t need to free anything when s1 goes out of scope.

This is known as a ***move***. we would say that s1 was moved into s2.

### 👉 Scope and Assignment
---

When you assign a completely new value to an existing variable, Rust will call drop and free the original value’s memory **immediately**. 

```rust
let mut s = String::from("hello");
s = String::from("ahoy");

println!("{s}, world!");
```

The original string thus immediately goes out of scope.

### 👉 Variables and Data Interacting with Clone
---

**👉 Clone** - If we do want to **deeply copy the heap data** of the String, not just the stack data, we can use a common method called `clone`.

**👉 Copy - Stack-Only Data** - Rust has a special annotation called the **Copy** trait that we can place on types that are stored on the stack, as integers. If a type implements the Copy trait, variables that use it do not move, but rather are **trivially copied**, making them still valid after assignment to another variable.

Some types that implement Copy trait:

1. All the **integer** types, such as `u32`.
2. The **Boolean** type, bool, with values `true` and `false`.
3. All the **floating-point** types, such as `f64`.
4. The **character** type, `char`.
5. **Tuples**, if they only contain types that also implement Copy. For example, `(i32, i32)` implements Copy, but `(i32, String)` does not.

## 👉 Ownership and Functions

Passing a variable to a function will **move or copy**, just as assignment does.

```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // Because i32 implements the Copy trait,
                                    // x does NOT move into the function,
                                    // so it's okay to use x afterward.

} // Here, x goes out of scope, then s. However, because s's value was moved,
  // nothing special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```

## 👉 Return Values and Scope

Returning values can also **transfer ownership**. 🫠

```rust
fn main() {
    let s1 = gives_ownership();        // gives_ownership moves its return
                                       // value into s1

    let s2 = String::from("hello");    // s2 comes into scope

    let s3 = takes_and_gives_back(s2); // s2 is moved into
                                       // takes_and_gives_back, which also
                                       // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {       // gives_ownership will move its
                                       // return value into the function
                                       // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                        // some_string is returned and
                                       // moves out to the calling
                                       // function
}

// This function takes a String and returns a String.
fn takes_and_gives_back(a_string: String) -> String {
    // a_string comes into
    // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

## **🥳 Over**