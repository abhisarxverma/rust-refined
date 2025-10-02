# 3 : Variables and Mutability

## In Rust, by default, variables are immutable 🥳

When a variable is immutable, once a value is bound to a name, you can’t change that value.

**Although variables are immutable by default, you can make them mutable by adding `mut` in front of the variable name.**

## 👉 Constants

Like immutable variables, constants are values that are bound to a name and are not allowed to change, but there are a few differences between constants and variables.

You aren’t allowed to use mut with constants. Constants aren’t just immutable by default—they’re **always immutable**. You declare constants using the `const` keyword instead of the `let` keyword, and the **type of the value must be annotated**.

Constants can be declared in any scope, including the global scope.

Constants may be set only to a **constant expression**, not the result of a value that could only be computed at runtime.

Rust’s naming convention for constants is to use **all uppercase with underscores between words**. For example -

```rust
const MAXIMUM_MARKS: u32 = 100;
```

Constants are valid for the entire time a program runs, within the scope in which they were declared.

## 👉 Shadowing

You can declare a new variable with the same name as a previous variable. ***Rustaceans*** say that the first variable is shadowed by the second, which means that the second variable is what the compiler will see when you use the name of the variable.

We can shadow a variable by using the same variable’s name and repeating the use of the `let` keyword.

Shadowing is different from marking a variable as `mut` because we’ll get a **compile-time error** if we accidentally try to reassign to this variable without using the `let` keyword. By using `let`, we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.

The other difference between `mut` and shadowing is that because we’re effectively creating a new variable when we use the `let` keyword again, we can **change the type of the value but reuse the same name**.

```rust
fn main() {
    let spaces = "   ";          // string type
    let spaces = spaces.len();   // gets changed to number type
}
```

## 🥳 Over
