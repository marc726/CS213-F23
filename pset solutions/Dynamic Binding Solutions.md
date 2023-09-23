### Problem 1:

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
##### Solution:
```Java
class TestAnimal{
	Animal animal = new Animal();
	animal.sound();//object is already associated with constructor
	Animal dog = new Dog();
	dog.sound(); 
	Animal cat = new Cat();
	cat.sound();
}
```

### Problem 2:

Expand on the previous classes. Update the `Dog` class such that it has a method `parentSound()` that calls the `sound()` method from the parent class.

**Expected Output**:
```
Dog barks 
Animal makes a sound
```

##### Solution:
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
    void parentSound(){
		super.sound();
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Cat meows");
    }
}
```

### Problem 3:

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

##### Solution:
`A obj1 = new B();`
Here, we're creating an instance of `B` but the reference type is `A`. This means `obj1` is an instance of `B` but is being referred to as an instance of `A`.

_(refer back to P1)_ Animal is the ref type but dog is the instance (type of animal).

`obj1.display();`
The method `display()` is called on `obj1`. Even though the reference type is `A`, due to dynamic binding in Java, the overridden version in the actual object type (`B`) will be called.

_(again refer back to the animal ref type but dog instance)_

### Problem 4:

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

##### Solution:
`Shape shape1 = new Circle();`
Here, `shape1` is a reference of type `Shape`, but it's pointing to an instance of `Circle`. In other words, the reference type is `Shape`, but the object it refers to is of type `Circle`.

`shape1.draw();`
Since `shape1` refers to an object of type `Circle`, and `Circle` has overridden the `draw()` method from `Shape`, the `draw()` method of `Circle` will be invoked due to dynamic binding. Thus, the output is `Drawing a circle`.

`shape1.draw("triangle");`
The `Circle` class does not override the `draw(String type)` method from `Shape`. So, when we call this method with a `String` parameter, the version in the `Shape` class will be executed, producing the output `Drawing a triangle`.

Note: Dynamic binding ensures that the method related to the actual object's class (`Circle`) is called, not just the reference type's class (`Shape`). But when a method isn't overridden in the actual object's class, it'll use the method from the reference type's class or its ancestors.

