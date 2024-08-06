## 5. Error Handling in a Functional Style

Error handling is a crucial aspect of programming, and Rust provides powerful tools to manage errors safely and effectively. In this section, we will explore the `Result` and `Option` types, pattern matching for error handling, and functional error propagation techniques.

### Using `Result` and `Option` Types

Rust has two primary types for handling errors and optional values: `Result` and `Option`.

#### `Result` Type

The `Result` type is used for functions that can return an error. It is an enum that can be either `Ok` (indicating success) or `Err` (indicating failure).

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Here’s an example of a function that returns a `Result`:

```rust
fn divide(numerator: f64, denominator: f64) -> Result<f64, String> {
    if denominator == 0.0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(numerator / denominator)
    }
}
```

You can use this function as follows:

```rust
fn main() {
    match divide(10.0, 2.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e),
    }

    match divide(10.0, 0.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e), // Output: Error: Cannot divide by zero
    }
}
```

#### `Option` Type

The `Option` type is used for values that may or may not be present. It can be either `Some` (indicating a value) or `None` (indicating no value).

```rust
enum Option<T> {
    Some(T),
    None,
}
```

Here’s an example of a function that returns an `Option`:

```rust
fn find_item(index: usize) -> Option<&'static str> {
    let items = ["apple", "banana", "cherry"];
    if index < items.len() {
        Some(items[index])
    } else {
        None
    }
}
```

You can use this function as follows:

```rust
fn main() {
    match find_item(1) {
        Some(item) => println!("Found: {}", item),
        None => println!("Item not found"),
    }

    match find_item(5) {
        Some(item) => println!("Found: {}", item),
        None => println!("Item not found"), // Output: Item not found
    }
}
```

### Pattern Matching for Error Handling

Pattern matching is a powerful feature in Rust that allows you to handle different cases of `Result` and `Option` types concisely.

#### Example with `Result`

You can use pattern matching to handle errors gracefully:

```rust
fn main() {
    let result = divide(10.0, 0.0);
    
    match result {
        Ok(value) => println!("Division result: {}", value),
        Err(err) => println!("Error occurred: {}", err), // Output: Error occurred: Cannot divide by zero
    }
}
```

#### Example with `Option`

Pattern matching can also be used with `Option`:

```rust
fn main() {
    let item = find_item(2);
    
    match item {
        Some(name) => println!("Item found: {}", name),
        None => println!("No item found"), // Output: No item found
    }
}
```

### Functional Error Propagation Techniques

Rust provides convenient methods for propagating errors using the `?` operator, which simplifies error handling by returning early from a function if an error occurs.

#### Using the `?` Operator

Here’s how to use the `?` operator with the `Result` type:

```rust
fn safe_divide(numerator: f64, denominator: f64) -> Result<f64, String> {
    let result = divide(numerator, denominator)?;
    Ok(result)
}
```

In this example, if `divide` returns an `Err`, the `safe_divide` function will return that error immediately.

#### Example with `Option`

You can also use the `?` operator with `Option`:

```rust
fn get_item_length(index: usize) -> Option<usize> {
    let item = find_item(index)?;
    Some(item.len())
}
```

In this case, if `find_item` returns `None`, `get_item_length` will also return `None`.

### Summary

In this section, we covered error handling in Rust using the `Result` and `Option` types, explored pattern matching for effective error management, and learned about functional error propagation techniques using the `?` operator. These tools enable you to write robust and safe code that gracefully handles errors. In the next lesson, we will explore concurrency in Rust, enhancing our ability to write multi-threaded applications.
