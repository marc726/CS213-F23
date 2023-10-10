
The following problems cover material from all psets up to #3 which are what encompass this exam.  This is to be used to test your knowledge and find gaps. 

## Inheritance, Static Members

#### 1. Inheritance and Object Creation:

1. `B c = new B();`
 **Not valid**. `B` does not have a no-argument constructor. The default no-arg constructor for the superclass `A` does not apply to the subclass `B` since `B` has explicitly defined constructors.
 
1. `A s = new B(1);`
**Valid**. You're assigning an instance of a subclass (`B`) to a reference of its superclass (`A`). `B` does have a constructor that takes a single `int` argument.

2. `B c = new B(1, 9);`
**Valid**. The class `B` has a constructor that takes two `int` arguments. It subsequently calls the corresponding constructor of its superclass `A`.

1. `A t = new B(1, 9, 4);`
**Not valid**. Neither class `A` nor class `B` has a constructor that accepts three `int` arguments.

1. `B t = (new B(1)).new B(1);`
*Not valid**. The syntax is incorrect. The `new` keyword is used to create new instances of a class. The nested `new` usage inside the parentheses is invalid.

1. `B b = new A(1, 2);`
**Not valid**. You're trying to assign an instance of a superclass (`A`) to a reference of its subclass (`B`). This is not allowed unless a proper casting is done, and even then, it is risky and might result in a `ClassCastException` at runtime if the actual object is not an instance of `B`.

---
#### 2a. Dynamic Binding, Method Overriding and `toString`:

1When you create a new instance of `E` using `B b = new E();`, you're creating an object of class `E` but referencing it with a reference of type `B`.

When you execute `System.out.println(b);`, the `println` method will internally call the `toString` method of the object referenced by `b`.

Although `b` is of type `B`, the actual object is of type `E`. Java uses dynamic method dispatch for instance methods, which means the method that gets executed is based on the actual runtime type of the object, not the reference type. Therefore, the `toString` method of class `E` will be called, not the one in class `B`.

Within the `toString` method of class `E`, you're calling `getX()` which returns the `x` value from class `B`. In class `B`, the `x` value is never initialized, so it takes the default value for `int`, which is `0`.

The `toString` method of `E` then concatenates the `x` value (`0`) with `y` value (`3`) and returns the resulting string.

Thus, the answer is `03`.
#### 2b.  Dynamic Binding in Polymorphism:

1. 
```
Bark
Meow
```

2. The variable `myDog` is declared as an `Animal` type. While it's true that the actual object it refers to is an instance of `Dog`, the compiler checks method calls against the reference type (i.e., `Animal`), not the actual object type. Since the `Animal` class doesn't have a `fetch()` method, it results in a compile-time error.

3. **Change the Reference Type**: If you know that `myDog` will always be a `Dog` object, you can change the type of the reference or **Type Cast** to `((Dog) myDog).fetch();`
#### 2c.  Dynamic Binding with Inheritance:

1. 
```
Drawing a shape.
Drawing a red shape.
s1 is a: Generic shape
```

2. **The line `System.out.println("s2 has color: " + s2.getColor());` is commented out. Predict what would happen if you uncomment it and try to compile the program. Why does this occur?** If you uncomment this line and try to compile the program, you'll get a compilation error. The reason is that the reference variable `s2` is of type `Shape`, and the `Shape` class doesn't have a `getColor()` method. The compiler checks method calls against the reference type (in this case, `Shape`), not against the actual object type (which is `ColoredShape`).

3. **Change the Reference Type** 
```Java
ColoredShape s2 = new ColoredShape("red");
System.out.println("s2 has color: " + s2.getColor());
```

or

**Type Cast**
```Java
System.out.println("s2 has color: " + ((ColoredShape) s2).getColor());
```

---

####  3. Static Methods and Inheritance:

<u>Static methods are associated with the class itself</u>, not its instances. When you call a static method, it's not subjected to the usual polymorphic behavior that instance methods have in Java. This means static methods are not overridden in the usual sense.

You're using a reference of type `V` to refer to an instance of `W`.

When we call: `System.out.println(v.stuff());

We are actually calling the static method of class `V`, because the reference type is `V`. It does not matter that the actual object is of type `W`. In the context of static methods, the type of reference determines which static method is invoked, not the type of the object.

Thus, `V.stuff()` is called, and the output is `1`.

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

The statement `new Foo().bar(new Child());` is calling the `bar` method with an argument of type `Child`.

Here's how the compiler resolves the method call:

- The compiler first tries to find the overloaded `bar` method that matches the `Child` type. Since there's no method that takes a `Child` directly, it looks up the inheritance hierarchy.

- The next type up the hierarchy is `Parent`. The `Foo` class does have a `bar` method that takes a `Parent`, so the compiler matches the call to this method.

- If there was no `bar` method that took a `Parent`, the compiler would continue looking up the hierarchy and would match with the `bar` method that takes a `GrandParent`.

Since there is a `bar` method that takes a `Parent` and `Child` is a subclass of `Parent`, the compiler resolves the method call to `bar(Parent p)`, and thus the output will be: `called with type Parent

---
#### 5. Final Methods, Static Methods, and Inheritance (also requiring the creation of a basic method):

The given code won't compile. 

The `displayInfo()` method is defined in the `Child` class and not in the `Parent` class. When you create the reference `Parent p = new Child();`, you can only call methods that are defined in the `Parent` class or inherited by the `Child` class from the `Parent` class. In this scenario, the `displayInfo()` method is not available in the `Parent` class.

Therefore, the line `p.displayInfo();` will result in a compilation error, as the `displayInfo()` method is not defined for the reference type `Parent`.

To mitigate this, you would have to change the reference type to `Child`:
```Java
Child c = new Child();
c.displayInfo();
```
then output would be: 
```
I am in class Parent, dynamic invocation.
I am in class Child, static invocation.
```

Note: `printName()` method is called before the `printClassName()` method within the `displayInfo()` method. Therefore `I am in class Parent, dynamic invocation.` will print first.

##  Interfaces

#### 1. **Interface Implementation & Compilation**:

Class `D` is a simple class with no methods or properties. It compiles.

Class `C` implements `Comparable<D>`. So, `C` should have a method with the signature `int compareTo(D o)`. This requirement is satisfied in the given class. It compiles.

Interfaces `I` and `J` both declare a method `stuff()`. Both interfaces compile.

Class `F` implements both interfaces `I` and `J`. Since both `I` and `J` have a method `stuff()`, `F` must provide an implementation for this method. However, since the method signature (name and parameters) is the same in both interfaces, `F` only needs to provide one implementation for `stuff()`. But, from the given code, class `F` doesn't provide an implementation for `stuff()`. Therefore, class `F` won't compile.

So, while the first three components (`D`, `C`, `I`, and `J`) will compile, **class `F` will not compile** because it doesn't provide an implementation for the `stuff()` method.

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

The code will not compile.

- Both interfaces `I` and `J` declare a method named `stuff()`. However, the return types of these methods are different. `I` has `void stuff();` and `J` has `int stuff();`.

- When a class tries to implement both interfaces, there's a conflict, because Java does not support method overloading based solely on return type. So the `F` class cannot provide a single method implementation that would satisfy both interfaces.

To fix this, either: 

1. Change one of the interfaces so that the methods don't conflict. This might involve renaming one of the methods or changing their parameters in a way that they can be overloaded.

2. Choose not to implement one of the interfaces in the `F` class.


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

The `binarySearch` method in the `Searcher` class has a generic type parameter `<T>` that extends `Comparable<T>`. This means that the method expects an array of items where each item type implements `Comparable` of its own type.

Given the following class definitions:

-  `X` implements `Comparable<X>`, meaning an instance of `X` can be compared with another instance of `X`.

-  `Z` implements `Comparable<X>`, which means an instance of `Z` can be compared with an instance of `X`, but not necessarily with another instance of `Z`.

When you call: `binarySearch(zs,new Z());`

The generic type `T` is inferred to be `Z`. However, `Z` doesn't implement `Comparable<Z>`, it implements `Comparable<X>`. This means the type `Z` does not match the constraint `<T extends Comparable<T>>` in the `binarySearch` method.

So, the code will not compile because the `binarySearch` method's type constraint is not satisfied with the given array and item.

To fix this, you'd need to either:

1. Modify the `Z` class to implement `Comparable<Z>` and provide an appropriate `compareTo` method.
2. Modify the type constraint of the `binarySearch` method, but that would affect the general utility and correctness of that method for other scenarios.

---
#### 4. **Algorithm Interface Design**:

```Java
public interface SortingStrategy<T extends Comparable<T>> { void sort(T[] array); }

public class InsertionSort<T extends Comparable<T>> implements SortingStrategy<T> {
    @Override
    public void sort(T[] array) {
        // Insertion sort logic
        // ...
    }
}

public class QuickSort<T extends Comparable<T>> implements SortingStrategy<T> {
    @Override
    public void sort(T[] array) {
        // Quicksort logic
        // ...
    }
}

public class HeapSort<T extends Comparable<T>> implements SortingStrategy<T> {
    @Override
    public void sort(T[] array) {
        // Heapsort logic
        // ...
    }
}
```

---
#### 5. **Interface Comparison**:

Define the difference between `java.lang.Comparable<T>` and `java.util.Comparator<T>`. Then, create a basic method that demonstrates a use case where `Comparator<T>` offers an advantage over `Comparable<T>`.

1. **`java.lang.Comparable<T>`**:
    
    - Located in the `java.lang` package.
    - Used to define the natural order of an object. When a class implements this interface, it's indicating that its instances have an intrinsic way of ordering.
    - Contains a single method: `int compareTo(T obj)`.
    - An example would be the `String` class, which implements `Comparable` to provide a natural alphabetical ordering.
2. **`java.util.Comparator<T>`**:
    
    - Located in the `java.util` package.
    - Used to define external orders for an object. That means you can have multiple ordering strategies without modifying the class itself.
    - Contains multiple methods, but the most used one is `int compare(T o1, T o2)`.
    - Typically used when you need multiple ways to sort an object or when you can't modify the source code of the class to implement `Comparable`.

**Advantage of using `Comparator<T>`**: `Comparator` offers flexibility in sorting objects in different ways. This is especially beneficial when:

- You don't have access to the source code of a class (so you can't make it implement `Comparable`).
- You need more than one way to sort instances of a class.

**Demonstration**: Let's say you have a `Person` class, and you want to sort a list of persons by age and then by name. With `Comparator`, you can have separate strategies for both:
```Java
import java.util.Arrays;
import java.util.Comparator;

class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class ComparatorDemo {
    public static void main(String[] args) {
        Person[] persons = {
            new Person("John", 25),
            new Person("Anna", 20),
            new Person("Mike", 25)
        };

        // Sort by age
        Arrays.sort(persons, new Comparator<Person>() {
            @Override
            public int compare(Person p1, Person p2) {
                return Integer.compare(p1.age, p2.age);
            }
        });
        System.out.println(Arrays.toString(persons)); // Anna (20), John (25), Mike (25)

        // Sort by name
        Arrays.sort(persons, new Comparator<Person>() {
            @Override
            public int compare(Person p1, Person p2) {
                return p1.name.compareTo(p2.name);
            }
        });
        System.out.println(Arrays.toString(persons)); // Anna (20), John (25), Mike (25)
    }
}
```

In the above code, we didn't modify the `Person` class itself but used two different sorting strategies using `Comparator`. This would not be possible with only `Comparable` unless we had modified the `Person` class each time.

---
## Access Levels, Inner Classes, Abstract Classes, Polymorphism

#### 1. **Access Levels and Inheritance**:

1. **Are protected members of `A` accessible in `C`?**
    
    No, the protected members of `A` are not accessible in `C`.
    
    Justification: In Java, a protected member of a class is accessible within its own package and in subclasses, **but** there's a catch when it comes to subclasses outside the package. A subclass outside the package can inherit a protected member, but it can't access the inherited protected member through a reference whose declared type is the superclass unless it's a reference to itself or its subclass.
    
    Given the setup:
    
    - `C` is in package `cd`.
    - `A` is in package `ab`.
    
    So, `C` can inherit the protected members of `A` because `C` extends `A`, but it can't access them on an instance of `A`. However, it can access them on an instance of `C` or its subclasses.
    
2. **Are protected members of `A` accessible in `D`?**
    
    Yes, the protected members of `A` are accessible in `D`.
    
    Justification: As stated above, a subclass outside the package of the superclass can inherit the protected members. Given the hierarchy:
    
    - `D` extends `B`.
    - `B` extends `A`.
    
    So, `D` indirectly inherits from `A` through `B`. Because `D` is a subclass of `B` (which in turn is a subclass of `A`), it can access the protected members of `A` on an instance of `D` or its subclasses. Additionally, since `B` and `A` are in the same package (`ab`), `B` can access the protected members of `A` directly, and since `D` extends `B`, it too can access those protected members.


---

#### 2. **Inner Classes**:

Typical instantiation (requires an instance of the outer class):
```Java
public class InnerApp {
    public static void main(String[] args) {
        Outer outer = new Outer("Hello from Outer");
        Outer.Inner inner = outer.getInnerInstance();
        System.out.println(inner.toString());
    }
}
```

If we were to make `Inner` a static nested class:
```Java
public class Outer {
    private String outerField;

    public Outer(String outerField) {
        this.outerField = outerField;
    }

    public static class Inner {
        private String fieldFromOuter;

        public Inner(String field) {
            this.fieldFromOuter = field;
        }

        @Override
        public String toString() {
            return fieldFromOuter;
        }
    }
}
```

Then you can instantiate the `Inner` class directly without an `Outer` instance:
```Java
public class InnerApp {
    public static void main(String[] args) {
        Outer.Inner inner = new Outer.Inner("Hello from directly instantiated Inner");
        System.out.println(inner.toString());
    }
}
```

#### 3. **Abstract Classes & Compilation**:

1. **`public abstract class X { ... }`**
    
    This will compile.
    
    Explanation: It's a simple abstract class definition. There's nothing wrong with it.
    
2. **`public abstract class Y extends X { ... }`**
    
    This will compile.
    
    Explanation: Class `Y` is defined as an abstract class and it extends another abstract class `X`. This is allowed in Java.
    
3. **`public interface I { void stuff(); }`**
    
    This will compile.
    
    Explanation: It's a basic interface definition with an abstract method `stuff()`. All methods in interfaces are implicitly abstract, so there's no need to specify it. There's nothing wrong with this definition.
    
4. **`public abstract class C { ... }`**
    
    This will compile.
    
    Explanation: Again, it's a simple abstract class definition. There's nothing wrong with it.
    
5. **`public class D extends C { ... }`**
    
    This might or might not compile, and it depends on the details in class `C`.
    
    Explanation: Class `D` extends abstract class `C`. If `C` has any abstract methods, then class `D` (as a concrete class) must provide implementations for all of those abstract methods. If `D` does not provide implementations for all of the abstract methods from `C`, it won't compile. If `C` doesn't have any abstract methods or `D` provides implementations for all of them, then it will compile.

---

#### 4. **Polymorphism with People & Students**:

```Java
import java.util.ArrayList;

class Address {
    private String street;
    private String city;
    private String state;
    private String zip;

    public Address(String street, String city, String state, String zip) {
        this.street = street;
        this.city = city;
        this.state = state;
        this.zip = zip;
    }

    @Override
    public String toString() {
        return street + ", " + city + ", " + state + " " + zip;
    }
}

class Person {
    protected Address homeAddress;

    public Person(Address homeAddress) {
        this.homeAddress = homeAddress;
    }

    public void printAddress() {
        System.out.println("Home Address: " + homeAddress);
    }
}

class Student extends Person {
    private Address schoolAddress;

    public Student(Address homeAddress, Address schoolAddress) {
        super(homeAddress);
        this.schoolAddress = schoolAddress;
    }

    @Override
    public void printAddress() {
        super.printAddress();
        System.out.println("School Address: " + schoolAddress);
    }
}

public class AddressApp {
    public static void main(String[] args) {
        ArrayList<Person> persons = new ArrayList<>();

        Address johnHome = new Address("123 Elm St", "Anytown", "NY", "12345");
        Address school = new Address("456 School St", "Anytown", "NY", "12345");
        persons.add(new Person(johnHome));
        persons.add(new Student(johnHome, school));

        for (Person person : persons) {
            person.printAddress();
            System.out.println("-------------");
        }
    }
}
```

- The `Address` class is a simple representation of an address.
- In the `Person` class, the `printAddress` method prints the home address.
- In the `Student` class, we override the `printAddress` method. We first call the super class's (`Person`) `printAddress` method using `super.printAddress()`, which prints the home address. Then, we print the school address for the student.
- The `AddressApp` class demonstrates how you can store both `Person` and `Student` objects in an `ArrayList` and call the `printAddress` method on each.

For `Student` objects in the `ArrayList`, the overridden `printAddress` method in the `Student` class will be called, printing both the home and school addresses. For `Person` objects, only the home address will be printed.


---
#### 5. **Shape Hierarchy & Polymorphism**:

```Java
abstract class Shape {
    // Abstract method to calculate the area of the shape
    public abstract double area();

    // Static method to find the shape with the largest area
    public static Shape biggest(Shape[] s) {
        if (s == null || s.length == 0) {
            return null;  // Handle empty or null array
        }

        Shape largestShape = s[0];
        for (int i = 1; i < s.length; i++) {
            if (s[i].area() > largestShape.area()) {
                largestShape = s[i];
            }
        }

        return largestShape;
    }
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

// If we later add more shapes like Rhombus:
class Rhombus extends Shape {
    private double diagonal1;
    private double diagonal2;

    public Rhombus(double diagonal1, double diagonal2) {
        this.diagonal1 = diagonal1;
        this.diagonal2 = diagonal2;
    }

    @Override
    public double area() {
        return 0.5 * diagonal1 * diagonal2;
    }
}
```

