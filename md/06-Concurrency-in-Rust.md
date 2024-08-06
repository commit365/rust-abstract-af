## 6. Concurrency in Rust

Concurrency is an essential aspect of modern programming, allowing multiple tasks to be executed simultaneously. Rust provides a powerful concurrency model that emphasizes safety and performance. In this section, we will explore Rust's concurrency model, how to use threads and message passing, and functional approaches to concurrent programming.

### Overview of Rust's Concurrency Model

Rust's concurrency model is built around the concepts of ownership, borrowing, and types, which help prevent data races at compile time. This means that you can write concurrent code in Rust without worrying about common pitfalls associated with multi-threading, such as race conditions and deadlocks.

Key features of Rust's concurrency model include:

- **Ownership and Borrowing**: Rust ensures that data is either mutable and owned by one thread or immutable and shared among multiple threads.
- **Send and Sync Traits**: Rust provides traits to indicate whether types can be safely transferred between threads (`Send`) or accessed by multiple threads (`Sync`).
- **Fearless Concurrency**: By enforcing these rules at compile time, Rust allows developers to write concurrent code confidently.

### Using Threads and Message Passing

Rust provides a straightforward way to create and manage threads using the standard library. The `std::thread` module allows you to spawn threads and communicate between them.

#### Spawning Threads

Here’s how to create a simple thread in Rust:

```rust
use std::thread;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..5 {
            println!("Hello from the thread! {}", i);
        }
    });

    // Wait for the thread to finish
    handle.join().unwrap();

    println!("Thread has finished execution.");
}
```

In this example, a new thread is spawned, and it prints messages in a loop. The `join` method is called to wait for the thread to complete before continuing.

#### Message Passing

Message passing is a common way to communicate between threads in Rust. The `std::sync::mpsc` module provides channels for sending messages.

Here’s an example of using channels for message passing:

```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    // Create a channel
    let (tx, rx) = mpsc::channel();

    let handle = thread::spawn(move || {
        for i in 1..5 {
            tx.send(i).unwrap(); // Send messages through the channel
        }
    });

    // Receive messages in the main thread
    for received in rx {
        println!("Received: {}", received);
    }

    handle.join().unwrap();
}
```

In this example, a channel is created, and the sender (`tx`) sends messages to the receiver (`rx`). The main thread receives and prints the messages.

### Functional Approaches to Concurrent Programming

Rust also supports functional programming techniques that can be applied to concurrency, such as using iterators and higher-order functions.

#### Using Iterators

You can use iterators to process collections in parallel. The `rayon` crate provides an easy way to achieve parallelism with iterators.

First, add `rayon` to your `Cargo.toml`:

```toml
[dependencies]
rayon = "1.5"
```

Then, you can use it as follows:

```rust
use rayon::prelude::*;

fn main() {
    let numbers = vec![1, 2, 3, 4, 5];

    let squares: Vec<i32> = numbers.par_iter() // Use parallel iterator
        .map(|&x| x * x)
        .collect();

    println!("Squares: {:?}", squares); // Output: Squares: [1, 4, 9, 16, 25]
}
```

In this example, `par_iter` allows the computation of squares to be distributed across multiple threads, leveraging parallelism for improved performance.

#### Functional Concurrency with Futures

For more advanced concurrency patterns, Rust provides the `async` and `await` syntax for asynchronous programming. You can use the `tokio` or `async-std` libraries to work with asynchronous tasks.

Here’s a simple example using `async-std`:

First, add `async-std` to your `Cargo.toml`:

```toml
[dependencies]
async-std = "1.10"
```

Then, you can write an asynchronous function:

```rust
use async_std::task;

async fn say_hello() {
    println!("Hello from async!");
}

fn main() {
    task::block_on(say_hello()); // Run the async function
}
```

### Summary

In this section, we explored Rust's concurrency model, focusing on its safety features and ease of use. We learned how to create and manage threads, utilize message passing for communication, and apply functional programming techniques to concurrent programming. Rust's concurrency capabilities allow you to write efficient and safe concurrent applications. In the next lesson, we will conclude the course with a recap of what we've learned and discuss next steps for further exploration in Rust.
