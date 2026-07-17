Of course\! Here is a complete guide to Rust's basic number types, followed by solutions to all the exercises on the page.

# Rust's Basic Number Types 🔢

This guide covers the fundamental concepts of number types in Rust, including integers, floating-point numbers, and numeric operations.

-----

## Theory

Rust is a statically typed language, which means that it must know the types of all variables at compile time. Number types are fundamental primitives in Rust and are divided into two main categories: **integers** and **floating-point numbers**.

### 1\. Integer Types

Integers are whole numbers. Rust provides several built-in integer types, which are categorized by their size (in bits) and whether they are **signed** or **unsigned**.

  * **Signed integers** (start with `i` for "integer") can store both positive and negative numbers. They use two's complement representation.
  * **Unsigned integers** (start with `u` for "unsigned") can only store non-negative numbers (zero and positive).

Here's a table of Rust's integer types:

| Size    | Signed | Unsigned | Range (Signed)                      | Range (Unsigned)       |
|---------|--------|----------|-------------------------------------|------------------------|
| 8-bit   | `i8`   | `u8`     | `-128` to `127`                     | `0` to `255`           |
| 16-bit  | `i16`  | `u16`    | `-32,768` to `32,767`               | `0` to `65,535`        |
| 32-bit  | `i32`  | `u32`    | `-2^31` to `2^31 - 1`               | `0` to `2^32 - 1`      |
| 64-bit  | `i64`  | `u64`    | `-2^63` to `2^63 - 1`               | `0` to `2^64 - 1`      |
| 128-bit | `i128` | `u128`   | `-2^127` to `2^127 - 1`             | `0` to `2^128 - 1`     |
| arch    | `isize`| `usize`  | Depends on the computer's architecture (32-bit or 64-bit) |

The `isize` and `usize` types are primarily used for indexing collections. The **default integer type** in Rust is `i32`.

You can write integer literals in several formats:

  * **Decimal**: `98_222`
  * **Hex**: `0xff`
  * **Octal**: `0o77`
  * **Binary**: `0b1111_0000`
  * **Byte** (`u8` only): `b'A'`

### 2\. Floating-Point Types

Rust also has two primitive types for floating-point numbers (numbers with a decimal point).

  * `f32`: 32-bit single-precision float.
  * `f64`: 64-bit double-precision float.

The **default floating-point type** is `f64` because on modern CPUs, it's roughly the same speed as `f32` but is capable of more precision.

```rust
fn main() {
    let x = 2.0; // f64 (default)
    let y: f32 = 3.0; // f32 (with type annotation)
}
```

### 3\. Numeric Operations

Rust supports the basic mathematical operations you’d expect: addition `+`, subtraction `-`, multiplication `*`, division `/`, and remainder `%`.

```rust
// integer division
let integer_division = 5 / 2; // result is 2

// float division
let float_division = 5.0 / 2.0; // result is 2.5
```

### 4\. Type Inference and Casting

The Rust compiler can usually infer the type of a number based on its value and how it's used. However, sometimes it needs help. For example, a number literal like `42` could be an `i32`, a `u8`, or any other integer type. If the type is ambiguous, you must add a **type annotation**.

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

Rust does **not** perform implicit type conversions (casting) between primitive types. You must do it explicitly using the `as` keyword.

```rust
let x: u8 = 10;
let y: u16 = 15;
// The line below would cause a type mismatch error
// let z = x + y;
// We must explicitly cast one of the variables
let z = (x as u16) + y;
```

Casting can be lossy. For example, casting a large `i32` to an `i8` will truncate the value.

-----

## Solutions

### Problem 1

```rust
// Remove the given line to make it work
fn main() {
    let x: i32 = 5;
    let mut y: u32 = 5;

    y = x; 
    
    let z = 10; // Type of z ? 

    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let x: i32 = 5;
    let mut y: u32 = 5;

    // y = x;  // This line is removed.
    
    let z = 10; // Type of z is i32 (default integer type)

    println!("Success!");
}
```

**Explanation:** Rust does not allow assigning a variable of one type (`i32`) to a variable of another type (`u32`) directly. Removing the line `y = x;` resolves the type mismatch error.

-----

### Problem 2

```rust
// Fill the blank
fn main() {
    let v: u16 = 38_u8 as __;

    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let v: u16 = 38_u8 as u16;

    println!("Success!");
}
```

**Explanation:** We are explicitly casting the `u8` value `38` into a `u16` type using the `as` keyword. This is a valid cast because `38` fits within the range of both `u8` and `u16`.

-----

### Problem 3

```rust
// Modify `assert_eq!` to make it work
fn main() {
    let x = 5;
    assert_eq!("i32".to_string(), type_of(&x));

    println!("Success!");
}

// Get the type of given variable, return a string representation of the type
fn type_of<T>(_: &T) -> String {
    format!("{}", std::any::type_name::<T>())
}
```

**Solution**

```rust
fn main() {
    let x: u32 = 5; // Add type annotation
    assert_eq!("u32".to_string(), type_of(&x));

    println!("Success!");
}

// Get the type of given variable, return a string representation of the type
fn type_of<T>(_: &T) -> String {
    format!("{}", std::any::type_name::<T>())
}
```

**Explanation:** By default, Rust infers the type of `x` as `i32`. The assertion expects the type to be `u32`. We add an explicit type annotation `let x: u32 = 5;` to make `x` a `u32` and satisfy the assertion.

-----

### Problem 4

```rust
// Fill the blanks to make it work
fn main() {
    assert_eq!(i8::MAX, __); 
    assert_eq!(u8::MAX, __); 

    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    assert_eq!(i8::MAX, 127); 
    assert_eq!(u8::MAX, 255); 

    println!("Success!");
}
```

**Explanation:** The `MAX` constant associated with a numeric type gives its maximum possible value. For an `i8`, the range is -128 to 127. For a `u8`, the range is 0 to 255.

-----

### Problem 5

```rust
// Fix errors and panics to make it work
fn main() {
   let v1 = 251_u8 + 8;
   let v2 = i8::checked_add(251, 8).unwrap();
   println!("{},{}",v1,v2);
}
```

**Solution**

```rust
fn main() {
   let v1 = 251_u16 + 8; // Change u8 to u16 to avoid overflow
   let v2 = i8::checked_add(127, -8).unwrap(); // Use values within i8 range
   println!("{},{}", v1, v2);
}
```

**Explanation:**

1.  `251_u8 + 8` results in `259`, which overflows the `u8` type (max 255). We change `251_u8` to `251_u16`, which can easily hold the result.
2.  `i8::checked_add(251, 8)` fails because `251` is not a valid `i8` value. `checked_add` performs addition and returns `None` if overflow occurs. We change the values to `127` and `-8`, which are valid `i8`s and their sum `119` does not overflow.

-----

### Problem 6

```rust
// Modify `assert!` to make it work
fn main() {
    let v = 1_000_000_000_000i64; // f64
    let f = 0.52f64;
    assert!(v as f64 * f == 520_000_000_000.0);

    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let v = 1_000_000_000_000i64;
    let f = 0.52f64;
    assert!(v as f64 * f == 520_000_000_000.0);

    println!("Success!");
}
```

**Explanation:** The original code had a comment suggesting `v` was `f64`, but it was an `i64`. The assertion correctly casts `v` to an `f64` for the multiplication. The code was already correct; no changes were needed beyond potentially removing the misleading comment.

-----

### Problem 7

```rust
// Fill the blank to make it work
fn main() {
    let x = 5;
    let y = 10;
    
    // Oups, x is i32, but y is i64.
    // We need to cast x to i64 to make it work.
    let z = y + x as i64;
    
    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let x: i32 = 5;
    let y: i64 = 10; // Add type annotation to make y an i64
    
    let z = y + x as i64;
    
    println!("Success!");
}
```

**Explanation:** The code as written would infer `y` as an `i32`, making the cast unnecessary but harmless. To match the problem's intent of demonstrating a type mismatch, we explicitly annotate `y` as `i64`. Then, to perform the addition, we must cast `x` from `i32` to `i64` to match `y`'s type.

-----

### Problem 8

```rust
// Fill the blank to make it work
fn main() {
    let mut sum = 0;
    for i in -3..2 {
        sum += i
    }

    assert!(sum == -5);

    for c in 'a'..='z' {
        println!("{}",c);
    }
}
```

**Solution**

```rust
fn main() {
    let mut sum = 0;
    for i in -3..2 {
        sum += i
    }

    assert!(sum == -5); // The sum is -3 + -2 + -1 + 0 + 1 = -5

    for c in 'a'..='z' { // Use ..= for an inclusive range
        println!("{}", c as u8); // Print the ASCII value of the character
    }
}
```

**Explanation:**

1.  The first loop correctly calculates the sum of the range `-3, -2, -1, 0, 1`.
2.  The `for c in 'a'..='z'` loop iterates through characters. Using `..=` creates a range that is inclusive of the end value (`'z'`). We print the `u8` value of each character to see its ASCII code.

-----

### Problem 9

```rust
// Fill the blank
fn main() {
    let x = 1_000.000_1; // f64
    let y: f32 = 0.12;
    let z = x as f32 - y;

    assert_eq!(z, __);

    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let x = 1_000.000_1; // f64
    let y: f32 = 0.12;
    let z = x as f32 - y;

    assert_eq!(z, 1000.0 - 0.12); // Approximate result

    println!("Success!");
}
```

**Explanation:** The `f64` value `x` is cast to an `f32`. This cast is lossy; `1_000.000_1` loses precision and becomes `1000.0` as an `f32`. Then, `0.12` is subtracted. The assertion is modified to reflect this loss of precision. *Note: Floating-point arithmetic can be imprecise, and this problem highlights the potential data loss when casting from a higher-precision float to a lower-precision one.*

-----

### Problem 10

```rust
// Fix the errors
fn main() {
    let mut sum = 0;
    for i in -3..2 {
        sum += i
    }

    assert!(sum == -5);

    for c in 'a'..='z' {
        println!("{}",c);
    }
}
```

**Solution**

```rust
fn main() {
    let mut sum = 0;
    for i in -3..2 {
        sum += i
    }

    assert!(sum == -5);

    for c in 'a'..='z' { // Use ..= for an inclusive range
        println!("{}", c as u8);
    }
}
```

**Explanation:** This appears to be a duplicate of an earlier problem. The range `'a'..='z'` must be inclusive to include 'z'. We also print the character's `u8` value.

-----

### Computations

```rust
// Fill the blank and fix the error
fn main() {
    let v = {
        let mut x = 1;
        x += 2
    };

    assert_eq!(v, __);

    let v = {
        let x = 3;
        x
    };
    
    assert!(v == 3);
    
    println!("Success!");
}
```

**Solution**

```rust
fn main() {
    let v = {
        let mut x = 1;
        x += 2;
        x // Add x here to make the block evaluate to it
    };

    assert_eq!(v, 3);

    let v = {
        let x = 3;
        x
    };
    
    assert!(v == 3);
    
    println!("Success!");
}
```

**Explanation:** In Rust, a block `{}` can be an expression that evaluates to a value. The value of the block is the last expression in it. In the first block, `x += 2` is a statement and does not return a value, so the block defaults to returning `()`. By adding `x` as the last line, we make the block evaluate to the final value of `x`, which is `3`.
