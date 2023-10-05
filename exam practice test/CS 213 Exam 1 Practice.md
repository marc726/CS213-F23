
The following problems cover material from all psets up to #3 which are what encompass this exam.  This is to be used to test your knowledge and find gaps. 

## Inheritance, Static Members

#### 1. Inheritance and Object Creation:

Given the class structure:
```Java
public class A {
   public A() {}
   public A(int a, int b) {}
}

public class B extends A {
   public B(int r) {}
   public B(int r, int w) { 
      super(r, w);
   }
}
```

Determine the legitimacy of the following constructor calls:

``` Java
B c = new B();
A s = new B(1);
B c = new B(1, 9);
A t = new B(1, 9, 4);
B t = (new B(1)).new B(1);
B b = new A(1, 2);
```

For invalid calls, why are they invalid.

---
#### 2a. Dynamic Binding, Method Overriding and `toString`:

Given the classes:
```Java 
public class B {
   private int x;
   public int getX() {
      return x;
   }
   public String toString() {
      return x + "";
   }
}

public class E extends B {
   public int y=3;
   public String toString() {
      return getX() + y + "";
   }
}
```
What is the output of the following code?
```Java
B b = new E();
System.out.println(b);
```

#### 2b.  Dynamic Binding in Polymorphism:

Observe the following code: 
```Java
class Animal {
    void makeSound() {
        System.out.println("Some sound...");
    }
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark");
    }

    void fetch() {
        System.out.println("Fetch the ball");
    }
}

class Cat extends Animal {
    void makeSound() {
        System.out.println("Meow");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        Animal myCat = new Cat();

        myDog.makeSound();
        myCat.makeSound();

        // Uncomment the following line
        // myDog.fetch();
    }
}
```

1. What is the output when the program is run?
2. Why does the uncommented call to `myDog.fetch()` result in a compile-time error even though the `myDog` object is an instance of the `Dog` class?
3. How can you modify the code to successfully call the `fetch` method on the `myDog` object?

#### 2c.  Dynamic Binding with Inheritance:

Imagine there are two classes: `Shape` and a subclass `ColoredShape` : 

```Java
public class Shape {
    void draw() {
        System.out.println("Drawing a shape.");
    }

    String getType() {
        return "Generic shape";
    }
}

public class ColoredShape extends Shape {
    String color;

    ColoredShape(String color) {
        this.color = color;
    }

    @Override
    void draw() {
        System.out.println("Drawing a " + color + " shape.");
    }

    String getColor() {
        return this.color;
    }
}
```

Now, in the main method:
```Java
public class ShapeApp {
    public static void main(String[] args) {
        Shape s1 = new Shape();
        Shape s2 = new ColoredShape("red");

        s1.draw();
        s2.draw();

        System.out.println("s1 is a: " + s1.getType());
        // Uncomment the following line
        // System.out.println("s2 has color: " + s2.getColor());
    }
}
```

1. What will be the output when you run the `ShapeApp` class?
2. The line `System.out.println("s2 has color: " + s2.getColor());` is commented out. Predict what would happen if you uncomment it and try to compile the program. Why does this occur?
3. How can you modify the code to access the `getColor()` method of `s2` object without causing a compilation error?


---

####  3. Static Methods and Inheritance:

Given:
```Java
public class V {
   public static int stuff() {
      return 1;
   }
}

public class W extends V {
   public static int stuff() {
      return 2;
   }
}
```
What is the output of:
```Java
V v = new W(); 
System.out.println(v.stuff());
```

---
#### 4. Method Overloading and Inheritance:

```Java
class GrandParent { }
class Parent extends GrandParent{ }
class Child extends Parent { }

class Foo {
   public void bar(GrandParent p) {
      System.out.println("called with type GrandParent");
   }
   public void bar(Parent p) {
      System.out.println("called with type Parent");
   }
}

public class Test {
   public static void main(String[] args) {
      new Foo().bar(new Child());
   }
}
```

What is the output of this code? Explain.

---

#### 5. Final Methods, Static Methods, and Inheritance (also requiring the creation of a basic method):

Given: 
```Java
public class Parent {
   public final void printName() {
      System.out.println("I am in class Parent, dynamic invocation.");
   }
}

public class Child extends Parent {
   public void displayInfo() {
      printName();
      printClassName();
   }
   public static void printClassName() {
      System.out.println("I am in class Child, static invocation.");
   }
}
```
Write the output of the following code:

```Java
Parent p = new Child();
p.displayInfo();
```

##  Interfaces

#### 1. **Interface Implementation & Compilation**:

Given the following class and interface definitions, state if the code will compile. If not, explain why.

```Java
public class D { }
public class C implements Comparable<D> {
   public int compareTo(D o) { return 0; }
}
public interface I { void stuff(); }
public interface J { void stuff(); }
public class F implements I,J { }
```

---

#### 2. **Multiple Interfaces with Methods**:

Given the following interface definitions and class, state if the code will compile. If it does, implement the required methods in the class. If not, explain the reason.

```Java
public interface I { void stuff(); }
public interface J { int stuff(); }
public class F implements I,J {
    // Implement required methods here
}
```

---

#### 3. **Generics with Comparable Interface**:

Given the following class definitions, determine if the `Searcher` class's `binarySearch` method can accept the specified array and item. If not, explain why.

```Java
class X implements Comparable<X> {
    public int compareTo(X o) { return 0; }
}
class Z implements Comparable<X> { }
public class Searcher {
    public static <T extends Comparable<T>> 
    boolean binarySearch(T[] list, T item) {
        return false;
    }
    public static void main(String[] args) {
        Z[] zs = new Z[2];
        zs[0] = new Z();
        zs[1] = new Z();
        binarySearch(zs,new Z());
    }
}
```

#### 4. **Algorithm Interface Design**:

Imagine you have three sorting algorithms: insertion sort, quicksort, and heapsort. Design an interface that allows users to utilize any of these algorithms in their applications and switch from one to another with minimal code changes.

---
#### 5. **Interface Comparison**:

Define the difference between `java.lang.Comparable<T>` and `java.util.Comparator<T>`. Then, create a basic method that demonstrates a use case where `Comparator<T>` offers an advantage over `Comparable<T>`.

## Access Levels, Inner Classes, Abstract Classes, Polymorphism

#### 1. **Access Levels and Inheritance**:

Given two packages `ab` and `cd`, with the following class hierarchies: Classes `A` and `B` are in package `ab`, and classes `C` and `D` are in package `cd`. Both `C` and `B` extend `A`, and `D` extends `B`. All classes are declared to be public.

- Are protected members of `A` accessible in `C`? Justify your answer.
- Are protected members of `A` accessible in `D`? Justify your answer.

---

#### 2. **Inner Classes**:

Design a class named `Outer` that contains an inner class named `Inner`. The `Outer` class has a method that returns an instance of the inner class. `Outer` has a private String field initialized by the constructor, and the `Inner` class has a `toString()` method that displays this field. In a separate class named `InnerApp`, instantiate the inner class without creating an object of the outer class.

#### 3. **Abstract Classes & Compilation**:

Given the following class and method definitions:

```Java
public abstract class X { ... }
public abstract class Y extends X { ... }
public interface I { void stuff(); }
public abstract class C { ... }
public class D extends C { ... }
```
State for each provided class or method if the code will compile. If not, explain why.

---

#### 4. **Polymorphism with People & Students**:

Design a system where you have a `Person` class and a `Student` class. The `Student` class is a subclass of `Person`. Every person has a home address, while every student has a school address in addition to the home address. You have an array list storing all `Person` and `Student` objects. Describe a method in the `Person` class that prints the address of the person. How would this method behave for `Student` objects?

---
#### 5. **Shape Hierarchy & Polymorphism**:

Given an abstract class `Shape` with subclasses `Circle` and `Rectangle`, complete the method in the `Shape` class:

```Java
public static Shape biggest(Shape[] s)
```

This method should return the shape with the largest area. The shapes should be compared using their area. If more shapes, like `Rhombus`, were added to the hierarchy, would your method work seamlessly?