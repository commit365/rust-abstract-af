## 3. Immutability and Data Structures

### Emphasizing Immutability in Rust

Immutability is a core principle in Rust, promoting safer and more predictable code. By default, variables in Rust are immutable, meaning once a value is assigned, it cannot be changed. This helps prevent unintended side effects and makes reasoning about code easier.

#### Declaring Immutable Variables

When you declare a variable with `let`, it is immutable:

```rust
let x = 5;
// x = 10; // This will cause a compile-time error
```

If you need a mutable variable, you can use the `mut` keyword:

```rust
let mut y = 10;
y = 15; // This is allowed because `y` is mutable
println!("y: {}", y); // Output: y: 15
```

### Using Tuples and Structs for Data Representation

Rust provides several ways to group related data together. Two common data structures are tuples and structs.

#### Tuples

Tuples are fixed-size collections that can hold multiple values of different types. They are defined using parentheses:

```rust
let person: (&str, i32) = ("Alice", 30);
println!("Name: {}, Age: {}", person.0, person.1); // Output: Name: Alice, Age: 30
```

You can also destructure tuples for easier access:

```rust
let (name, age) = person;
println!("Name: {}, Age: {}", name, age); // Output: Name: Alice, Age: 30
```

#### Structs

Structs are custom data types that allow you to define a collection of related data with named fields. They are defined using the `struct` keyword:

```rust
struct Person {
    name: String,
    age: i32,
}

let alice = Person {
    name: String::from("Alice"),
    age: 30,
};

println!("Name: {}, Age: {}", alice.name, alice.age); // Output: Name: Alice, Age: 30
```

You can also create methods for structs using `impl`:

```rust
impl Person {
    fn greet(&self) {
        println!("Hello, my name is {}.", self.name);
    }
}

alice.greet(); // Output: Hello, my name is Alice.
```

### Pattern Matching with Enums

Enums (short for enumerations) allow you to define a type that can be one of several variants. They are particularly useful when combined with pattern matching, enabling elegant handling of different data states.

#### Defining Enums

Here’s how to define a simple enum:

```rust
enum Direction {
    North,
    South,
    East,
    West,
}

let direction = Direction::North;
```

#### Pattern Matching

You can use pattern matching to execute different code based on the enum variant:

```rust
match direction {
    Direction::North => println!("Heading North!"),
    Direction::South => println!("Heading South!"),
    Direction::East => println!("Heading East!"),
    Direction::West => println!("Heading West!"),
}
```

#### Enums with Data

Enums can also hold data, allowing for more complex representations:

```rust
enum Message {
    Quit,
    ChangeColor(u32, u32, u32), // RGB values
    Move { x: i32, y: i32 }, // Named fields
}

let msg = Message::ChangeColor(255, 0, 0);

match msg {
    Message::Quit => println!("Quit"),
    Message::ChangeColor(r, g, b) => println!("Change color to RGB({}, {}, {})", r, g, b),
    Message::Move { x, y } => println!("Move to ({}, {})", x, y),
}
```

### Summary

In this section, we emphasized the importance of immutability in Rust, explored how to use tuples and structs for data representation, and learned about pattern matching with enums. These concepts are fundamental to writing safe and effective Rust code. In the next lesson, we will delve into traits and generics, further enhancing our understanding of Rust's capabilities.