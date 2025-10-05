# Functions

We define a function in Rust by entering `fn` followed by a function name and a set of parentheses.

```rust
fn main() {
    // rust code here
}
```

Rust code uses **snake case** as the conventional style for function and variable names, in which all letters are lowercase and underscores separate words.

## 👉 Parameters

Parameters are special variables that are part of a function’s signature. When a function has parameters, you can provide it with concrete values for those parameters. Technically, the concrete values are called **arguments**.

```rust
fn another_function(x: i32) {
    // function code here
}
```

In function signatures, you must declare the **type** of each parameter.

When defining multiple parameters, separate the parameter declarations with commas.

## 👉 Statements and Expressions

Rust is an expression-based language 🥳.

- **Statements** - Instructions that perform some action and do not return a value.
- **Expressions** - Evaluate to a resultant value.

### 👉 Statements
---

Creating a variable and assigning a value to it with the let keyword is a statement.

Function definitions are statements.

Statements do not return values. Therefore, you can’t assign a let statement to another variable, like : 

```rust
fn main() {
    let x = (let y = 6); // Error 
}
```

The `let y = 6` statement does not return a value, so there isn’t anything for `x` to bind to.

### 👉 Expressions
---

Expressions evaluate to a value, such as 5 + 6, which is an expression that evaluates to the value 11. 

Expressions can be part of statements: the 6 in the statement `let y = 6;` is an expression that evaluates to the value 6. 

Calling a function is an expression. 

Calling a macro is an expression. 

A new scope block created with curly brackets is an expression, For example - 

```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };
}
```

Expressions **do not include ending semicolons**. If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value.

## 👉 Functions with Return Values

**Functions** can return values to the code that calls them. We don’t name return values, but we must declare their type after an arrow **(->)**. 

In Rust, the return value of the function is synonymous with the value of the **final expression** in the block of the body of a function. 

You can return early from a function by using the `return` keyword and specifying a value, but most functions return the **last expression implicitly**.

```rust
fn five() -> i32 {
    5
}
```