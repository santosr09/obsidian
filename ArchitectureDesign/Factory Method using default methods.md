Interfaces cannot carry state, Abstract classes can carry state.
Interfaces cannot have non final fields.

Abstract Factory vs. Factory Method

Factory Method: A class or an interface relies on a derived class to provide the implementation whereas the base provides the common behavior

Factory method uses inheritance as a design tool.
Interfaces and default method fit into Factory methods.

```java

interface Person {
  Pet getPet();   //Factory method to get Field, interfaces cannot contains instance fields
  default void play() {
    System.out.println("Playing with " + getPet());
  }
}

class Dog Person implements Person {
  private Dog dog  = new Dog();
- public Pet getPet() { return dog;}
}

class CarLover implements Person {
  private Cat cat = new Cat();
  public Pet getPet() { return cat; }
}

public class Sample {
  public static void call(Person person){
    person.play();
  }
public static void main(String args[]) {
  call(new DogPerson());
  call(new CatLover());
}
}
```

Think of interfaces as Factory methods
Pulls the data from the derived class.

Abstract Factory use Delegation as a design tool.
Factory uses inheritance, you don't have an extra object.