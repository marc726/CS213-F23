
### Basic Understanding

a) **True/False**: Every class in Java is directly or indirectly derived from the Object class.

b) **MCQ**: Which keyword is used to inherit a class in Java? 
	a) `implements` 
	b) `inherits` 
	c) `extends` 
	d) `derived`

### Coding

Given the class `Point` defined as:

```Java
public class Point {
    int x, y;
}
```

a. Write a derived class `ColoredPoint` that adds an instance variable `color` of type `String` to represent the color of the point.

b. Extend the `ColoredPoint` class to add a method `display()` that prints the x, y coordinates and the color of the point.

### Advanced Concepts


a) **True/False**: In Java, multiple inheritance is supported through the use of interfaces.

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

### Practical 

a) Consider a basic e-commerce application. Create an abstract class `Product` with attributes like `id`, `name`, and `price`. Extend this class to create two derived classes: `Electronics` (which has attributes like `warrantyPeriod` and `brand`) and `Clothing` (which has attributes like `size` and `fabricType`). Implement appropriate constructors and methods to display product details.


b) Explain the concept of dynamic method dispatch in Java with a suitable example.

### Challenge Problem

Implement a class hierarchy representing geometric shapes. Start with an abstract class `Shape` with methods `area()` and `perimeter()`. Extend this class to create classes like `Circle`, `Rectangle`, and `Triangle`. Implement the area and perimeter methods for each derived class. Create a driver class to test and display the area and perimeter of each shape.
