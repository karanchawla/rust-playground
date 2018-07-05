# Ownership
- Explicit ownership is the biggest feature rust brings to the table 
- Checked at compile time so little runtime impact
- A piece of data can have only one owner at a time
- Data must be guaranteed to live after its references or all references must be valid

### Move semantics
- Moving ownership is a compile time semantic; no data is moved or copied when the program is running

### Ownership 
- Ownership doesn't need to be moved. 

### Borrowing
- Instead of transferring ownership we can borrow data by using references
- When a reference goes out of scope the borrowing is over
- The original variable retains ownership throughout 
- Ownership cannot be transferred from a variable while references exist since that would invalidate the reference
- References like variables are immutable by default 
- Variable can be borrowed using mutable references like so: `&mut Vec<i32>`
- Rust auto dereferences variables for e.g: 
```
/// `length` only needs `vector` temporarily, so it is borrowed.
fn length(vec_ref: &&Vec<i32>) -> usize {
        // vec_ref is auto-dereferenced when you call methods on it.
            vec_ref.len()
}

fn main() {
        let vector = vec![];
            length(&&&&&&&&&&&&vector);
}
```
- Dereference variables when writing into them: 
```
let mut a = 5;
let ref_a = &mut a;
*ref_a = 4;
println!("{}", *ref_a + 4);
// ==> 8
```

### Referencing using `ref`
- These statements are equivalent
```
let mut vector = vec![];
let ref1 = &vector;
let ref ref2 = vector;
assert_eq!(ref1, ref2);
```

## Holy Grail — Borrowing Rules
- You cannot borrow something after it stops existing
- You can either have multiple immutable reference to the object
- OR exactly one mutable reference to it 
