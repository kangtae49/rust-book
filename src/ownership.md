## `i32`
```rust
let n1 = 32;  // stack memory
let n2 = n1;  // `copy`
println!("[{:p}] {}", &n1, n1);
println!("[{:p}] {}", &n2, n2);
```

| Stack | `i32` |
| ----- | ----- |
| `0x7ffc25bebdd0` | 32 |
| `0x7ffc25bebdd4` | 32 |

## `String`
```rust
let s1 = String::from("rust");  // heap memory
println!("[{:p}] ({:p}) {}", &s1, s1.as_ptr(), s1);
let s2 = s1;  // `move`
println!("[{:p}] ({:p}) {}", &s2, s2.as_ptr(), s2);
```

| Stack | Heap | `String` |
| ----- | ---- | ----- |
| 0x7ffc6affaba8 | `0x5f0bfcfd5b10` | rust |
| 0x7ffc6affac60 | `0x5f0bfcfd5b10` | rust |

## `&str`
```rust
let s1 = "rust";  // static memory
let s2 = s1;  // `borrowing`
println!("[{:p}] [{:p}] {}", &s1, s1.as_ptr(), s1);
println!("[{:p}] [{:p}] {}", &s2, s2.as_ptr(), s2);
```

| Stack | Static | `&str` |
| ----- | ------ | ----- |
| 0xa3026ff8f8 | `0x7ff6a9c6a370` | rust |
| 0xa3026ff908 | `0x7ff6a9c6a370` | rust |

## `Option<i32>`

```rust
let opt1 = Some(32);  // stack memory
let opt2 = opt1;  // `copy`

if let Some(ref n1) = opt1 {
    println!("[{:p}] [{:p}] {:?}", &opt1, &n1, n1);
}

if let Some(ref n2) = opt2 {
    println!("[{:p}] [{:p}] {:?}", &opt2, &n2, n2);
}
```

| Stack | Stack | `Option<i32>` |
| ----- | ---- | ----------- |
| 0x7ffcbc581d78 | `0x7ffcbc581d88` | 32 |
| 0x7ffcbc581d80 | `0x7ffcbc581e30` | 32 |

## `Option<String>`

```rust
let opt1 = Some(String::from("rust"));  // heap memory

if let Some(ref s1) = opt1 {
    println!("[{:p}] ({:p}) {}", &opt1, s1.as_ptr(), s1);
}

let opt2 = opt1;  // `move`

if let Some(ref s2) = opt2 {
    println!("[{:p}] ({:p}) {}", &opt2, s2.as_ptr(), s2);
}
```

| Stack | Heap | `Option<String>` |
| ----- | ---- | ----------- |
| 0x7ffff0a60368 | `0x606459232b10` | rust |
| 0x7ffff0a60440 | `0x606459232b10` | rust |

## Option<&str>
```rust
let opt1 = Some("rust");  // static memory
let opt2 = opt1;  // `borrow`

if let Some(s1) = opt1 {
    println!("[{:p}] [{:p}] {:?}", &opt1, s1.as_ptr(), s1);
}


if let Some(s2) = opt2 {
    println!("[{:p}] [{:p}] {:?}", &opt2, s2.as_ptr(), s2);
}
```

| Stack | Static | `Option<&str>` |
| ----- | ---- | ----------- |
| 0x7ffe24342648 | `0x5fdb0f182040` | rust |
| 0x7ffe24342708 | `0x5fdb0f182040` | rust |

## Copy trait
> `#derive(Copy)`

```rust
#[derive(Debug)]
struct Foo;

let x = Foo;
let y = x;  // move

println!("{:?}", x);  // ❌error
```

```rust
#[derive(Debug, Copy, Clone)]
struct Foo;

let x = Foo;
let y = x;  // copy

println!("{:?}", x);
```

```rust
#[derive(Debug)]
struct Point {
    x: i32,
    y: i32,
}

let x = Point { x: 1, y: 2 };
let y = x;  // move
println!("{:?}", x);  // ❌error
```

```rust
#[derive(Debug, Copy, Clone)]
struct Point {
    x: i32,
    y: i32,
}

let x = Point { x: 1, y: 2 };
let y = x;  // copy
println!("{:?}", x);
```

```rust
#[derive(Debug, Copy, Clone)]  // ❌error derive(Copy)
struct Person {
    name: String,
    age: i32,
}
```
> `String does not implement the Copy trait`.


## Dangling References [^1]

```rust
fn main() {
    let s = hello();
    println!("{}", s);
}

fn hello() -> &String {
    let s = String::from("hello");

    &s  // ❌ dangling reference
}
```

```rust
fn main() {
    let s = hello();
    println!("{}", s);
}

fn hello() -> &'static str {
    "hello"
}
```

```rust
fn main() {
    let s = hello();
    println!("{}", s);
}

fn hello() -> String {
    let s = String::from("hello");

    s  // `move`
}
```

## Lifetimes Elision 
- Every reference in Rust has a lifetime. [^3]
- The borrow checker will allow you to omit them to save typing and to improve readability. [^2]
```rust
fn my_input(x: &i32) {
    println!("`elided_input`: {}", x);
}
```

```rust
fn my_input<'a>(x: &'a i32) {
    println!("`annotated_input`: {}", x);
}
```

```rust
fn longest(x: &str, y: &str) -> &str {
    x
}
```

```rust
fn longest<'a>(x: &'a str, y: &str) -> &'a str {
    x
}
```

## The Rules of References
- At any given time, you can have either `one mutable reference(&mut)` or `any number of immutable references(&)`.[^4]
```rust
    let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;  // error

    println!("{}, {}", r1, r2);
```

```rust
    let mut s = String::from("hello");

    {
        let r1 = &mut s;
    }

    let r2 = &mut s;
```

```rust
    let mut s = String::from("hello");

    let r1 = &s;
    let r2 = &s;
    let r3 = &mut s;

    println!("{}, {}, and {}", r1, r2, r3);
```

```rust
    let mut s = String::from("hello");

    let r1 = &s;
    let r2 = &s;

    println!("{}", r1);
    let r3 = &mut s;

    println!("{} {}", r2, r3);
```

```rust
    let mut s = String::from("hello");

    let r1 = &s;
    let r2 = &s;

    println!("{} {}", r1, r2);
    let r3 = &mut s;

    println!("{}", r3);
```

## self, &self, &mut self

``` rust,,noplayground
    fn into_iter(self) -> Self::IntoIter {}  // move
    fn iter(&self) -> Iter<'_, T> {}
    fn iter_mut(&mut self) -> IterMut<'_, T>
```

```rust
fn main() {
    let mut v1 = vec![1,2,3];
    let v2: Vec<_>  = v1.iter_mut()  // mutable borrow
        .map(|x|{
            let n = v1.len();  // second borrow
            *x *= n; 
            x.to_string()
        }).collect();
    println!("{:?}", v1);
    println!("{:?}", v2);
}
```

```rust
fn main() {
    let mut v1 = vec![1,2,3];
    let n = v1.len();
    let v2: Vec<_>  = v1.iter_mut()  // mutable borrow
        .map(|x|{
            *x *= n; 
            x.to_string()
        }).collect();
    println!("{:?}", v1);
    println!("{:?}", v2);
}
```

[^1]: <https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#references-and-borrowing>
[^2]: <https://doc.rust-lang.org/rust-by-example/scope/lifetime/elision.html>
[^3]: <https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html>
[^4]: <https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#the-rules-of-references>

