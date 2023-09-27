
Java interfaces allow for the abstraction of method signatures without implementation. This problem set will challenge your understanding of interfaces and their applications in Java.

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

