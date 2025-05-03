## Auto Deref [^1]
```rust
    let s1 = String::from("10");
    println!("{:?}", s1.parse::<i32>());

    let s2 = Box::new(String::from("10"));
    println!("{:?}", s2.parse::<i32>());
```


[^1]: <https://doc.rust-lang.org/stable/reference/expressions/field-expr.html?highlight=deref#automatic-dereferencing>
[^2]: <https://doc.rust-lang.org/book/ch15-02-deref.html>