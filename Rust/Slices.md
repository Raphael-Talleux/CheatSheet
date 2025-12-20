# Rust Slices Cheat Sheet

## What is a Slice?

A **slice** is a **borrowed view** of a contiguous sequence of elements in a collection (like an array or a `String`), without owning it.

---

## Types of Slices

1. **String Slice (`&str`)**

   * A view into a `String`.
   * Immutable by default.
   * Slices are often used to refer to parts of a string without copying the data.

   ```rust
   let s = String::from("hello");
   let slice = &s[0..2]; // "he"
   ```

2. **Array Slice (`&[T]`)**

   * A view into an array or vector.
   * You can slice arrays and vectors to get a sub-array.

   ```rust
   let arr = [1, 2, 3, 4, 5];
   let slice = &arr[1..4]; // [2, 3, 4]
   ```

---

## Slicing Syntax

### Slicing a String

```rust
let s = String::from("Hello, world!");
let slice = &s[0..5]; // "Hello"
```

* **`&s[0..5]`**: From index `0` to `5` (exclusive).
* **`&s[..5]`**: Same as `&s[0..5]`.
* **`&s[7..]`**: From index `7` to the end.
* **`&s[..]`**: Entire string slice (`&str`).

### Slicing an Array

```rust
let arr = [1, 2, 3, 4, 5];
let slice = &arr[1..3]; // [2, 3]
```

* **`&arr[1..3]`**: From index `1` to `3` (exclusive).
* **`&arr[..3]`**: From start to index `3` (exclusive).
* **`&arr[2..]`**: From index `2` to the end.
* **`&arr[..]`**: Entire array slice.

---

## Slice Length

You can check the length of a slice using the `.len()` method:

```rust
let arr = [1, 2, 3, 4, 5];
let slice = &arr[1..4];
println!("{}", slice.len()); // 3
```

---

## Slice Mutability

* **Immutable Slices**: You can't modify the underlying data through an immutable slice.

```rust
let s = String::from("Hello");
let slice = &s[0..3];
// slice[0] = 'h'; // Error: cannot modify a borrowed value
```

* **Mutable Slices**: You can modify the underlying data through a mutable slice.

```rust
let mut arr = [1, 2, 3, 4];
let slice = &mut arr[1..3];
slice[0] = 42;
println!("{:?}", arr); // [1, 42, 3, 4]
```

---

## Slicing a `Vec`

You can also slice a `Vec` (vector) in the same way as arrays.

```rust
let vec = vec![1, 2, 3, 4, 5];
let slice = &vec[2..4]; // [3, 4]
```

---

## Common Slice Methods

* **`split_at(mid: usize)`**: Splits a slice into two parts at the `mid` index.

  ```rust
  let arr = [1, 2, 3, 4, 5];
  let (left, right) = arr.split_at(2); 
  println!("{:?} {:?}", left, right); // [1, 2] [3, 4, 5]
  ```

* **`windows(size: usize)`**: Iterates over windows (sub-slices) of a given size.

  ```rust
  let arr = [1, 2, 3, 4, 5];
  for window in arr.windows(3) {
      println!("{:?}", window); // [1, 2, 3], [2, 3, 4], [3, 4, 5]
  }
  ```

---

## Performance Considerations

* **No Memory Allocation**: Slices do not allocate memory, they simply provide a reference to an existing collection.
* **Efficient**: Slicing does not involve copying the data. It's just a reference, so it's very efficient.
* **Read-Only by Default**: If you need to modify data, use a **mutable slice** (`&mut`).

---

## Borrowing Rules with Slices

* Slices are **borrowed** references to data, so they follow the same borrowing rules as regular references:

  * You can have **multiple immutable slices** at the same time.
  * You can have **only one mutable slice** at a time.

---

## Important Notes

1. **Slices do not own the data** they point to. You cannot use slices to modify the ownership of the underlying data.
2. You cannot create **dangling slices**: a slice cannot live longer than the data it references.

---

## Example: Slicing with Functions

```rust
fn print_slice(slice: &[i32]) {
    for &item in slice {
        println!("{}", item);
    }
}

let arr = [10, 20, 30, 40];
print_slice(&arr[1..3]); // 20, 30
```
