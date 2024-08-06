## 2. Functional Programming Concepts

### Understanding Functional Programming Principles

Functional programming (FP) is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing state and mutable data. Key principles of functional programming include:

- **Immutability**: Data should not be changed after it is created. Instead of modifying existing data, new data structures are created.
- **First-Class Functions**: Functions are treated as first-class citizens, meaning they can be assigned to variables, passed as arguments, and returned from other functions.
- **Pure Functions**: Functions that, given the same input, always produce the same output and have no side effects (e.g., they do not modify global state).
- **Function Composition**: The ability to combine simple functions to create more complex ones.

### First-Class Functions and Closures

In Rust, functions are first-class citizens. This means you can assign functions to variables, pass them as arguments, and return them from other functions.

#### Defining Functions

Here’s how to define a simple function in Rust:

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

You can assign this function to a variable:

```rust
let sum = add; // `sum` is now a function pointer
let result = sum(5, 3); // Calls `add(5, 3)`
println!("Result: {}", result); // Output: Result: 8
```

#### Closures

Closures are anonymous functions that can capture their environment. They are defined using the `||` syntax:

```rust
let multiply = |x: i32, y: i32| x * y;
let result = multiply(4, 5);
println!("Result: {}", result); // Output: Result: 20
```

Closures can capture variables from their surrounding scope:

```rust
let factor = 3;
let closure = |x: i32| x * factor; // Captures `factor`
let result = closure(10);
println!("Result: {}", result); // Output: Result: 30
```

### Higher-Order Functions and Their Applications

Higher-order functions are functions that take other functions as arguments or return them as results. They are a powerful feature of functional programming.

#### Example: Map

The `map` function applies a given function to each element of a collection and returns a new collection. Here’s how to use it with Rust’s iterator:

```rust
let numbers = vec![1, 2, 3, 4, 5];
let squares: Vec<i32> = numbers.iter().map(|&x| x * x).collect();
println!("Squares: {:?}", squares); // Output: Squares: [1, 4, 9, 16, 25]
```

#### Example: Filter

The `filter` function creates a new collection with elements that satisfy a specific condition:

```rust
let even_numbers: Vec<i32> = numbers.iter().filter(|&&x| x % 2 == 0).copied().collect();
println!("Even Numbers: {:?}", even_numbers); // Output: Even Numbers: [2, 4]
```

#### Example: Reduce

The `fold` function (similar to reduce) combines all elements of a collection into a single value:

```rust
let sum: i32 = numbers.iter().fold(0, |acc, &x| acc + x);
println!("Sum: {}", sum); // Output: Sum: 15
```

### Summary

In this section, we explored functional programming concepts in Rust, including first-class functions, closures, and higher-order functions. These features allow you to write expressive and powerful code, leveraging the functional programming paradigm. In the next lesson, we will dive into immutability and data structures in Rust.
