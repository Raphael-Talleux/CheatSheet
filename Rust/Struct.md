# **Rust Structures Cheat Sheet**

### **Defining a Struct**

A struct is defined using the `struct` keyword. Here's an example:

```rust
struct Person {
    name: String,
    age: u32,
}
```

* `Person` is the name of the struct.
* `name` and `age` are fields with their respective types: `String` and `u32`.

---

### **Instantiating a Struct**

To create an instance of a struct, you assign values to each field:

```rust
let person1 = Person {
    name: String::from("Alice"),
    age: 30,
};
```

---

### **Accessing Struct Fields**

You can access fields in a struct using dot notation:

```rust
println!("Name: {}", person1.name);
println!("Age: {}", person1.age);
```

---

### **Modifying Struct Fields**

If the struct instance is mutable, you can modify its fields using dot notation:

```rust
let mut user1 = User {
    active: true,
    username: String::from("someusername123"),
    email: String::from("someone@example.com"),
    sign_in_count: 1,
};

// Modify the email field
user1.email = String::from("anotheremail@example.com");
```

* **Important**: The entire struct instance must be mutable (`mut`) to change any of its fields. Rust doesn’t allow marking individual fields as mutable.

---

### **Tuple Structs**

Tuple structs don’t have named fields. You access their values by position.

```rust
struct Point(i32, i32);

let point = Point(10, 20);
println!("X: {}, Y: {}", point.0, point.1);
```

---

### **Structs with Methods**

You can define methods for structs using the `impl` block. These methods allow you to operate on struct data.

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // Method to calculate area
    fn area(&self) -> u32 {
        self.width * self.height
    }

    // Method to create a new instance of Rectangle
    fn new(width: u32, height: u32) -> Rectangle {
        Rectangle { width, height }
    }
}

let rect = Rectangle::new(10, 5);
println!("Area: {}", rect.area());
```

---

### **Field Init Shorthand**

If the struct field names and the function parameter names are the same, you can use the **field init shorthand** syntax to avoid repeating the field names:

```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username, // shorthand for username: username
        email,    // shorthand for email: email
        sign_in_count: 1,
    }
}
```

* If the function parameters have the same names as the struct fields, Rust allows you to skip repeating the field names in the initialization.

---

### **Creating Instances with Struct Update Syntax**

You can create a new struct instance by copying most of the values from another instance of the same type, while changing some specific fields. This is done using **struct update syntax**:

```rust
let user2 = User {
    active: user1.active,
    username: user1.username,
    email: String::from("another@example.com"),  // changed field
    sign_in_count: user1.sign_in_count,
};
```
Or:
```rust
let person2 = Person {
    name: String::from("Bob"),
    ..person1 // copies remaining fields from `person1`
};
```

* This is useful when you want to create a new instance with most of the same data but with a few modifications.
* It’s more concise than specifying each field individually.

---

### **Unit-Like Structs**

Unit-like structs don’t have any fields. They’re useful when you just want to define a type without storing data.

```rust
struct Unit;

let unit = Unit;
```

---

### **Using `Option<T>` with Structs**

You can use `Option<T>` to represent a field that may be missing (`None`) or present (`Some`).

```rust
struct Person {
    name: String,
    age: Option<u32>, // Age might not be available
}

let person = Person {
    name: String::from("Charlie"),
    age: Some(22),
};
```

* `Option<T>` is a powerful enum to deal with potentially missing values safely.

---

### **Destructuring Structs**

Rust allows destructuring to extract values from structs directly:

```rust
let person = Person {
    name: String::from("Alice"),
    age: 30,
};

let Person { name, age } = person;
println!("Name: {}, Age: {}", name, age);
```

---


### **Visibility of Struct Fields**

By default, struct fields are private to the module. You can make them public using the `pub` keyword.

```rust
pub struct Car {
    pub make: String,
    pub model: String,
    year: u32, // this field is still private
}
```


---

### **`#[derive]` Attribute**

Rust allows you to automatically implement common traits for your structs using the `#[derive]` attribute.

```rust
#[derive(Debug, Clone, PartialEq)]
struct Car {
    make: String,
    model: String,
    year: u32,
}

let car1 = Car {
    make: String::from("Toyota"),
    model: String::from("Corolla"),
    year: 2020,
};

println!("{:?}", car1);  // Using the `Debug` trait to print
```

* `#[derive(Debug)]` auto-implements the `Debug` trait for easy printing.
* `#[derive(Clone)]` enables cloning of the struct.
* `#[derive(PartialEq)]` allows comparison with `==`.
