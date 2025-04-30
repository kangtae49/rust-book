## Box
- The Box<T> type for heap allocation.[^1]

## Rc
- The type Rc<T> provides shared ownership of a value of type T, allocated in the heap.[^2]
```rust
    let apple = String::from("apple");
    let banana = String::from("banana");

    let v1 = vec![apple, banana];  // move
    let v2 = vec![banana];  // error

    println!("{:?} {:?}", v1, v2);
```

```rust
    let apple = Rc::new(String::from("apple"));
    let banana = Rc::new(String::from("banana"));
    
    let v1 = vec![apple.clone(), banana.clone()];  // move
    let v2 = vec![banana.clone()];  // move
    
    println!("{:?} {:?}", v1, v2);
```

```text
    list1 = A -> B -> C -> D
    list2 = tail(list1) = B -> C -> D
    list3 = push(list2, X) = X -> B -> C -> D
```
- This just can't work with Boxes, because ownership of B is shared.[^3]
- Who should free it? If I drop list2, does it free B? 

```text
    list1 -> A ---+
                  |
                  v
    list2 ------> B -> C -> D
                  ^
                  |
    list3 -> X ---+
```


## Arc

## RefCell

## 

[^1]: <https://doc.rust-lang.org/std/boxed/index.html>
[^2]: <https://doc.rust-lang.org/std/rc/index.html>
[^3]: <https://rust-unofficial.github.io/too-many-lists/third-layout.html>

