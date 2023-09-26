
**1. Basic Constructor Usage**

Write a class named `Rectangle` with the following:

- Two private instance variables `length` and `width` of type `double`.
- A default constructor that initializes `length` and `width` to `1`.
- A parameterized constructor that initializes `length` and `width` to given values.
- A method `area()` that returns the area of the rectangle.
- A method `perimeter()` that returns the perimeter of the rectangle.

---

**2. Constructor Overloading**

Extend the `Rectangle` class from the first problem to include:

- Another constructor that takes a single parameter. If this constructor is used, it should initialize the rectangle to be a square with the given side length.
- Ensure that negative values for `length` and `width` are not allowed. If a negative value is provided, set the corresponding dimension to `1`.

---

**3. Copy Constructor**

For the `Rectangle` class:

- Implement a copy constructor that initializes a new rectangle object using another rectangle object as the source.
- Implement a method `isSame(Rectangle other)` that checks if the current rectangle has the same dimensions as the `other` rectangle.

---

**4. The `this` Keyword**

Design a class named `Circle` with:

- A private instance variable `radius` of type `double`.
- A default constructor that initializes `radius` to `1`.
- A constructor that takes the radius as a parameter.
- A constructor that takes another `Circle` object and initializes the new circle with the same radius (copy constructor).
- All constructors should use the `this` keyword appropriately.
- Methods to calculate and return the area and circumference of the circle.

---

**5. Constructor Chaining**

Create a class `Box` representing a three-dimensional box with:

- Three private instance variables `length`, `width`, and `height` of type `double`.
- A default constructor that initializes all sides to `1`.
- A constructor that takes one parameter and initializes all sides to the provided value.
- A constructor that takes three parameters to initialize `length`, `width`, and `height` respectively.
- All constructors should call another constructor using `this`.
- Methods to calculate and return the volume and surface area of the box.

---

**6. Static Initialization Blocks**

Consider a class `DatabaseConnection`.

- The class has a private static variable `connectionString` of type `String`.
- The class contains a static initialization block that sets the `connectionString` to some default value.
- The class contains a public method `connect()` that simulates a connection using the `connectionString`.

Demonstrate the use of this class and the initialization of the `connectionString`.

---

**7. Instance Initialization Blocks**

Design a class named `Vehicle`:

- It has private instance variables: `make`, `model`, and a `List<String> features`.
- The class contains an instance initialization block that initializes `features` with a default set of features.
- Provide constructors to initialize `make` and `model`.
- Include a method to add a feature to the `features` list and another method to display all features.

---

**8. Reflection and Constructors**

Given a class named `Simple`, with a private instance variable `data` and appropriate constructors:

- Write a program that creates an instance of `Simple` using Java's Reflection API, without directly calling any of its constructors.

**Hint**: Look into the `Constructor` class from the `java.lang.reflect` package.