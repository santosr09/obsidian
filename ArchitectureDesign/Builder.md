## Tags: 
#patterns-design/static-factory-methods #patterns-design/creational
-

## Related Ideas [[]]
## Source [[]]
-
Consider a builder when faced with many constructor parameters
Static factories method [[static factory methods]] and constructors share a limitation: they **do not scale well to large numbers of optional parameters**.

The telescoping constructor pattern works, but it is hard to write client code when there are many parameters, and harder still to read it.

**JavaBeans Pattern** in which you call a parameterless constructor to create the object and then call setter methods to set each required parameter and each optional parameter of interest. But this has serious disadvantages of its own because construction is split across multiple calls, a JavaBean may be in an inconsistent state partway through its construction.
The JavaBean pattern precludes the possiblity of making a class immutable.

Builder combines the safety ot the telescoping constructor pattern with the readability of the JavaBeans pattern. Instead of making the desired object directly, the client calls a constructor(or [[static factory methods]]) with all the required parameters and **gets** a *builder object*.  Then the client calls setter-like methods on the builder object to set each optional parameter of interest. Finally the client calls a parameterless ==**build**== method to generate the object, which is tipically **[[Immutable]]**

Th builder is tipically a static member class of the class it builds.

```java
// Builder Pattern
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // Required parameters
        private final int servingSize;
        private final int servings;

        // Optional parameters - initialized to default values
        private int calories      = 0;
        private int fat           = 0;
        private int sodium        = 0;
        private int carbohydrate  = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val)
            { calories = val;      return this; }
        public Builder fat(int val)
            { fat = val;           return this; }
        public Builder sodium(int val)
            { sodium = val;        return this; }
        public Builder carbohydrate(int val)
            { carbohydrate = val;  return this; }

        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
```

The **NutritionFacts class is immutable**, and all parameter default values are in one place. The builder’s setter methods return the builder itself so that invocations can be chained, resulting in a *fluent API*. Here’s how the client code looks:

```java
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
        .calories(100).sodium(35).carbohydrate(27).build();
```

To detect invalid parameters as soon as possible, check [[parameter validity]] in the builder’s constructor and methods.
Check [[invariants]] involving multiple parameters in the constructor invoked by the build method. To ensure these invariants against attack, do the checks on object fields after copying parameters from the builder([[Defensive copy]]). If a check fails, throw an IllegalArgumentException whose detail message indicates which parameters are invalid.

The Builder pattern is well suited to class hierarchies. Use a parallel hierarchy of builders, each nested in the corresponding class. Abstract classes have abstract builders; concrete classes have concrete builders.

==Disadvantages== 
In order to create an object, you must first create its builder. While the cost of creating this builder is unlikely to be noticeable in practice, it could be a problem in performance critical situations. Also, the builder pattern is more verbose than the telescoping constructor.


