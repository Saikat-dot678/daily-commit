# Rust Variables, Binding, and Mutability 🦀

This guide covers the fundamental concepts of variables in Rust, including binding, mutability, scope, and shadowing, followed by solutions to the exercises from practice.course.rs.

-----

## Theory

In Rust, variables are not just containers for data; they are **bindings** of a name to a value. The language is designed for safety and concurrency, and its handling of variables is a core part of that design.

### 1\. Bindings & Immutability

In many languages, variables are mutable by default. In Rust, it's the opposite. When you declare a variable using the `let` keyword, it is **immutable**.

```rust
fn main() {
    let x = 5;
    // The line below will cause a compiler error!
    // x = 6; 
    println!("The value of x is: {}", x);
}
```

> **Error:** `cannot assign twice to immutable variable 'x'`

This is a deliberate design choice. It encourages you to think about how data flows through your program, leading to safer, more predictable code, especially in concurrent situations.

### 2\. Mutability

Of course, you often need to change a variable's value. To do this, you can make a variable **mutable** by adding the `mut` keyword in front of its name.

```rust
fn main() {
    let mut y = 5;
    println!("The initial value of y is: {}", y);
    y = 6; // This is now allowed because 'y' is mutable.
    println!("The new value of y is: {}", y);
}
```

### 3\. Initialization

Rust guarantees that a variable will not be used before it is given an initial value. Attempting to use a variable that has been declared but not initialized will result in a compile-time error.

```rust
fn main() {
    let x: i32;
    // The line below will cause a compiler error because 'x' is not initialized.
    // println!("The value of x is: {}", x); 
}
```

### 4\. Scope

A variable's **scope** is the region of the program where it is valid. In Rust, a scope is typically defined by a block of code enclosed in curly braces `{}`. A variable declared inside a scope is only accessible within that scope and its child scopes.

```rust
fn main() {
    let outer_var = "I'm outside";
    {
        // This is a new scope
        let inner_var = "I'm inside";
        println!("From inner scope: {}", outer_var); // Works!
        println!("From inner scope: {}", inner_var); // Works!
    }
    println!("From outer scope: {}", outer_var); // Works!
    // The line below would cause an error because 'inner_var' is out of scope.
    // println!("From outer scope: {}", inner_var);
}
```

### 5\. Shadowing

Rust allows you to declare a new variable with the same name as a previous variable. This is called **shadowing**. The new variable "shadows" the previous one, and any use of the name will refer to the new variable until it goes out of scope.

```rust
fn main() {
    let x = 5;
    let x = x + 1; // 'x' is now 6.

    {
        let x = x * 2; // 'x' is shadowed again, now it's 12.
        println!("The value of x in the inner scope is: {}", x); // Prints 12
    }

    println!("The value of x is: {}", x); // Prints 6
}
```

Shadowing is different from marking a variable as `mut`.

  * You must use the `let` keyword to shadow.
  * You can change the type of the variable when shadowing, which you cannot do with a `mut` variable.

### 6\. Unused Variables

If you declare a variable and don't use it, the Rust compiler will issue a helpful warning. If this is intentional, you can tell the compiler by starting the variable name with an underscore `_`.

```rust
fn main() {
    let _unused_variable = 3; // No warning
    let used_variable = 5;    // Warning if this is not used later
    println!("{}", used_variable);
}
```

### 7\. Destructuring

You can use a pattern with `let` to break apart, or **destructure**, a tuple, struct, or enum into separate variables.

```rust
fn main() {
    let (a, b) = (10, 20); // 'a' is 10, 'b' is 20
    println!("a: {}, b: {}", a, b);
}
```

This also works in assignments for mutable variables, a feature known as **destructuring assignments**. The `..` syntax can be used to ignore parts of the structure.

```rust
fn main() {
    let (mut x, mut y) = (1, 2);
    (x, y) = (3, 4); // Destructuring assignment

    let (z, ..) = (10, 20); // 'z' is 10, the rest is ignored
    println!("x: {}, y: {}, z: {}", x, y, z);
}
```

-----

## Solutions

### Binding and mutability

**Problem 1**

```rust
// Fix the error below with least amount of modification to the code
fn main() {
    let x: i32; // Uninitialized but used, ERROR !
    let y: i32; // Uninitialized but also unused, only a Warning !
    assert_eq!(x, 5);
    println!("Success!");
}
```

**Solution**

```rust
// Fix the error below with least amount of modification to the code
fn main() {
    let x: i32 = 5; // Initialize x
    let _y: i32; // Add underscore to silence the warning
    assert_eq!(x, 5);
    println!("Success!");
}
```

**Explanation:** The error occurs because `x` is used in `assert_eq!` without being initialized. We fix this by assigning it the value `5`. We also add an underscore to `_y` to let the compiler know its being unused is intentional.

-----

**Problem 2**

```rust
// Fill the blanks in the code to make it compile
fn main() {
    let __ __ = 1;
    __ += 2; 
    assert_eq!(x, 3);
    println!("Success!");
}
```

**Solution**

```rust
// Fill the blanks in the code to make it compile
fn main() {
    let mut x = 1;
    x += 2; 
    assert_eq!(x, 3);
    println!("Success!");
}
```

**Explanation:** To change the value of a variable, it must be declared as mutable. We declare `x` with `let mut x = 1;` so we can later reassign its value with `x += 2;`.

-----

### Scope

**Problem 1**

```rust
// Fix the error below with least amount of modification
fn main() {
    let x: i32 = 10;
    {
        let y: i32 = 5;
        println!("Inner scope value of x is {} and value of y is {}", x, y);
    }
    println!("Outer scope value of x is {} and value of y is {}", x, y);
}
```

**Solution**

```rust
// Fix the error below with least amount of modification
fn main() {
    let x: i32 = 10;
    let y: i32 = 5; // Move declaration to the outer scope
    {
        println!("Inner scope value of x is {} and value of y is {}", x, y);
    }
    println!("Outer scope value of x is {} and value of y is {}", x, y);
}
```

**Explanation:** The variable `y` was declared inside the inner scope, so it was not accessible in the outer scope for the second `println!`. By moving its declaration to the outer scope, it becomes accessible to both print statements.

-----

**Problem 2**

```rust
// Fix the error with the use of define_x
fn main() {
    println!("{}, world", x); 
}

fn define_x() {
    let x = "hello";
}
```

**Solution**

```rust
// Fix the error with the use of define_x
fn main() {
    let x = define_x(); // Call the function to get the value
    println!("{}, world", x); 
}

fn define_x() -> String {
    let x = "hello".to_string();
    x // Return the value
}
```

**Explanation:** The `main` function cannot access the `x` variable defined in `define_x` due to scope rules. To fix this, we modify `define_x` to return the `String` value. Then, in `main`, we call the function and bind its return value to a new variable `x`.

-----

### Shadowing

**Problem 1**

```rust
// Only modify `assert_eq!` to make the `println!` work(print `42` in terminal)
fn main() {
    let x: i32 = 5;
    {
        let x = 12;
        assert_eq!(x, 5);
    }
    assert_eq!(x, 12);
    let x = 42;
    println!("{}", x); // Prints "42".
}
```

**Solution**

```rust
// Only modify `assert_eq!` to make the `println!` work(print `42` in terminal)
fn main() {
    let x: i32 = 5;
    {
        let x = 12; // This 'x' shadows the outer 'x' and is 12
        assert_eq!(x, 12);
    }
    // The inner 'x' is out of scope, the outer 'x' is 5 again
    assert_eq!(x, 5);
    let x = 42; // The outer 'x' is shadowed again
    println!("{}", x); // Prints "42".
}
```

**Explanation:** Inside the inner block, `x` is shadowed and its value is `12`. Once that block ends, the inner `x` goes out of scope, and the original `x` (with value `5`) is visible again.

-----

**Problem 2**

```rust
// Remove a line in the code to make it compile
fn main() {
    let mut x: i32 = 1;
    x = 7;
    // Shadowing and re-binding
    let x = x; 
    x += 3;

    let y = 4;
    // Shadowing
    let y = "I can also be bound to text!"; 
    println!("Success!");
}
```

**Solution**

```rust
// Remove a line in the code to make it compile
fn main() {
    let mut x: i32 = 1;
    x = 7;
    // Shadowing and re-binding
    let x = x; // The new 'x' is immutable and has the value 7
    // x += 3; // This line is removed

    let y = 4;
    // Shadowing
    let y = "I can also be bound to text!"; 
    println!("Success!");
}
```

**Explanation:** The line `let x = x;` shadows the mutable `x` with a new, immutable `x`. Therefore, trying to modify it with `x += 3;` causes an error. Removing the line fixes the code.

-----

### Unused variables

**Problem**

```rust
fn main() {
    let x = 1;
}
// Warning: unused variable: `x`
```

**Solution**

```rust
fn main() {
    let _x = 1;
}
```

**Explanation:** Prefixing the variable name with an underscore `_` is the standard Rust convention to tell the compiler that you are intentionally not using this variable, which suppresses the warning.

-----

### Destructuring

**Problem**

```rust
// Fix the error below with least amount of modification
fn main() {
    let (x, y) = (1, 2);
    x += 2;

    assert_eq!(x, 3);
    assert_eq!(y, 2);

    println!("Success!");
}
```

**Solution**

```rust
// Fix the error below with least amount of modification
fn main() {
    let (mut x, y) = (1, 2);
    x += 2;

    assert_eq!(x, 3);
    assert_eq!(y, 2);

    println!("Success!");
}
```

**Explanation:** Just like with regular `let` bindings, variables created via destructuring are immutable by default. To modify `x`, we need to make it mutable by adding `mut` inside the tuple pattern: `(mut x, y)`.

-----

### Destructuring assignments

**Problem**

```rust
fn main() {
    let (x, y);
    (x,..) = (3, 4);
    [.., y] = [1, 2];
    // Fill the blank to make the code work
    assert_eq!([x,y], __);
    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let (x, y);
    (x,..) = (3, 4); // x becomes 3, the rest of the tuple is ignored
    [.., y] = [1, 2]; // y becomes 2, the rest of the array is ignored
    // Fill the blank to make the code work
    assert_eq!([x,y], [3, 2]);
    println!("Success!");
}
```

**Explanation:**

  - The line `(x, ..) = (3, 4);` uses a destructuring assignment to bind `x` to the first element of the tuple, which is `3`. The `..` ignores any other elements.
  - The line `[.., y] = [1, 2];` binds `y` to the last element of the array, which is `2`.
  - Therefore, the array `[x, y]` is equal to `[3, 2]`.
