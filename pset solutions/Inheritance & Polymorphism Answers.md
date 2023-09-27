
### Basic Understanding

a) **True/False**: Every class in Java is directly or indirectly derived from the Object class.

##### Solution
True  
	**Explanation**: In Java, if a class doesn’t extend any other class then it is directly derived from the `Object` class. If it extends another class, it is indirectly derived from the `Object` class because the parent class itself will be derived from `Object`.


b) **MCQ**: Which keyword is used to inherit a class in Java? 
	a) `implements` 
	b) `inherits` 
	c) `extends` 
	d) `derived`

##### Solution
c) `extends`  
    **Explanation**: In Java, the `extends` keyword is used to inherit properties and behaviors (methods) from another class.

### Coding
Given the class `Point` defined as:

```Java
public class Point {
    int x, y;
}
```

a. Write a derived class `ColoredPoint` that adds an instance variable `color` of type `String` to represent the color of the point.
##### Solution:
```Java
public class ColoredPoint extends Point {
    String color;
}
```

b. Extend the `ColoredPoint` class to add a method `display()` that prints the x, y coordinates and the color of the point.
##### Solution:
```Java
public class ColoredPoint extends Point {
    String color;

    public void display() {
        System.out.println("Coordinates: (" + x + "," + y + ") Color: " + color);
    }
}
```

### Advanced Concepts


a) **True/False**: In Java, multiple inheritance is supported through the use of interfaces.

##### Solution: 
True  
**Explanation**: Java doesn't support multiple inheritance through classes to avoid the diamond problem. However, it does support multiple inheritance through interfaces, where a class can implement multiple interfaces.



b) **MCQ**: What will be the output of the following code?


```Java
class A {
    void display() {
        System.out.println("Class A");
    }
}

class B extends A {
    void display() {
        System.out.println("Class B");
    }
}

public class Main {
    public static void main(String[] args) {
        A obj = new B();
        obj.display();
    }
}
```

a) Class A  
b) Class B  
c) Compilation error  
d) None of the above

##### Solution: 
b) Class B  
**Explanation**: This is a classic example of method overriding and polymorphism. The object is of class `A` but it refers to an instance of class `B`. Thus, the `display()` method of class `B` is called.

### Practical 

a) Consider a basic e-commerce application. Create an abstract class `Product` with attributes like `id`, `name`, and `price`. Extend this class to create two derived classes: `Electronics` (which has attributes like `warrantyPeriod` and `brand`) and `Clothing` (which has attributes like `size` and `fabricType`). Implement appropriate constructors and methods to display product details.

```Java
abstract class Product {
    int id;
    String name;
    double price;

    // Constructors, getters, setters, etc.

    public void display() {
        System.out.println("ID: " + id + " Name: " + name + " Price: " + price);
    }
}

class Electronics extends Product {
    String warrantyPeriod;
    String brand;

    // Constructors, getters, setters, etc.
    
    @Override
    public void display() {
        super.display();
        System.out.println("Warranty: " + warrantyPeriod + " Brand: " + brand);
    }
}

class Clothing extends Product {
    String size;
    String fabricType;

    // Constructors, getters, setters, etc.
    
    @Override
    public void display() {
        super.display();
        System.out.println("Size: " + size + " Fabric: " + fabricType);
    }
}
```


b) Explain the concept of dynamic method dispatch in Java with a suitable example.

##### Solution: 
Dynamic method dispatch is a mechanism by which a call to an overridden method is resolved at runtime rather than at compile-time. This is central to Java's implementation of runtime polymorphism. When an overridden method is called through a superclass reference, Java uses the object's class (not the reference's type) to determine which version of the method should be executed.

```Java
class A {
    void show() {
        System.out.println("In A");
    }
}

class B extends A {
    @Override
    void show() {
        System.out.println("In B");
    }
}

public class Test {
    public static void main(String[] args) {
        A obj = new B();  // superclass reference but B's object
        obj.show();  // calls B's version of show()
    }
}
```

### Polymorphism

1) **True/False**: Polymorphism allows us to perform a single action in different ways.

##### Solution:
True  
**Explanation**: Polymorphism, derived from Greek words meaning "many shapes", allows us to invoke methods of the same name in different objects and get different behaviors.



2) **MCQ**: Which concept in Java is the essence of polymorphism? 
	a) Overloading 
	b) Overriding 
	c) Hiding 
	d) Encapsulation

##### Solution: 
b) Overriding  
**Explanation**: Overriding allows subclass methods to provide a specific implementation for a method that is already defined in its superclass, which is a key aspect of runtime polymorphism.




3) Consider the following code:
```Java
class Vehicle {
    void run() {
        System.out.println("Vehicle is running");
    }
}

class Bike extends Vehicle {
    void run() {
        System.out.println("Bike is running safely");
    }
}

public class TestPolymorphism {
    public static void main(String[] args) {
        Vehicle v = new Bike();
        v.run();
    }
}
```

What will be the output when `TestPolymorphism` is executed?
##### Solution:
**Answer**: Bike is running safely  
**Explanation**: Even though the reference type is `Vehicle`, the object type is `Bike`. Due to runtime polymorphism, the overridden method in the `Bike` class is called.



4) **True/False**: Overloading is an example of runtime polymorphism.
##### Solution
False  
**Explanation**: Overloading is an example of compile-time polymorphism. The method to be invoked is determined at compile time based on the method signature.



5) Differentiate between compile-time and runtime polymorphism with suitable examples.
##### Solution:
- **Compile-time Polymorphism**: This is achieved through method overloading. In this case, the method to be executed is determined at compile time. Example: having multiple methods in a class with the same name but different parameters.
- **Runtime Polymorphism**: This is achieved through method overriding, where the subclass provides a specific implementation for a method that is already defined in its superclass. The method to be executed is determined at runtime based on the object type. Example: using the `extends` keyword to derive a class and override its methods.
