- Rust doesn’t have exceptions. [^1]
- Instead, it has the type `Result<T, E>` for `recoverable errors` and the panic! macro that stops execution when the program encounters an `unrecoverable error`. 

```rust
use std::fs::File;

fn main() { 
    let result = File::open("example.txt"); 

    match result { 
        Ok(_file) => println!("Ok"), 
        Err(error) => println!("Error: {:?}", error), 
    } 
}
```


```rust
    let v = vec![1, 2, 3];
    v[99];  // ❌panic!
```

```rust,editable
fn main () {
    let v = vec![1, 2, 3];
    let n = match v.get(99) {
        Some(n) => {
            *n
        }
        None => {
            v[0] // recoverable errors
        }
        // None => {
        //    panic!("stops execution") // unrecoverable errors
        // }
    };
    println!("{}", n);
}
```

```rust
println!("{:?}", "10".parse::<i32>());  
// Ok(10)
```

```rust
println!("{:?}", "err".parse::<i32>());  
// Err
```

```rust
println!("{:?}", "err".parse::<i32>().unwrap());  
// panic!
```

```rust
println!("{:?}", "err".parse::<i32>().unwrap_or(0));  
// 0
```

```rust
println!("{:?}", "err".parse::<i32>().ok());  
// Result -> Option
```

```rust
println!("{:?}", "10".parse::<i32>().map(|x| x*2));  
// Ok(20)
```

```rust
println!("{:?}", "err".parse::<i32>().map(|x| x*2));  
// Err
// map(|x| x/n) is not executed.
```

```rust
let n = 0;
println!("{:?}", "10".parse::<i32>().map(|x| x/n));  
// panic!
```

```rust
let n = 0;
println!("{:?}", "err".parse::<i32>().map(|x| x/n));  
// Err
// map(|x| x/n) is not executed.
```

```rust
println!("{:?}", "10".parse::<i32>().and_then(|x| Ok(x*2)));  
// Ok(20)
```

```rust
println!("{:?}", "err".parse::<i32>().and_then(|x| Ok(x*2)));  
// Err
// and_then(|x| Ok(x*2)) is not executed.
```

[^1]: https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html