---
title: "Rust: For-Loop over Iterators"
date: 2020-09-13T11:16:41+02:00
draft: true
toc: false
images:
tags:
  - untagged
---
## Table of Content:

- [Introduction](#introduction)
- [For-Loops in Other Languages](#other-languages)

## Introduction {#introduction}

One of the most essential feature of any programming language is its `for loop`. As a programmer, we use `for loops` almost on a daily basis. However, a beginner in Rust might be confused by the variety of ways one could loop. Besides the [infinite loop keyword](https://doc.rust-lang.org/stable/rust-by-example/flow_control/loop.html) and the common [while-loop](https://doc.rust-lang.org/1.2.0/book/while-loops.html), Rust comes with 3 options for you to do a `for-loop` on : [`into_iter`](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter), [`iter`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.iter) and [`iter_mut`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.iter_mut).

All three approaches use the `for in` construct to convert a `collection` into an `Iterator` for looping purposes. However, they convert `collections` into `iterators` in slightly different ways.

## For-Loops & For-Ranges in Other Languages {#other-languages}
While it is not necessary, it helps to compare Rust's approach to for-loops with some other popular languages, such as Python, Javascript and Go.

In **Python**, a for-loop or a for-range is as simple as the following, human-readable example. More complicated loops, such as looping over a `list` with index as well, requires built-in functions such as [`enumerate`](https://book.pythontips.com/en/latest/enumerate.html).
```python
# PYTHON EXAMPLES
arr = [1, 2, 3]
for item in arr:
  print(item)
# Output: 1, 2, 3 on new lines

for item in range(0, 4):
  print(item)
# Output: 1, 2, 3 on new lines
```

**Javascript**, similarly, has several approaches, including `for...in`, `for...of`, or an object's prototype method `forEach` (examples are modified from [StackOverflow](https://stackoverflow.com/questions/29285897/what-is-the-difference-between-for-in-and-for-of-statements-in-jav)):
```javascript
// JAVASCRIPT EXAMPLES
var arr = [1, 2, 3];
arr.foo = "bar"; // => [1, 2, 3, foo: "bar"]

for (var i in arr) {
  console.log(i); // Output indices/keys: "0", "1", "2", "foo"
}

for (var i of arr) {
  console.log(i); // Output: "1", "2", "3"
}

arr.forEach( (i) => console.log(i) ) // Output: "1", "2", "3"
```

In contrast, the lightweight and simple **Go** has a very convenient for-range construct for handling looping over arrays and maps, besides the classic C-like for loop:
```go
// GO EXAMPLES
arr := []int{1, 2, 3}
for _, v := range arr {
  fmt.Println(v)
}

for i := 0; i < len(arr); i++ {
    fmt.Printf("%d", arr[i])
}
```

## Rust's For...In and into_iter 
Very similar to Javascript's syntax, we can use `for...in` to loop over a [`vector`](https://doc.rust-lang.org/std/vec/struct.Vec.html) in **Rust**. In the following example, suppose we want to find out what the largest number in the vector `number_list` is, we could assign the first number in the vector as the `largest`, loop over the vector and compare each subsequent number with `largest`, reassigning `largest` to the next number if it is larger than the previous one: 

```rust
let number_list = vec![34, 50, 25, 100, 65];

let mut largest = number_list[0];

for item in number_list {
    if item > largest {
        largest = item;
    }
}

println!("largest is {}", largest);
// Run the following line results in compiler error
println!("{:?}", number_list);
```

Everything should work fine. But if for some reason you'd want to re-examine the vector `number_list` again by running the `println!` macro, your Rust compiler will throw you an error:
```
    |
2   |     let number_list = vec![34, 50, 25, 100, 65];
    |         ----------- move occurs because `number_list` has type `std::vec::Vec<i32>`, which does not implement the `Copy` trait
...
6   |     for item in number_list {
    |                 -----------
    |                 |
    |                 `number_list` moved due to this implicit call to `.into_iter()`
    |                 help: consider borrowing to avoid moving into the for loop: `&number_list`
...
14  |     println!("{:?}", number_list); 
    |                      ^^^^^^^^^^^ value borrowed here after move
    |
note: this function consumes the receiver `self` by taking ownership of it, which moves `number_list`
```
Behind the scene, we are [converting the vector](https://doc.rust-lang.org/std/iter/index.html#for-loops-and-intoiterator) into an [`IntoIterator`](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html).

In the official documentation, it is stated that there are [three common methods](https://doc.rust-lang.org/std/iter/index.html#the-three-forms-of-iteration) which can create iterators from a collection:

iter(), which iterates over &T.
iter_mut(), which iterates over &mut T.
into_iter(), which iterates over T.

It's literally the same as:

```rust
fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let mut largest = number_list[0];
    
    for item in number_list.into_iter() {
        if item > largest {
            largest = item;
        }
    }
    
    println!("largest is {}", largest);
    // If for some reason you want to examine the original vec, Rust panicks
    // println!("{:?}", number_list); 
}
```


## Safe for-loop

```rust
// Iterator over the 
fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let mut largest = number_list[0];
    
    for &item in number_list.iter() {
        if item > largest {
            largest = item;
        }
    }
    
    println!("largest is {}", largest);
    println!("{:?}", number_list);
}
```


## Finally, iter_mut {#bottom}

```rust
fn main() {
    let mut number_list = vec![34, 50, 25, 100, 65];

    let mut largest = number_list[0];
    
    for &mut item in number_list.iter_mut() {
        if item > largest {
            largest = item;
        }
    }
    
    println!("largest is {}", largest);
    // If for some reason you want to examine the original vec, Rust panicks
    println!("{:?}", number_list); 
}
```

Or the following works, too:
```rust
fn main() {
    let mut number_list = vec![34, 50, 25, 100, 65];

    let mut largest = number_list[0];
    
    for item in number_list.iter_mut() {
        if *item > largest {
            largest = *item;
        }
    }
    
    println!("largest is {}", largest);
    // If for some reason you want to examine the original vec, Rust panicks
    println!("{:?}", number_list); 
}
```

The difference between these lines lie in Rust's reference pattern: https://doc.rust-lang.org/reference/patterns.html#reference-patterns.



## [What is deref?](#deref)

For the other problems, you can dig a little bit more into the documentation

Deref trait will be an intuitive concept once you learn about it, deref-ing struct lets you access the "inner" value of the struct which means you can also access its method.

You can manually deref struct by prefixing the variable with * like so

```rust
let foo = Foo::new(); // Let's assume that `Foo` implement Deref<Target = Bar>
let bar = *foo; // This can be desugar into `*foo.deref()`
// Which if we look at the trait definition will return `&Self::Target` or `&Bar`
```

And you can also use . separator which will try to deref the type first and then access the method/field.

```rust
let foo = Foo::new(); // Let's assume that `Foo` implement Deref<Target = Bar>
let result = foo.method_from_bar(); // Will first de-sugar into (*foo).method_from_bar()
// (*foo) will then be resolved to `Bar` which will call the method_from_bar() and return the result.
```

You can also just think of it as "inheriting" method from Target type if you think that's easier to understand.