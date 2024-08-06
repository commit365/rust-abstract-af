## 7. Building a Functional Application

In this final section, we will walk through the process of building a functional application in Rust. We will cover project setup and structure, how to apply functional programming principles in a real-world application, and strategies for testing and debugging.

### Project Setup and Structure

To start building a Rust application, you'll need to set up your project using Cargo, Rust's package manager and build system.

#### Step 1: Create a New Project

Open your terminal and create a new Rust project:

```bash
cargo new functional_app
cd functional_app
```

This command creates a new directory called `functional_app` with the following structure:

```
functional_app/
├── Cargo.toml
└── src
    └── main.rs
```

- **Cargo.toml**: This file contains metadata about your project and its dependencies.
- **src/main.rs**: This is the main source file where your application code will reside.

#### Step 2: Organize Your Code

You can organize your code into modules for better structure. For example, create a directory called `src/lib.rs` for your library code and `src/main.rs` for the executable.

```rust
// src/lib.rs
pub mod math;
```

```rust
// src/math.rs
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}

pub fn multiply(a: i32, b: i32) -> i32 {
    a * b
}
```

```rust
// src/main.rs
use functional_app::math;

fn main() {
    let sum = math::add(5, 10);
    let product = math::multiply(4, 3);
    println!("Sum: {}, Product: {}", sum, product);
}
```

### Applying Functional Programming Principles in a Real-World Application

Let’s create a simple functional application that processes a list of numbers, applying functional programming principles like immutability, higher-order functions, and pattern matching.

#### Example: Number Processing Application

1. **Define Your Data**: Use an immutable vector to hold your numbers.

```rust
// src/main.rs
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    let squares: Vec<i32> = numbers.iter().map(|&x| x * x).collect();
    let sum: i32 = squares.iter().sum();
    
    println!("Squares: {:?}", squares);
    println!("Sum of squares: {}", sum);
}
```

2. **Use Higher-Order Functions**: Leverage functions like `map` and `filter` to process your data.

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    
    // Get squares of even numbers
    let even_squares: Vec<i32> = numbers
        .iter()
        .filter(|&&x| x % 2 == 0) // Filter even numbers
        .map(|&x| x * x) // Square them
        .collect();
    
    println!("Even squares: {:?}", even_squares);
}
```

### Testing and Debugging Strategies

Testing and debugging are essential for ensuring your application works correctly. Rust provides built-in support for testing.

#### Step 1: Writing Tests

You can write tests in Rust by creating a `tests` module in your source file or in a separate file under the `tests` directory.

```rust
// src/lib.rs
pub mod math;

#[cfg(test)]
mod tests {
    use super::math;

    #[test]
    fn test_add() {
        assert_eq!(math::add(2, 3), 5);
    }

    #[test]
    fn test_multiply() {
        assert_eq!(math::multiply(4, 5), 20);
    }
}
```

#### Step 2: Running Tests

To run your tests, use the following command in your terminal:

```bash
cargo test
```

This command will compile your code and run all the tests defined in your project, providing feedback on their success or failure.

#### Step 3: Debugging

If you encounter issues, Rust provides helpful debugging tools. You can use `println!` statements to output variable values at different stages of your program. Additionally, you can use the Rust debugger, `gdb`, or `lldb`, for more complex debugging tasks.

To run your application in debug mode, use:

```bash
cargo run
```

### Summary

In this section, we built a functional application in Rust, covering project setup and structure, applying functional programming principles, and implementing testing and debugging strategies. By leveraging Rust's features and functional programming concepts, you can create robust and maintainable applications. As you continue your journey with Rust, consider exploring more advanced topics and libraries to further enhance your skills. Happy coding!
