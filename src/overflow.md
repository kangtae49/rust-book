## Integer Overflow [^1]
- When you’re compiling in `debug mode`, Rust includes checks for integer overflow that cause your program to `panic` at runtime if this behavior occurs.
- When you’re compiling in release mode with the `--release` flag, Rust does not include checks for integer overflow that cause panics. In the case of a u8, the value 256 becomes 0, the value 257 becomes 1, and so on. 

```rust
    let mut n:u8 = 255;
    println!("{}", n);
    n += 1;
    println!("{}", n);
```
```shell
$ cargo build --release
$ target/release/???.exe
255
0
```

- To explicitly handle the possibility of overflow
```rust
    println!("wrapping_add   : {:?}", 255u8.wrapping_add(1));
    println!("checked_add    : {:?}", 255u8.checked_add(1));
    println!("overflowing_add: {:?}", 255u8.overflowing_add(1));
    println!("saturating_add : {:?}", 255u8.saturating_add(1));
    println!("");
    println!("wrapping_add   : {:?}", 0u8.wrapping_add(1));
    println!("checked_add    : {:?}", 0u8.checked_add(1));
    println!("overflowing_add: {:?}", 0u8.overflowing_add(1));
    println!("saturating_add : {:?}", 0u8.saturating_add(1));
```

```rust
    println!("wrapping_add   : {:?}", 127i8.wrapping_add(1));
    println!("checked_add    : {:?}", 127i8.checked_add(1));
    println!("overflowing_add: {:?}", 127i8.overflowing_add(1));
    println!("saturating_add : {:?}", 127i8.saturating_add(1));
    println!("");
    println!("wrapping_add   : {:?}", 0i8.wrapping_add(1));
    println!("checked_add    : {:?}", 0i8.checked_add(1));
    println!("overflowing_add: {:?}", 0i8.overflowing_add(1));
    println!("saturating_add : {:?}", 0i8.saturating_add(1));
```
[^1]: <https://doc.rust-lang.org/book/ch03-02-data-types.html#integer-overflow>