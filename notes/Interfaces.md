
when implementing an interface we use `implements`


when a class implements an interface, the class MUST implement all methods within the interface and `@override` them with their own methods. 


```Java
public class Rabbit implements Prey{
	@override
	public void flee(){
		System.out.println("The rabbit flees")
	}
}

public interface Prey{
	void flee(); //every class that implements prey must have flee() method
}
```
