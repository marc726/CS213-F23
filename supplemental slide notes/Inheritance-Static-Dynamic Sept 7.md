
## **Inheritance, Superclass and Subclass**


**Superclass (Parent Class)**: `Point`
- Contains fields `x` and `y`.
```Java
public class Point {
    int x,y;
}
```

**Subclass (Child Class)**: `ColoredPoint`
- Inherits from `Point`.
- Thus, `ColoredPoint` automatically has the fields `x` and `y` from `Point`.
```Java
public class ColoredPoint extends Point {
}
```
Note: There's an emphasis on "CODE REUSE", indicating that by using inheritance, we avoid re-declaring fields and methods in subclasses that are already declared in the superclass.

---
#### **Inheritance and super/sub constructors**

**Point Class**:
- Contains fields `x` and `y`.
- Custom constructor defined to initialize `x` and `y`.
```Java
public class Point {
    int x,y;
    public Point(int x, int y) {
        this.x = x; 
        this.y = y;
    }
}
Point p = new Point(3,4); // p is (3,4)
```

**ColoredPoint Class**:
- Inherits from `Point`.
- Compilation error: As there's no default constructor in `Point`, it throws an error. If a class doesn't have a no-arg constructor, subclasses must call another constructor explicitly.

---

#### **Inheritance - Subclass constructor**

**Subclass Constructor**:
- The very first line in a subclass constructor should be a call to the superclass's constructor. This is achieved using the `super()` method.
```Java
public class ColoredPoint extends Point {
    int x,y;
    public ColoredPoint() {
        super(); 
    }
}  
```
This emphasizes the concept of initializing the superclass part of an instance before initializing the subclass-specific attributes.

---

#### **Why call super(...) in Inheritance?**

**Concept**:
- When a subclass object is instantiated, there isn't a separate instance of the superclass created inside it.
- Instead, the subclass instance incorporates the superclass's attributes and behaviors. This emphasizes "CODE REUSE" and not "instance reuse".

**Example**:
- Consider a `ColoredPoint` instance with `x=2`, `y=3`, and `color="blue"`.
- It doesn't mean there's an inner `Point` instance inside `ColoredPoint`. It's just code reuse.


### Inheritance – Fields and Methods

_View the PPT directly_

## Static and Dynamic Types with super and sub classes


#### **Static and Dynamic Types**

**Static (Compile-Time) Type:** It refers to the type assigned to the variable at the time of declaration.

Example: `Point p1 = new Point(2,3);`
- `p1` is declared of type `Point`, so its static type is `Point`.



**Dynamic (Run-Time) Type:** It refers to the type of the actual object that a variable refers to during program execution.

Example: `Point p1 = new Point(2,3);`
- The object created is of type `Point`, so the dynamic type of `p1` is also `Point`.

#### **Inheritance and Dynamic Binding**

A subclass can always be referred to by a superclass variable.
Example: `Point p3 = new ColoredPoint(2,3,"red");`
- Static type: `Point`
- Dynamic type: `ColoredPoint`

Not every superclass is an instance of the subclass, so the reverse assignment is invalid and will not compile.
- Invalid Example: `ColoredPoint p4 = new Point(5,6);`

Dynamic Binding: At runtime, the JVM uses the dynamic type (actual object's type) to determine which method to execute.
Example: 
```Java
Point p3 = new ColoredPoint(2,3,"red");
System.out.println(p3.toString());
```
The overridden `toString()` in `ColoredPoint` is called, not the one in `Point`.

#### **Compile-time Errors with Dynamic Types**

If the static type of a variable doesn't have a particular method, trying to call that method will result in a compile-time error, even if the dynamic type has that method.
Example:
```Java
Point p5 = new ColoredPoint(1,2,green);
System.out.println(p5.getColor());  // Compile-time error
```
The method `getColor()` is not present in the `Point` class, so the compiler flags an error.