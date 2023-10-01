
### **Given Classes and Packages:**

Classes A and B are in package `ab`, and classes C and D are in package `cd`. Classes C and B both extend A, and D extends B. All classes are declared public.

1. Can class C access protected members of class A? Justify your answer.
2. Can class D access private members of class A? Why or why not?
3. If class B has a public method that accesses a protected member of class A, can class D use that method to indirectly access the protected member of A?


---

### **Inner Classes in Java**

1. Write a class named `OuterClass` which contains an inner class named `InnerClass`. The `OuterClass` should have a private `String` field initialized by the constructor, and the `InnerClass` should override the `toString()` method to display this field. In the main method, instantiate an `InnerClass` object and print it.


2. Write a class named `OuterClass2` with an inner class `InnerClass2`. In a separate class named `InnerApp2`, create an instance of the inner class without creating an object of the outer class. Is this possible? Explain.

### **Abstract Classes in Java**

1. Review the following class declarations and determine if they will compile. If not, explain the error:
```Java
a) public abstract class X { }
b) public class X { public abstract void myMethod(); }
c) public abstract class X { public abstract void myMethod() { System.out.println("This is X"); } }
d) public abstract class X { public void myMethod() { System.out.println("This is X"); } }
e) public class Y extends X { }
```


2. Given an abstract class `Z` with an abstract method `printDetails()`, create a subclass `W` that provides an implementation for this method.


---

### **Polymorphism in Java**

Given a class hierarchy of `Shape` which includes subclasses `Circle` and `Rectangle`:

1. Implement a method in `Shape` called `largestArea(Shape[] shapes)` that returns the shape with the largest area.
2. Suppose you add a new shape, `Triangle`, to the hierarchy. Would you need to make any changes to the `largestArea` method to accommodate this new shape? Explain.
3. Implement the `Comparable` interface in the `Shape` class to compare shapes based on their area. Override the `compareTo` method in each of the shape subclasses.


---


### **Design and Implementation Considerations**

Consider an application with a `Person` class and a `Student` subclass. Every `Person` has a `homeAddress`, while every `Student` has a `schoolAddress` as well:

1. Design the `Person` and `Student` classes ensuring encapsulation principles are maintained.

2. Describe different strategies to print the address of students. Discuss the pros and cons of each strategy.

3. Implement a method in the `Person` class that prints the address and override it in the `Student` class to print both the home and school addresses.

