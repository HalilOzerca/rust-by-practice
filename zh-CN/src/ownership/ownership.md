# æææ

1. ðð
```rust,editable

fn main() {
    // ä½¿ç¨å°½å¯è½å¤çæ¹æ³æ¥éè¿ç¼è¯
    let x = String::from("hello, world");
    let y = x;
    println!("{},{}",x,y);
}
```

2. ðð
```rust,editable
// ä¸è¦ä¿®æ¹ main ä¸­çä»£ç 
fn main() {
    let s1 = String::from("hello, world");
    let s2 = take_ownership(s1);

    println!("{}", s2);
}

// åªè½ä¿®æ¹ä¸é¢çä»£ç !
fn take_ownership(s: String) {
    println!("{}", s);
}
```


3. ðð
```rust,editable

fn main() {
    let s = give_ownership();
    println!("{}", s);
}

// åªè½ä¿®æ¹ä¸é¢çä»£ç !
fn give_ownership() -> String {
    let s = String::from("hello, world");
    // convert String to Vec
    // å° String è½¬æ¢æ Vec ç±»å
    let _s = s.into_bytes();
    s
}
```

4. ðð
```rust,editable
// ä¿®å¤éè¯¯ï¼ä¸è¦å é¤ä»»ä½ä»£ç è¡
fn main() {
    let s = String::from("hello, world");

    print_str(s);

    println!("{}", s);
}

fn print_str(s: String)  {
    println!("{}",s)
}
```

5. ðð 
```rust, editable
// ä¸è¦ä½¿ç¨ cloneï¼ä½¿ç¨ copy çæ¹å¼æ¿ä»£
fn main() {
    let x = (1, 2, (), "hello".to_string());
    let y = x.clone();
    println!("{:?}, {:?}", x, y);
}
```

#### å¯åæ§
å½æææè½¬ç§»æ¶ï¼å¯åæ§ä¹å¯ä»¥éä¹æ¹åã

6. ð
```rust,editable

fn main() {
    let s = String::from("hello, ");
    
    // åªä¿®æ¹ä¸é¢è¿è¡ä»£ç  !
    let s1 = s;

    s1.push_str("world")
}
```

7. ððð
```rust,editable

fn main() {
    let x = Box::new(5);
    
    let ...      // å®æè¯¥è¡ä»£ç ï¼ä¸è¦ä¿®æ¹å¶å®è¡ï¼
    
    *y = 4;
    
    assert_eq!(*x, 5);
}
```

### é¨å move
å½è§£æä¸ä¸ªåéæ¶ï¼å¯ä»¥åæ¶ä½¿ç¨ `move` åå¼ç¨æ¨¡å¼ç»å®çæ¹å¼ãå½è¿ä¹åæ¶ï¼é¨å `move` å°±ä¼åçï¼åéä¸­ä¸é¨åçæææè¢«è½¬ç§»ç»å¶å®åéï¼èå¦ä¸é¨åæä»¬è·åäºå®çå¼ç¨ã

å¨è¿ç§æåµä¸ï¼ååéå°æ æ³åè¢«ä½¿ç¨ï¼ä½æ¯å®æ²¡æè½¬ç§»æææçé£ä¸é¨åä¾ç¶å¯ä»¥ä½¿ç¨ï¼ä¹å°±æ¯ä¹åè¢«å¼ç¨çé£é¨åã

#### ç¤ºä¾
```rust,editable

fn main() {
    #[derive(Debug)]
    struct Person {
        name: String,
        age: Box<u8>,
    }

    let person = Person {
        name: String::from("Alice"),
        age: Box::new(20),
    };

    // éè¿è¿ç§è§£æå¼æ¨¡å¼å¹éï¼person.name çæææè¢«è½¬ç§»ç»æ°çåé `name`
    // ä½æ¯ï¼è¿é `age` åéå´æ¯å¯¹ person.age çå¼ç¨, è¿é ref çä½¿ç¨ç¸å½äº: let age = &person.age 
    let Person { name, ref age } = person;

    println!("The person's age is {}", age);

    println!("The person's name is {}", name);

    // Error! åå æ¯ person çä¸é¨åå·²ç»è¢«è½¬ç§»äºæææï¼å æ­¤æä»¬æ æ³åä½¿ç¨å®
    //println!("The person struct is {:?}", person);

    // è½ç¶ `person` ä½ä¸ºä¸ä¸ªæ´ä½æ æ³åè¢«ä½¿ç¨ï¼ä½æ¯ `person.age` ä¾ç¶å¯ä»¥ä½¿ç¨
    println!("The person's age from person struct is {}", person.age);
}
```

#### ç»ä¹ 

8. ð
```rust,editable

fn main() {
   let t = (String::from("hello"), String::from("world"));

   let _s = t.0;

   // ä»ä¿®æ¹ä¸é¢è¿è¡ä»£ç ï¼ä¸ä¸è¦ä½¿ç¨ `_s`
   println!("{:?}", t);
}
```

9. ðð
```rust,editable

fn main() {
   let t = (String::from("hello"), String::from("world"));

   // å¡«ç©ºï¼ä¸è¦ä¿®æ¹å¶å®ä»£ç 
   let (__, __) = __;

   println!("{:?}, {:?}, {:?}", s1, s2, t); // -> "hello", "world", ("hello", "world")
}
```

> ä½ å¯ä»¥å¨[è¿é](https://github.com/sunface/rust-by-practice/blob/master/solutions/ownership/ownership.md)æ¾å°ç­æ¡(å¨ solutions è·¯å¾ä¸) 
