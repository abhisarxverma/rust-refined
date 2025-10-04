# Data Types

Rust is a statically typed language, which means that it must know the types of all variables at compile time.

## 👉 Scaler Types

A scalar type represents a single value. Rust has four primary scalar types -

- integers
- floating-point numbers
- Booleans
- characters

### 👉 Integer Types
---

An integer is a number without a fractional component. Ex - `u32` and `i32`.

Signed integer types start with `i` instead of `u`.

| Length               | Signed | Unsigned |
|----------------------|--------|----------|
| 8-bit                | i8     | u8       |
| 16-bit               | i16    | u16      |
| 32-bit               | i32    | u32      |
| 64-bit               | i64    | u64      |
| 128-bit              | i128   | u128     |
| Architecture dependent | isize  | usize    |

**Signed** and **unsigned** refer to whether the number needs to have a sign with it (signed) or whether it will only ever be positive and can therefore be represented without a sign (unsigned).

Signed variant : −(2<sup>n</sup> − 1) to 2<sup>n − 1</sup> − 1 inclusive.

where <em>n</em> is the number of bits that variant uses.

Unsigned variants : 0 to 2<sup>n</sup> − 1

### 👉 Floating-point Types
---

Rust also has two primitive types for floating-point numbers, which are numbers with decimal points. Rust’s floating-point types are `f32` and `f64`, which are 32 bits and 64 bits in size, respectively. The default type is `f64`.

#### 👉 Number operations
---

Rust supports the basic mathematical operations you’d expect for all the number types: addition, subtraction, multiplication, division, and remainder. Integer division truncates toward zero to the nearest integer.

```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // Results in -1

    // remainder
    let remainder = 43 % 5;
}
```

### 👉 The Boolean type
---

A Boolean type in Rust has two possible values: `true` and `false`. 

Booleans are **one byte** in size. The Boolean type in Rust is specified using `bool`.

### 👉 The Character type
---

Rust’s char type is the language’s most primitive alphabetic type.

We specify char literals with **single quotes**, as opposed to string literals, which use double quotes.

Rust’s char type is **four bytes** in size and represents a Unicode scalar value, which means it can represent a lot more than just ASCII. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid char values in Rust.

## 👉 Compound types

Compound types can group multiple values into one type.

### 👉 The Tuple type
---

A tuple is a general way of grouping together a number of values with a variety of types into one compound type. Tuples have a **fixed length**: once declared, they cannot grow or shrink in size.

We create a tuple by writing a comma-separated list of values inside parentheses.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

To get the individual values out of a tuple, we can use pattern matching to destructure a tuple value, like this:

```rust
let tup = (500, 6.4, 1);

let (x, y, z) = tup;
```

This is called **destructuring**.

We can also access a tuple element directly by using a period **(.)** followed by the index of the value we want to access. For example:

```rust
let x: (i32, f64, u8) = (500, 6.4, 1);

let five_hundred = x.0;

let six_point_four = x.1;
```

#### 👉 Unit

The tuple without any values has a special name, **unit**. This value and its corresponding type are both written **()** and represent an empty value or an empty return type. Expressions implicitly return the unit value if they don’t return any other value.

### 👉 The Array type
---

Another way to have a collection of multiple values is with an **array**. 

Unlike a tuple, every element of an array must have the same type. 

Arrays in Rust have a fixed length.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```

Arrays are useful when you want your data allocated on the **stack**, the same as the other types we have seen so far, rather than the **heap** or when you want to ensure you always have a fixed number of elements. 

An array isn’t as flexible as the **vector** type, though. 

👉 **Vector** - A vector is a similar collection type provided by the standard library that is allowed to grow or shrink in size because its contents live on the **heap**. If you’re unsure whether to use an array or a vector, chances are you should use a vector.

You write an array’s type using square brackets with the type of each element, a semicolon, and then the number of elements in the array, like so:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
let a = [3; 5]; // creates an array having 5 3's.
```

**Accessing** - Indexes in square brackets like `array[0]`.