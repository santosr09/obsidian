A simple static method that returns an instance of the class
* Unlike constructors they have names
* Unlike constructors they are not required to create NEW objects each time they're invoked
* _intance controlled_ gurantee that is a singleton or noninstantiable, [[Immutable]] value class.
* Unlike constructors they can return an object of any subtype of their return type
* The class of the returned object can vary from call to call as a function of the input parameters. Any subtype of the declared return is permissible. The class of the returned object can also vary from release to release.
* The class of the returned object need not exist when the class containing the method is written
Such flexible static factory methods form the basis of [[service provider framework]], like the Java Database Connectivity API (JDBC).

==Limitations==
* The main **limitation** of providing only static factory methods is that classes without public or protected constructors **cannot be subclassed**.
* They are hard for programmers to find.

==Examples==
*from* - A type conversion method that takes a single parameter and returns a corresponding instance of this type, for example:
```java
Date d = Date.from(instant);
```

*of*  - An aggregation method that takes multiple parameters and returns an instance of this type that incorporates them, for example:
```java
Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
```

*valueOf* - A more verbose alternative to from and of, for example:
```java
BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
```

*instance* or *getInstance* — Returns an instance that is described by its parameters (if any) but cannot be said to have the same value, for example:
```java
StackWalker luke = StackWalker.getInstance(options);
```

