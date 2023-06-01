Functions are composable

```java
public class Sample {
  public static void print(int number, String message, Function<Integer, Integer> func) {
    System.out.println(number + " " + message + ": " + func.apply(number));
  }
  public static void main(String args[]) {
    Function<Integer, Integer> inc = value -> value +1;
    Function<Integer, Integer> double = value -> value * 2 ;
    
    print(5, "incremented", inc);
    print(5, "doubled", doubled);
    
    print(5, "incremented and doubled", inc.andThen(doubled)) //Function composition
   
  }
}
```

Function composition:
inc --->| inc | ---->
doubled ----> | doubled | ---->

combined ---->| ---->| inc | ---->| doubled | ---->| ---->


Combining functions together.

Example of Decorator using Lambdas:

```java
class Camera {
  private Function<Color, Color> filter;

  public Camera(Function<Color, Color>... filters) {
    filter = Stream.of(filters)
      .reduce(Function.identity(), Function::andThen);
  }
public Color snap(Color input) {
  return filter.apply(input);
}
}

public class Sample {
  public static void print(Camera camera) {
    System.out.println(camera.snap(new Color(125, 125, 125)));
  }
  public static void main(String[] args) {
    print(new Camera());
    print(new Camera(Color::brighter));
    print(new Camera(Color::darker));
    print(new Camera(Color::brighter, Color::darker)); //Chaining, Decorating with different behaivors
  }
}
```

Pass Lambdas instead creating a herarchy of classes that becomes a lot easier to work.
