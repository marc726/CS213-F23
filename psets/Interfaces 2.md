**Based off of pset from recitation**


### Compilation Questions:

1. Given the code:
```Java
public class A { }
public class B implements Comparable<A> {
   public int compareTo(A o) { return 0; }
}
```
a. Will this code compile? Explain your answer. 
b. If not, what changes would you make to allow it to compile?



2. Consider the scenario where you have two interfaces with default methods having the same signature:
```Java
public interface I { 
    default void show() { 
        System.out.println("I"); 
    } 
}
public interface J { 
    default void show() { 
        System.out.println("J"); 
    } 
}
public class K implements I, J { }
```
a. Will this code compile? Explain your answer. 
b. If not, how can you resolve the conflict?



3. For the given code:
```Java
public interface I { int method(); }
public interface J { String method(); }
public class C implements I, J { 
    public int method() { return 42; }
}
```
a. Will this code compile? If not, why? 
b. Can this conflict be resolved while implementing both interfaces?



4. Using generics, create a method that accepts a list of objects that implement `Comparable` and returns the maximum element from the list.

### Design Questions:

1. You're building a library for mathematical operations. You want to support addition, subtraction, multiplication, and division operations for integers, floats, and doubles.
	a. Design interfaces to represent a generic mathematical operation and specific operations (addition, subtraction, etc.). 
	b. Implement a class for each datatype (integer, float, double) that implements these operations.


2. You want to build a filtering mechanism for a list of items. Design an interface `Filter` that can be used to filter lists of different types of items (e.g., integers, strings, custom objects).
	a. How would you design the `Filter` interface? 
	b. Implement a filter that filters out even numbers from a list of integers using your interface.

### Concept Questions: 

1. Explain the difference between `Comparable` and `Comparator` in Java. When would you use one over the other?


2. In Java, what is type erasure with respect to generics? Why was it introduced, and what are its implications?


3. Consider the following code:
```Java
List<String> list = new ArrayList<>();
List<?> wildcardList = list;
```
Describe what `?` represents in the context of generics. What operations are valid on `wildcardList`?


4. Explain the difference between upper-bounded wildcards (`<? extends T>`) and lower-bounded wildcards (`<? super T>`) in Java generics. Give a scenario where each would be useful.

