
Constructors do NOT create an object, they only initialize it. We use `Object o = new Object` to create. 
	When created, the fields of the object are initialized to default values, (`NULL, 0,`)


`public class Point { }`
Will it compile?
	Yes, even though there is no visible constructor, the compiler throws in a default constructor like this:
```Java
public class Point{
	public Point(){ } // <- constructor
	}
```

Given this definition of a Point class:
```Java
public class Point { 
	int x,y; 
	public Point(int x, int y) { 
		this.x = x; this.y = y; 
	} 
}
```

Will this statement compile: `Point p = new Point();`

No, because we already assigned a constructor to class `Point()` therefore the default no args constructor does not exist here.

A program can have multiple constructors (as per rules of overloaded methods). If two constructors that pass same amt of arg of same type exist it will not compile. 

---

#### Super / Sub Classes


We use `extends` to mark super/sub relationship. 

Example: 
```Java
public class Point {  
	int x,y;
}
public class ColoredPoint extends Point{
	int x,y;
}
```

`Point p = new Point();` Works
`ColoredPoint cp =  new ColoredPoint();` Works
`ColoredPoint cp = new Point()` works 




```Java
public class Point {  
	int x,y;  
	public Point(int x, int y) {  
		this.x = x; this.y = y;  
	}  
}
```

Creating an object, `Point p = new Point(3,4);` Works 

```Java
public class ColoredPoint extends Point {

}
```

This is ACTUALLY: 

```Java
public class ColoredPoint extends Point {
	//int x,y;
	//public ColoredPoint(){
		//super();
	//}
```

Problem here is that `Point` already has a constructor, therefore a default no-args constructor is not generated. This will not compile.

Note:
	A default constructor will ALWAYS call the superclass no-args constructor

To fix this: 
```Java
public class ColoredPoint extends Point {  
	//int x,y; (hidden)  
	String color;  
	public ColoredPoint(int x, int y, String color) {  
		super(x,y);  
		this.color = color
	}
}
```

This manually makes a call to `super()` with two arguments `x` and `y`. Now, when we call the constructor in the super class, it will pass both args and will now be valid. 



When a `ColoredPoint` instance is created, is an inner `Point` instance created as well?

No. It's code reuse not instance reuse. 

reusing `super()` is good programming practice. 


```Java
public class PointApp {  
	public static void  
	main(String[] args) {
		Point p1 = new Point(2,3);  
	}
```

The static type is declared at the beginning of an object creation: `Point p1.....`

As far as the compiler is concerned, the type of `p1` is `Point`. 

The dynamic type of a variable is what it points: `new Point(2,3)`. Dynamic type is the name of the class that is used with new. So dynamic type of p1 is also `Point`

Static -> Compile-Time Type                                            Dynamic -> Run-Time Type


```Java
public class PointApp {  
	public static void  
	main(String[] args) {  
	
		Point p1 = new Point(2,3);  
		// static and dynamic type of p1 is Point  
		ColoredPoint p2 = new ColoredPoint(4,5,”blue”);  
		// static and dynamic type of p2 is ColoredPoint  
		Point p3 = new ColoredPoint(2,3,”red”);
		// static type of p2 is Point  
		// dynamic type of p3 is ColoredPoint  
}
```

Every `ColoredPoint`(sub) is a `Point` (super). 

---

#### Dynamic Binding

```Java
package geometry;  
public class ColoredPoint  
extends Point {  
	//int x,y; (hidden)  
	String color;  
	public ColoredPoint(int x, int y, String color) {  
		super(x,y);  
		this.color = color;  
	}  
	
//public int getX() { return x; }  (hidden) 
//public int getY() { return y; }  (hidden) 
	public String toString() {  
		return x + “,” + y + "," + color;  
		//     return super.toString() + "," + color;
	}  
}
```

`return super.toString() + "," + color;`

Reusing inherited method code in overriding is good programming practice

`ColoredPoint p4 = new Point(5,6);`  will NOT work. a `Point` *instance* cannot be referenced by a `ColorPoint` variable. (remember, all Points are ColorPoints but not all ColorPoints are Points)

---


```Java
public class Point {  
	private int x,y;  
	...  
}  
public class ColoredPoint extends Point {  
	// x and y inherited but HIDDEN
	public int getX() { // override inherited getX()  
		return x;  
	}  
}
```

Will `return x;` compile? 

No because `int x` was declared `private` so it is hidden outside of it's class

x and y are inherited but HIDDEN

`getX()` is not overridden. 

Differences: 
`System.out.println(cp.x);` will not compile. x is private

instead use a method inside the class that has private x to access it's value:
`System.out.println(cp.getX());`

Note:
	Private methods are NOT inherited!


```Java
// Superclass
public class SuperClass {
    private void privateMethod() {
        System.out.println("Called from SuperClass");
    }
    
    public void publicMethod() {
        privateMethod();
    }
}

// Subclass
public class SubClass extends SuperClass {
    // Note: We can't override privateMethod() because it's private in SuperClass.
}

// Main Execution
public static void main(String[] args) {
    SubClass obj = new SubClass();
    obj.publicMethod();  // Output: Called from SuperClass
}
```

If we were to call `obj.privateMethod();` directly, it would not compile since `privateMethod()` is private. Similar to before, use a method call inside the same class to access `privateMethod()`

##### Static

Static fields are inherited


```Java
public class Supercl {  
	static int x=2;  
}
```
```Java
public class Subcl extends Supercl {  
	static int x=3;  
	public int getX() {  
		return x;
	}
}
```
`System.out.println(Supercl.x);` Outputs 2
`System.out.println(Subcl.x);` Outputs 3

- Static field `x` inherited from `Supercl` is HIDDEN

tl;dr: static field called in sub, sub's value is used even if super is called. 

`System.out.println(new Subcl().getX());` Outputs 3

```Java
public class Supercl {  
	static int x=2;  
}
```
```Java
public class Subcl extends Supercl {  
	int x=3;  
}
```

`System.out.println(Subcl.x);` does not compile. 

- the `x` in `Supercl` is static, meaning it belongs to the class itself and not to any instance of the class.
- the variable `x` in `Subcl` is an instance variable (non static) meaning it belongs to instances of `Subcl` not to the class itself. 

```Java
public static int getX() {  
return x;  
}
```

will not compile because of static reference to nonstatic field 


```Java
public class Supercl {  
	static int x=2;  
}
```
```Java
public class Subcl extends Supercl {  
	int x=3;  
}
```


`Supercl supercl = new Subcl();`
^static                             ^dynamic type 

Inherited static fields are statically bound (to reference/declared type), NOT dynamically bound (to instance type)

thus when we print `System.out.println(supercl.x);` we get 2


