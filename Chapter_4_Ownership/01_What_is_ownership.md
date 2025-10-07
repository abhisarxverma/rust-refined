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

### --- ☺️ To be continued ---