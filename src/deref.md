## Deref
```rust
    let s1 = String::from("10");
    println!("{:?}", s1.parse::<i32>());

    let s2 = Box::new(String::from("10"));
    println!("{:?}", s2.parse::<i32>());
```

```rust
    let a = Some(1);
    let b = Some(2);
    let c = a + b;  // ❌error
```

```rust
    let a = Box::new(1);
    let b = Box::new(2);
    let c = *a + *b;
    println!("{}", c);
```

```rust
    let a = String::from("Hello");
    let b = Box::new(Box::new(a));
    println!("{}", b);
```

```rust
    let a = String::from("Hello");
    let b = Box::new(Box::new(a));

    let c = **b;  // String
    println!("{}", c);    
```

```rust
    let a = String::from("Hello");
    let b = Box::new(Box::new(a));

    let c: &String = &b;
    println!("{}", c);    
```

```rust
    let a = String::from("Hello");
    let b = Box::new(Box::new(a));

    let c: &str = &b;
    println!("{}", c);    
```

```rust
    let a = String::from("Hello");
    let b = &a;
    let c = *b;  // ❌ can not move
```

```rust
    let a = Box::new(String::from("Hello"));
    let b = *a;  // `move`
    println!("{}", b);
```

- <https://doc.rust-lang.org/stable/reference/expressions/field-expr.html?highlight=deref#automatic-dereferencing>
- <https://doc.rust-lang.org/book/ch15-02-deref.html>