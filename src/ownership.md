## `i32`
```rust
let n1 = 32;  // stack memory
let n2 = n1;  // `copy`
println!("[{:p}] {}", &n1, n1);
println!("[{:p}] {}", &n2, n2);
```
| var | addr               | `i32`       |
| --- | ------------------ | ----------- |
| n1  | 0x0000004995affb50 | 20 00 00 00 |
| n2  | 0x0000004995affb54 | 20 00 00 00 |

## `&str`
```rust
let s1 = "rust";  // static memory
let s2 = s1;  // `borrowing`
println!("[{:p}] [{:p}] {} {}", &s1, s1.as_ptr(), s1.len(), s1);
println!("[{:p}] [{:p}] {} {}", &s2, s2.as_ptr(), s1.len(), s2);
```
| var | addr                 | `&str`                    |      |
| --- | -------------------  | ------------------------- |----- |
| s1  | 0x0000005dc016f798   | 80 a3 4e e1   f6 7f 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x00007ff6e14ea380` | 72 75 73 74               | val  |
| s2  | 0x0000005dc016f7a8   | 80 a3 4e e1   f6 7f 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x00007ff6e14ea380` | 72 75 73 74               | rust |


## `String`
```rust
let s1 = String::from("rust");  // heap memory
println!("[{:p}] ({:p}) {}", &s1, s1.as_ptr(), s1);
let s2 = s1;  // `move`
println!("[{:p}] ({:p}) {}", &s2, s2.as_ptr(), s2);
```
| var | addr                 | `String`                  |      |
| --- | -------------------- | ------------------------- | ---- |
| s1  | 0x000000f0baaff648   | 04 00 00 00   00 00 00 00 |      |
|     |                      | 50 58 a9 c6   af 02 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x000002afc6a95850` | 72 75 73 74               | rust |
| s2  | 0x000000f0baaff700   | 04 00 00 00   00 00 00 00 |      |
|     |                      | 50 58 a9 c6   af 02 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x000002afc6a95850` | 72 75 73 74               | rust |



## `Option<i32>`

```rust
    let n1 = Some(32);  // stack memory
    let n2 = n1;  // `copy`
    if let Some(x) = n1 {
        println!("[{:p}] [{:p}] {}", &n1, &x, x);
    }
    if let Some(x) = n2 {
        println!("[{:p}] [{:p}] {}", &n2, &x, x);
    }
```
 
| var | addr                 | `Option<i32>`             |        |
| --- | -------------------- | ------------------------- | ------ |
| n1  | 0x000000a587bbf328   | 01 00 00 00   20 00 00 00 | len 32 |
| n2  | 0x000000a587bbf330   | 01 00 00 00   20 00 00 00 | len 32 |

## Option<&str>
```rust
    let s1 = Some("rust");  // static memory
    let s2 = s1;  // `borrowing`

    if let Some(x) = s1 {
        println!("[{:p}] [{:p}] {}", &s1, x.as_ptr(), x);
    }

    if let Some(x) = s2 {
        println!("[{:p}] [{:p}] {}", &s2, x.as_ptr(), x);
    }
```
| var | addr                 | `&str`          |      |
| --- | -------------------- | ------------------------- | ---- |
| s1  | 0x000000f8488ff7c8   | 80 a3 70 27   f7 7f 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x00007ff72770a380` | 72 75 73 74               | rust |
| s2  | 0x000000f8488ff888   | 80 a3 70 27   f7 7f 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x00007ff72770a380` | 72 75 73 74               | rust |

## `Option<String>`

```rust
    let s1 = Some(String::from("rust"));  // heap memory

    if let Some(ref x) = s1 {
        println!("[{:p}] [{:p}] {}", &s1, x.as_ptr(), x);
    }

    let s2 = s1;  // `move`

    if let Some(ref x) = s2 {
        println!("[{:p}] [{:p}] {}", &s2, x.as_ptr(), x);
    }
```

| var | addr                 | `Option<String>`          |      |
| --- | -------------------- | ------------------------- | ---- |
| s1  | 0x00000069acf6f768   | 04 00 00 00   00 00 00 00 |      |
|     |                      | 80 79 dd f4   8a 01 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x0000018af4dd7980` | 72 75 73 74               | rust |
| s2  | 0x00000069acf6f840   | 04 00 00 00   00 00 00 00 |      |
|     |                      | 80 79 dd f4   8a 01 00 00 | ptr  |
|     |                      | 04 00 00 00   00 00 00 00 | len  |
|     | `0x0000018af4dd7980` | 72 75 73 74               | rust |



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

