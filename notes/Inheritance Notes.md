
```Java
public class Shape {
   public String draw() {
      return "Drawing a shape";
   }

   public static String describe() {
      return "Generic shape description";
   }
}

public class Circle extends Shape {
   public String draw() {
      return "Drawing a circle";
   }

   public static String describe() {
      return "Circle is a shape with all points equidistant from the center";
   }
}
```

```
Shape shape = new Circle();
System.out.println(shape.draw());
System.out.println(shape.describe());
```

`public String draw() {}` - instance method. determined at runtime. 

`public static String describe() {}` - Static method. determined at compile time. 

**Polymorphism and Dynamic (Runtime) Binding**:

- In the shape problem, when you had a reference of type `Shape` pointing to an object of type `Circle`, this is polymorphism in action.
- When the `draw()` method was called on that reference, the Java runtime (not the compiler) decided which version of the `draw()` method to execute based on the actual object type (i.e., `Circle`). This is called dynamic binding or runtime polymorphism.


**Static (Compile-time) Binding**:

- The behavior of static methods, like `describe()`, is determined at compile-time based on the reference type.
- Since the reference type of `shape` was `Shape`, the `describe()` method from the `Shape` class was chosen by the compiler during the compile-time phase. Even if the runtime object is a `Circle`, this doesn't change the fact that a static method from `Shape` was chosen at compile-time.
