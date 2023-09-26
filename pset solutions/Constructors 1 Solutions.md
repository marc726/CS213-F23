
### Basics of Constructors

a. True or False: A constructor creates an object.
	False: A constructor initializes an object. The memory allocation and object creation is done by the `new` keyword.

b. Fill in the blanks: In the statement `new X()`, `new X` .... and `X()`....... .
	In the statement `new X()`, `new X` <u>creates an X object</u> and `X()` <u>calls the no-arg constructor of X on the new object, to initialize it.</u>

c. True or False: When an object is created with `new`, its fields are initialized to their intrinsic default values before the constructor is called.
	**True** - When an object is created with `new`, its fields are initialized to their intrinsic default values (like 0 for `int`, `null` for object references, etc.) before the constructor is called.

d. Given the class definition `public class Point { }`, will it compile? Explain why.
	**Yes**, it will compile. The Java compiler automatically provides a default no-arg constructor if no constructor is explicitly defined in the class.

e. If a class has no constructor defined, what type of constructor is provided by the compiler by default?
	A **default no-arg constructor** is provided by the compiler if no constructor is defined by the programmer.

### No-arg and Default Constructors

a. Given the following Point class:

```Java
public class Point {
    int x, y;
    public Point(int x, int y) {
        this.x = x; this.y = y;
    }
}
```

Will the statement `Point p = new Point();` compile? Why or why not?
##### Solution:
**No**, the statement `Point p = new Point();` will not compile. Given the definition of the Point class, there is no no-arg constructor available. The only constructor defined requires two integer arguments.


b. Explain the difference between a no-arg constructor and a default constructor.
##### Solution:
A **no-arg constructor** is a constructor that does not take any arguments. A **default constructor** is a no-arg constructor that is provided by the compiler when no other constructor is explicitly defined in the class.

### Multiple Constructors and `this()`:

a. For the code:

```Java
public class Point {
    int x, y;
    public Point(int x, int y) {
        this.x = x; this.y = y;
    }
    public Point(int x) {
        this(x, 0);
    }
    public Point() {
        this(0, 0);
    }
}
```

What will the following code initialize the variables `x` and `y` to?

``` Java
Point p1 = new Point(5); 
Point p2 = new Point();
```
##### Solution:
- `p1`: The constructor `public Point(int x)` is called. So, `x` will be initialized to `5` and `y` will be initialized to `0`.
- `p2`: The no-arg constructor `public Point()` is called, which in turn calls the two-arg constructor with `(0, 0)`. So, both `x` and `y` will be initialized to `0`.


b. In the class:

```Java
public class Point {
    public static final int X_MAX = 800, Y_MAX = 800;
    int x, y;
    public Point(int x, int y) {
        if (x < 0 || x > X_MAX || y < 0 || y > Y_MAX) {
            throw new IllegalArgumentException("invalid x or y");
        }
        this.x = x; this.y = y;
    }
    public Point(int x) {
        this(x, 0);
    }
    public Point(int y) {
        this(0, y);
    }
    public Point() {
        this(0, 0);
    }
}
```

If a point is created with `Point p = new Point(900, 400);`, what will happen? Explain.
##### Solution:
If a point is created with `Point p = new Point(900, 400);`, an `IllegalArgumentException` will be thrown with the message "invalid x or y". This is because the x-value provided (900) exceeds the `X_MAX` constant value of 800.

### Advanced

a. How can you ensure that a class can't be instantiated (i.e., objects can't be created from it)?
##### Solution:
To ensure that a class can't be instantiated, you can:

- Make its constructor private.
- If you want to provide more context, you can also throw an exception inside this private constructor.

```Java
public class NonInstantiableClass {
    private NonInstantiableClass() {
        throw new AssertionError("Cannot instantiate this class");
    }
}
```



b. Explain the purpose and usage of the `this()` call inside a constructor. Why would a programmer use it?
##### Solution:
The `this()` call inside a constructor is used to invoke another constructor within the same class. Programmers use it to reuse the code from one constructor in another, ensuring a single point of object initialization and reducing code duplication. It helps maintain a consistent initialization process and reduces potential errors.