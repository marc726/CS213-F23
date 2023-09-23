### Problem 1: Basic Dynamic Binding

Given the following classes:
```Java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Cat meows");
    }
}
```

Create a class `TestAnimal` that demonstrates dynamic binding using the above classes.

**Expected Output**:
```
Animal makes a sound
Dog barks
Cat meows
```
### Problem 2: super

Expand on the previous classes. Update the `Dog` class such that it has a method `parentSound()` that calls the `sound()` method from the parent class.

**Expected Output**:
```
Dog barks 
Animal makes a sound
```

### Problem 3: Order of Binding

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
    
    void print() {
        display();
    }
}
```

Analyze the output of the following statements:

```Java
A obj1 = new B();
obj1.display();
((B)obj1).print();
```

**Expected Output**:
```
Class B
Class B
```

### Problem 4: Overriding vs Overloading

```Java
class Shape {
    void draw() {
        System.out.println("Drawing a shape");
    }

    void draw(String type) {
        System.out.println("Drawing a " + type);
    }
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing a circle");
    }
}
```

Analyze the output for the following:
```Java
Shape shape1 = new Circle();
shape1.draw();
shape1.draw("triangle");
```

Output:
```
Drawing a circle
Drawing a triangle
```
