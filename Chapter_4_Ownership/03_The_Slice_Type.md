# 🍕 The Slice Type

Slices let you reference a **contiguous sequence** of elements in a collection. A slice is a **kind of reference**, so it does not have ownership.

## 👉🏼 String Slices

A string slice is a **reference** to a contiguous sequence of the elements of a String, and it looks like this:

```rust
let s = String::from("hello world");

let hello = &s[0..5];
let world = &s[6..11];
```

We create slices using a range within brackets by specifying `[starting_index..ending_index]`, where `starting_index` is the first position in the slice and `ending_index` is one more than the last position in the slice. 

Internally, the slice data structure stores the **starting position** and the **length** of the slice, which corresponds to `ending_index` minus `starting_index`.

With Rust’s `..` range syntax, if you want to start at index 0, you can drop the value before the two periods.

By the same token, if your slice includes the last byte of the String, you can drop the trailing number.

You can also drop both values to take a slice of the **entire string**.

### 👉🏼 String Literals as Slices

```rust
let s = "Hello, world!";
```

The type of `s` here is `&str`: it’s a slice pointing to that specific point of the binary. This is also why string literals are immutable; `&str` is an **immutable reference**.

### 👉🏼 String Slices as Parameters

```rust
fn first_word(s: &str) -> &str {}
```

If we have a **string slice**, we can pass that directly. If we have a **String**, we can pass a slice of the String or a reference to the String. This flexibility takes advantage of **deref coercions**.

```rust
fn main() {
    let my_string = String::from("hello world");

    // `first_word` works on slices of `String`s, whether partial or whole.
    let word = first_word(&my_string[0..6]);
    let word = first_word(&my_string[..]);
    // `first_word` also works on references to `String`s, which are equivalent
    // to whole slices of `String`s.
    let word = first_word(&my_string);

    let my_string_literal = "hello world";

    // `first_word` works on slices of string literals, whether partial or
    // whole.
    let word = first_word(&my_string_literal[0..6]);
    let word = first_word(&my_string_literal[..]);

    // Because string literals *are* string slices already,
    // this works too, without the slice syntax!
    let word = first_word(my_string_literal);
}
```

## 👉🏼 Other slices

String slices, as you might imagine, are specific to strings. But there’s a more general slice type too.

```rust
let a = [1, 2, 3, 4, 5];
```

Just as we might want to refer to part of a string, we might want to refer to part of an array. We’d do so like this:

```rust
let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];

assert_eq!(slice, &[2, 3]);
```

This slice has the type `&[i32]`. It works the same way as string slices do, by storing a reference to the first element and a length.

## 🥳 OVER