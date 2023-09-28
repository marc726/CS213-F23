
### Terms: 

1. What are interfaces? What do they do?

##### Solution: 
In Java, an **interface** is a reference type, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Interfaces provide a way to achieve abstraction and multiple inheritance in Java.

Here are the key points about interfaces in Java:

a. **Abstraction**: An interface allows you to define the structure of a class without implementing its functionality. It defines "what" a class should do, but not "how" it does it. A class that implements an interface must implement all its abstract methods.

b. **Multiple Inheritance**: Unlike many object-oriented languages (including Java), where a class can inherit from only one superclass, a class can implement multiple interfaces. This allows Java to work around the restriction of single inheritance while still ensuring a form of multiple inheritance.

c. **Default Methods**: Introduced in Java 8, interfaces can have method implementations with the `default` keyword. This was done to enhance the interfaces with additional methods without affecting classes that already use this interface.

d. **Static Methods**: Java 8 also introduced the ability for interfaces to contain static methods. These are utility methods that belong to the interface type itself rather than to instances of the interface.

e. **Private Methods**: Introduced in Java 9, interfaces can have private methods, which can be useful when you want to break down a default method or a static method into sub-methods without exposing these helper methods as part of the interface.`

Here's a simple example of an interface:
```Java
interface Animal {
    void eat(); // Abstract method, no implementation
    void sleep(); // Abstract method, no implementation

    default void breathe() {
        System.out.println("Breathing...");
    }

    static void info() {
        System.out.println("Animals are living organisms.");
    }
}

class Dog implements Animal {
    @Override
    public void eat() {
        System.out.println("Dog is eating...");
    }

    @Override
    public void sleep() {
        System.out.println("Dog is sleeping...");
    }
}

public class InterfaceDemo {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.sleep();
        d.breathe();  // Calling default method
        Animal.info();  // Calling static method
    }
}
```
- The `Animal` interface has two abstract methods (`eat` and `sleep`), a default method (`breathe`), and a static method (`info`).
- The `Dog` class implements the `Animal` interface, so it must provide concrete implementations for the abstract methods of the interface (`eat` and `sleep`).

To sum it up, interfaces in Java help promote a contract-based approach to design, ensuring that classes maintain a certain structure. They also help in achieving a form of multiple inheritance in a controlled manner.

---

2. What is `Comparable`? What does it do?

##### Solution: 
In Java, the `Comparable` interface is used to order objects of a user-defined class. Classes that implement the `Comparable` interface can be used in sorting methods like `Arrays.sort()` or collection sorting methods like `Collections.sort()`.

The primary method of the `Comparable` interface is `compareTo()`, which determines the natural order of objects.

Here's a quick breakdown:
```Java
public interface Comparable<T> {
    public int compareTo(T o);
}
```

The `compareTo` method returns:

- A positive integer if the current object is greater than the specified object.
- A negative integer if the current object is less than the specified object.
- Zero if the current object is equal to the specified object.

Here's an example of a simple `Person` class that implements the `Comparable` interface:
```Java
public class Person implements Comparable<Person> {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public int compareTo(Person other) {
        return this.age - other.age;  // Comparing based on age for natural order
    }

    @Override
    public String toString() {
        return name + ": " + age;
    }

    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("John", 25));
        people.add(new Person("Alice", 22));
        people.add(new Person("Bob", 28));

        Collections.sort(people);

        for (Person person : people) {
            System.out.println(person);
        }
    }
}
```
In the above code, the `Person` class is made `Comparable` by age. So, when the list of `Person` objects is sorted using `Collections.sort()`, it will be sorted by age in ascending order.

---
### **Basic Implementation:**

Given the following code snippet, identify if it will compile successfully:

```Java
public interface Animal {
    void speak();
}

public class Dog implements Animal {
    public void speak() {
        System.out.println("Woof!");
    }
}
```

##### Solution: 
Yes, it will compile successfully.  
**Explanation:** The class `Dog` properly implements the `speak` method defined in the `Animal` interface.

---
### **Multiple Interfaces:**

Will the code below compile? If not, what's the issue?

```Java
public interface Swimmer {
    void swim();
}

public interface Runner {
    void run();
}

public class Athlete implements Swimmer, Runner {
    public void swim() {
        System.out.println("Swimming fast!");
    }

    public void run() {
        System.out.println("Running fast!");
    }
}
```

##### Solution: 
Yes, it will compile.  
**Explanation:** The class `Athlete` implements both the `swim` method from the `Swimmer` interface and the `run` method from the `Runner` interface.

---
### **Overlapping Methods:**

Analyze the code snippet below. Will it compile?

```Java
public interface Mammal {
    void display();
}

public interface Bird {
    void display();
}

public class Bat implements Mammal, Bird {
    public void display() {
        System.out.println("I am a bat!");
    }
}
```
##### Solution: 
Yes, it will compile.  
**Explanation:** Even though both the `Mammal` and `Bird` interfaces have a `display` method, there's no ambiguity in the `Bat` class since it provides a single implementation for the method.

---

### **Abstract Class and Interface:**

Consider the following code. Identify any compilation errors, if present:

```Java
public abstract class Vehicle {
    abstract void move();
}

public interface Flyable {
    void fly();
}

public class Airplane extends Vehicle implements Flyable {
    public void move() {
        System.out.println("Moving forward!");
    }

    public void fly() {
        System.out.println("Flying in the sky!");
    }
}
```

##### Solution: 
Yes, it will compile successfully.  
**Explanation:** The class `Airplane` provides concrete implementations for the abstract `move` method of the `Vehicle` class and the `fly` method of the `Flyable` interface.

---
### **Interface Default Methods:**

Examine the following code. Will it compile successfully? If not, correct the issues:

```Java
public interface Painter {
    default void paint() {
        System.out.println("Painting in default color.");
    }
}

public class Artist implements Painter {
    public void paint() {
        System.out.println("Painting in blue.");
    }
}
```
##### Solution: 
Yes, it will compile.  
**Explanation:** The class `Artist` provides its own implementation of the `paint` method, overriding the default implementation provided in the `Painter` interface.