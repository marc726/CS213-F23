
### Basics of Constructors

a. True or False: A constructor creates an object.

b. Fill in the blanks: In the statement `new X()`, `new X` ________ and `X()` ________.

c. True or False: When an object is created with `new`, its fields are initialized to their intrinsic default values before the constructor is called.

d. Given the class definition `public class Point { }`, will it compile? Explain why.

e. If a class has no constructor defined, what type of constructor is provided by the compiler by default?

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

b. Explain the difference between a no-arg constructor and a default constructor.

### **Multiple Constructors and `this()`:**

a. Given the Point class:
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

### Advanced

a. How can you ensure that a class can't be instantiated (i.e., objects can't be created from it)?

b. Explain the purpose and usage of the `this()` call inside a constructor. Why would a programmer use it?