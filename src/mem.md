## std::mem:swap
- Swaps the values at two mutable locations, without deinitializing either one.
```rust
    use std::mem;

    let mut a = 1;
    let mut b = 2;

    println!("{} {}", a, b);
    mem::swap(&mut a, &mut b);
    println!("{} {}", a, b);

```
## std::mem::replace
- `Neither value is dropped.`
```rust
    use std::mem;

    let mut v: Vec<i32> = vec![1, 2];

    let old_v = mem::replace(&mut v, vec![3, 4, 5]);

    println!("{:?}", v);
    println!("{:?}", old_v);
```

## std::mem::take
- Replaces dest with the `default value of T`, returning the previous dest value.
```rust
    use std::mem;
    
    let mut v: Vec<i32> = vec![1, 2];
    
    let old_v = mem::take(&mut v);

    println!("{:?}", v);
    println!("{:?}", old_v);
```

