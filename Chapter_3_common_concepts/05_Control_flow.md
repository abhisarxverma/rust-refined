# Control Flow

The ability to run some code depending on whether a condition is `true` and to run some code repeatedly while a condition is `true`.

## 👉 If Expressions

All if expressions start with the keyword if, followed by a condition.

Blocks of code associated with the conditions in if expressions are sometimes called **arms**.

Optionally, we can also include an `else` expression to give the program an alternative block of code to execute should the condition evaluate to `false`.

The condition in this code must be a `bool`. If the condition isn’t a `bool`, we’ll get an **error**.

Unlike languages such as Ruby and JavaScript, Rust will not automatically try to convert non-Boolean types to a Boolean. You must be explicit and always provide if with a Boolean as its condition.

## 👉 Handling Multiple Conditions with else if

You can use **multiple conditions** by combining `if` and `else` in an `else if` expression.

Using too many `else if` expressions can clutter your code. Chapter 6 describes a powerful Rust branching construct called `match` for these cases.

## 👉 Using if in a let Statement

Because if is an expression, we can use it on the right side of a let statement to assign the outcome to a variable.

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}"); // number is 5
}
```

Remember that blocks of code evaluate to the **last expression** in them, and **numbers by themselves are also expressions**. 

The value of the whole if expression depends on which block of code executes. This means the values that have the potential to be results from each arm of the if must be the **same type**.

If the types are mismatched, we will get error.

## 👉 Repetition with loops

Rust has three kinds of loops: `loop`, `while`, and `for`.

### 👉 Repeating Code with loop

The `loop` keyword tells Rust to execute a block of code over and over again forever or until you explicitly tell it to stop.

- `break` keyword - a way to **break out** of a loop using code. You can place the `break` keyword within the loop to tell the program when to stop executing the loop.

- `continue` keyword - tells the program to **skip over** any remaining code in this iteration of the loop and go to the next iteration.

### 👉 Returning Values from Loops

You can pass the result of that operation out of the loop to the rest of your code. 

To do this, you can add the value you want returned after the `break` expression you use to stop the loop.

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```
You can also `return` from inside a loop. While `break` only exits the current loop, **return always exits the current function**.

## 👉 Loop Labels to Disambiguate Between Multiple Loops

If you have loops within loops, `break` and `continue` apply to the innermost loop at that point. 

You can optionally specify a **loop label** on a loop that you can then use with `break` or `continue` to specify that those keywords apply to the labeled loop instead of the innermost loop. 

Loop labels must begin with a **single quote**.

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

## 👉 Conditional Loops with while

While the condition is `true`, the loop runs. When the condition ceases to be `true`, the program calls `break`, stopping the loop.

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

## 👉 Looping Through a Collection with for

You can use a `for` loop and execute some code for each item in a collection.

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

For loops are more efficient and save than while loops for iterating over a sequence and execute some code for each.

#### 👉 Range

Range is provided by the **standard library**, which **generates all numbers in sequence** starting from one number and ending before another number.

```rust
fn main() {
    for number in (1..4).rev() {  // .rev() reverses the range
        println!("{number}!");
    }
}
```

### 🥳 Chapter completed....