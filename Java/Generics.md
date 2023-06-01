
## Tags:  #java/generics
# Generics

With generics you tell the compiler wath types of objects are permitted in each collection.

## Don't use Raw types
Generic classes and interfaces are collectively known as generic types.
Each generic types defines a set of  parameterized types: **List\<E\>**

```
Parameterized: List<String>
Raw type: List
```

*Discover errors as soon as possible after they are made,  ideally at compile time*

*If you use raw types, you lose all the safety and expressivness benefits of generics.

You lose type safety if you use a raw type such as List, but not if you use a parameterized type such as List\<Object\>.

==Unbounded wildcard type -> ? ==
```
	Example: List<''?''>
```
but the wildcard type is safe and the raw type isn’t. You can put any element into a collection with a raw type, easily corrupting the collection’s type invariant
you can't put any element (other than null) into a Collection

|Term| Example|Item|
|----|--------|-----|
|Parameterized type|List\<String\>|Item 26|
|Actual type parameter|String|Item 26|
|Generic type|List\<E\>|Items 26, 29|
|Formal type parameter|E|Item 26|
|Unbounded wildcard type|List\<?\>|Item 26|
|Raw type|List|Item 26|
|Bounded type parameter|\<E extends Number\>|Item 29|

## Related Ideas [[]]
## Source [[Effective Java, 3rd Edition]]
-



 