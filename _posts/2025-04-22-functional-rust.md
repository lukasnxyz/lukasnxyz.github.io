---
layout: post
title: "Functional Programming in Rust"
author: "Lukas N"
published: false
---
Over the last few weeks, I've been thinking about how to level up my programming skills and
tackle problems from different angles before diving into solutions. I want to be the best
possible computer programmer I can be. I've always been curious about functional programming
more specifically Haskell, but I'll be honest — topics like lambda calculus and closures
create a larger barrier to entry than expected. That said, I've been using Rust a lot the
past couple of weeks and I've started programming with some functional aspects in mind. With
this article, I want to list some ways I've been writing software differently (mainly in
Rust) and things that I love about Rust where it allows me to express problems in a more
mathematical and functional way. This is by no means an exhaustive list, but simply a collection
features and functional aspects of Rust that I have started using and almost prefer now for
solving programming problems.

### Immutability by Default
This one is huge. This keeps your code clean by default and prevents you from making more
errors than needed. I truly believe all programming languages should make variables immutable
by default. If you're using C, use `const` for as many variables as you can. With Rust, you
don't have to get into the habit of making your variables `const` by default because they
are already immutable.

In Rust you just declare your variables and if you decide later on that you do have to change
it, just stick a `mut` after the `let`
```rust
let mut x: i32 = 3;
let y = 5;
x += 1;
println!("x: {}, y: {}", x, y);
```
Clean, simple, safe.

### Pattern Matching
Pattern matching is just switch statements on steroids. They're a nice and concise way to
model forms of data from simple integers values to complex tuples. In Rust you can just use
the `match` keyword to pattern match a specific variable.

```rust
fn fib(n: u32) -> u32 {
    match n {
        0 => 0,
        1 => 1,
        n => fib(n - 1) + fib(n - 2),
    }
}
```

### Closures (Lambdas)
Closures and lambdas are a bit difficult to understand by just reading a formal definition so
I'm just going to give you two examples to make it very easy.
```rust
let y = 2;
let add_one = |x: i32| x + 1; // lambda
let add_y = |x: i32| x + y; // closure
```
A lambda function is basically just a function that takes an input, doesn't depend on any
outside variables, and produces an output. A closure is the same thing, but with the output
depending on outside variables, in this example `y`. For very basic

### Iterators
### Combinators


- Algebraic Data Types


#### Sources
- [Functional Programming in Rust - Sylvian Kerkour](https://kerkour.com/rust-functional-programming)
- [Closure vs. Lambda - Stack Overflow](https://stackoverflow.com/questions/220658/what-is-the-difference-between-a-closure-and-a-lambda)


// pattern matching and recursion
fn fib(n: u32) -> u32 {
    match n {
        0 => 0,
        1 => 1,
        n => fib(n - 1) + fib(n - 2),
    }
}

fn main() {
    // immutability by default
    let mut x: i32 = 3;
    let y = 5;
    x += 1;
    println!("x: {}, y: {}", x, y);

    // lambda/combinator
    let fib_nums = |n: u32| (0..=n).map(fib).collect::<Vec<u32>>();
    println!("fib nums: {:?}", fib_nums(10));
}

should do some functional programming in python as well
