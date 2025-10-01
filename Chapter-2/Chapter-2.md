# 2 : 🎱 Programming a guessing game

## 👉 Prelude

By default, Rust has a set of items defined in the standard library that it brings into the scope of every program. This set is called the **prelude**.

If a type you want to use isn’t in the prelude, you have to bring that type into scope explicitly with a ***use*** statement.

---

## 👉 Associated Function

A function that's implemented on a type.

For Example - 
```rust
String::new()
```
Here the `::` syntax shows that the new is the associated function declared on type String.

---

`read_line` puts whatever the user enters into the string we pass to it, but it also returns a **Result** value.

## 👉 Result

Result is an enumeration, often called an **enum**, which is a type that can be in one of **multiple possible states**. We call each possible state a **variant**.

### Variants of Result -

- **Ok** - Indicates the operation was successful, and it contains the successfully generated value.
- **Err** - Means the operation failed, and it contains information about how or why the operation failed.

An instance of **Result** has an `expect` method that you can call. 

If this instance of Result is an `Err` value, expect will cause the program to crash and display the message that you passed as an argument to `expect`.

If this instance of Result is an `Ok` value, `expect` will take the return value that `Ok` is holding and return just that value to you so you can use it.

## 👉 Crate

Crate is a collection of **Rust source code files**.

### 2 types of crates - 

- **Binary Crate** - Contains executable rust source code files.
- **Library Crate** - Contains code that is intended to be used in other programs and can’t be executed on its own. 

## 👉 Ordering

Import line - `std::cmp::Ordering`

The **Ordering** type is another **enum** and has the variants **Less**, **Greater**, and **Equal**.

## 👉 Cmp

The **cmp** method compares two values and can be called on anything that can be compared. It takes a reference to whatever you want to compare with. Then it returns a variant of the **Ordering** enum.

We use a **match** expression to decide what to do next based on which variant of **Ordering** was returned from the call to **cmp**.

## 👉 Match

A **match** expression is made up of ***arms***. An **arm** consists of a pattern to match against, and the code that should be run if the value given to match fits that arm’s pattern. Rust takes the value given to match and looks through each arm’s pattern in turn.

The match expression ends after the first successful match.

<h1>🥳 Over</h1>