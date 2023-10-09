
#### **Inheritance - Private Fields**


**`Point` Class**:
- Contains two private integer fields: `x` and `y`.


 **`ColoredPoint` Class**:
- Extends the `Point` class.
- Fields `x` and `y` from `Point` are inherited by `ColoredPoint`, but they remain **hidden** due to their private access modifier.
- There's an attempt to override the `getX()` method and directly access the `x` field.
- **Compilation Issue**: The code in `ColoredPoint` that tries to return `x` directly will not compile because the field `x` from `Point` is private and hidden in `ColoredPoint`.


 **Accessing Private Fields**:
- While the `x` field in the `Point` class is private and cannot be accessed directly in `ColoredPoint`, the `getX()` method (if present and public in the `Point` class) can be used to retrieve its value.
- Directly trying to access `cp.x` will result in a compilation error, but `cp.getX()` will work if `getX()` is a public method in the `Point` class.
- 
#### **Inheritance - Private Methods**

**`Supercl` Class**:

- Contains a private method `mpriv()` that prints "Supercl".
- Contains a public method `mpub()` which calls the `mpriv()` method.
- In the `main` method, creating an instance of `Supercl` and calling the `mpub()` method will print "Supercl" as a result of the `mpriv()` method being called.


 **`Subcl` Class**:

- Extends the `Supercl` class.
- While the `mpriv()` method is private in the superclass (`Supercl`), it is **not inherited** by the subclass (`Subcl`).
- The inherited `mpub()` method from `Supercl` when called on a `Subcl` object will still call the `mpriv()` method from `Supercl`.
- In the `Subcl` class, if there is another private method named `mpriv()` that prints "Subcl", it won't interfere with the inherited `mpub()`. Calling `mpub()` will still result in "Supercl" being printed, demonstrating that private methods are not overridden.

**Key Takeaways**:

- **Private methods are NOT inherited** by subclasses.
- An inherited public method from a superclass that calls a private method will still reference the superclass's private method, even if the subclass has a method with the same name.
- This behavior shows the encapsulation principle in action, where private members of a class remain private to that class and are not directly accessible or overridden by subclasses.


#### Inheritance – Static fields/methods

**Basic Inheritance of Static Fields**

- `Supercl` has a static field `x` with value 2.
- `Subcl` extends `Supercl` but doesn't declare its own `x`.
- Static fields are inherited. Thus, both `Supercl.x` and `Subcl.x` will print 2.


**Hiding Inherited Static Fields**

- `Subcl` declares its own static field `x` with value 3.
- This hides the inherited static field `x` from `Supercl`.
- `Supercl.x` will print 2 and `Subcl.x` will print 3.


**Accessing Static Fields via Instance Methods**

- `Subcl` has an instance method `getX()` which returns the static field `x`.
- Even though it's an instance method, it can access static fields.
- `Supercl.x` will print 2 and `new Subcl().getX()` will print 3.


**Instance Field with Same Name**

- `Subcl` declares an instance field `x` with value 3.
- This hides the inherited static field `x` from `Supercl`.
- Trying to access `Subcl.x` results in a compile-time error: "cannot make static reference to non-static field x".


**Static Fields are Statically Bound**

- Inherited static fields are bound to the reference type, not the instance type.
- For instance, when `Subcl subcl = new Subcl();` then `subcl.x` accesses the instance field x and will print 3.
- When `Supercl supercl = new Subcl();` then `supercl.x` accesses the static field x from `Supercl` and will print 2.


**Overriding Static Method with Another Static Method**

- Class `Sorter` has a static method `sort()`.
- Class `IllustratedSorter` extends `Sorter` and tries to "override" the static method with its own.
- It's important to note that static methods can't be overridden in the traditional sense. Instead, the method in `IllustratedSorter` hides the one in `Sorter`.
- Thus, `p.sort()` will print "simple sort" even if `p` references an `IllustratedSorter` object, because `sort()` is bound to the reference type (`Sorter`).


**Overriding a Static Method with an Instance Method**

- Trying to override a static method in `Sorter` with an instance method in `IllustratedSorter` results in a compile-time error: "Instance method cannot override static method sort from Sorter".


**Overriding an Instance Method with a Static Method**

- If `Sorter` has an instance method and `IllustratedSorter` tries to "override" it with a static method, it results in a compile-time error: "Static method cannot override instance method sort from Sorter".