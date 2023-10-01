
### **Given Classes and Packages:**

Classes A and B are in package `ab`, and classes C and D are in package `cd`. Classes C and B both extend A, and D extends B. All classes are declared public.

1. Can class C access protected members of class A? Justify your answer.
2. Can class D access private members of class A? Why or why not?
3. If class B has a public method that accesses a protected member of class A, can class D use that method to indirectly access the protected member of A?

##### Solution: 
1. No, class C cannot directly access protected members of class A since they're in different packages, and C doesn't directly extend A.
2. No, class D cannot access private members of class A (or any class) as private members are only accessible within the class they're declared.
3. Yes, class D can use that method of class B to indirectly access the protected member of A because D extends B and can use its public methods


---

### **Inner Classes in Java**

1. Write a class named `OuterClass` which contains an inner class named `InnerClass`. The `OuterClass` should have a private `String` field initialized by the constructor, and the `InnerClass` should override the `toString()` method to display this field. In the main method, instantiate an `InnerClass` object and print it.

##### Solution: 
```Java
public class OuterClass {
    private String field;

    public OuterClass(String field) {
        this.field = field;
    }

    public InnerClass getInnerClass() {
        return new InnerClass();
    }

    public class InnerClass {
        @Override
        public String toString() {
            return field;
        }
    }

    public static void main(String[] args) {
        OuterClass outer = new OuterClass("Hello from OuterClass");
        InnerClass inner = outer.getInnerClass();
        System.out.println(inner);
    }
}
```


3. Write a class named `OuterClass2` with an inner class `InnerClass2`. In a separate class named `InnerApp2`, create an instance of the inner class without creating an object of the outer class. Is this possible? Explain.

##### Solution: 

It's not possible to directly instantiate a non-static inner class without first instantiating the outer class.

Explanation: An inner class is bound to the instance of the outer class. To instantiate the inner class, you first need an instance of the outer class.

### **Abstract Classes in Java**

1. Review the following class declarations and determine if they will compile. If not, explain the error:
```Java
a) public abstract class X { }
b) public class X { public abstract void myMethod(); }
c) public abstract class X { public abstract void myMethod() { System.out.println("This is X"); } }
d) public abstract class X { public void myMethod() { System.out.println("This is X"); } }
e) public class Y extends X { }
```

##### Solution: 
a) Compiles successfully.
b) Doesn't compile. You cannot have an abstract method in a non-abstract class.
c) Doesn't compile. Abstract methods cannot have a body.
d) Compiles successfully.
e) Doesn't compile. Class Y must either be declared abstract or provide an implementation for `myMethod()` from X.


2. Given an abstract class `Z` with an abstract method `printDetails()`, create a subclass `W` that provides an implementation for this method.

##### Solution:
```Java
public abstract class Z {
    public abstract void printDetails();
}

public class W extends Z {
    @Override
    public void printDetails() {
        System.out.println("Details from class W.");
    }
}
```


---

### **Polymorphism in Java**

Given a class hierarchy of `Shape` which includes subclasses `Circle` and `Rectangle`:

1. Implement a method in `Shape` called `largestArea(Shape[] shapes)` that returns the shape with the largest area.

##### Solution:
```Java
public static final Shape largestArea(Shape[] shapes) {
    Shape maxShape = null;
    double maxArea = Double.NEGATIVE_INFINITY;
    for (Shape shape : shapes) {
        if (shape.getArea() > maxArea) {
            maxArea = shape.getArea();
            maxShape = shape;
        }
    }
    return maxShape;
}
```


2. Suppose you add a new shape, `Triangle`, to the hierarchy. Would you need to make any changes to the `largestArea` method to accommodate this new shape? Explain.

##### Solution:
No changes would be required to the `largestArea` method if a new shape `Triangle` is added, as long as `Triangle` provides an implementation for the `getArea()` method.


3. Implement the `Comparable` interface in the `Shape` class to compare shapes based on their area. Override the `compareTo` method in each of the shape subclasses.

##### Solution:
```Java 
public abstract class Shape implements Comparable<Shape> {
    public abstract double getArea();

    @Override
    public int compareTo(Shape other) {
        return Double.compare(this.getArea(), other.getArea());
    }
}
```


---


### **Design and Implementation Considerations**

Consider an application with a `Person` class and a `Student` subclass. Every `Person` has a `homeAddress`, while every `Student` has a `schoolAddress` as well:

1. Design the `Person` and `Student` classes ensuring encapsulation principles are maintained.


##### Solution:
```Java
public class Person {
    private String homeAddress;

    public Person(String homeAddress) {
        this.homeAddress = homeAddress;
    }

    public void printAddress() {
        System.out.println(homeAddress);
    }
}

public class Student extends Person {
    private String schoolAddress;

    public Student(String homeAddress, String schoolAddress) {
        super(homeAddress);
        this.schoolAddress = schoolAddress;
    }

    @Override
    public void printAddress() {
        super.printAddress();
        System.out.println(schoolAddress);
    }
}
```



2. Describe different strategies to print the address of students. Discuss the pros and cons of each strategy.

##### Solution:
Different strategies to print the address of students:

- Overriding the `printAddress()` method in the `Student` class (as shown above). This will allow us to print both the home and school address when the method is called on a `Student` object.
- Not overriding the `printAddress()` method, which will only print the home address.


3. Implement a method in the `Person` class that prints the address and override it in the `Student` class to print both the home and school addresses.
##### Solution:

Implemented in part a.