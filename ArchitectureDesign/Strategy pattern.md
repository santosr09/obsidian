Venkat Subramaniam 
We want to vary a small part of an algorithm while keeping the rest of the algorithm the same.
Language design is program design.
Design patterns often kick in to fill the gaps of a programming language.

A more power a language is, the less we talk about design patterns as these naturally become the features of the language.

Strategy in the past:
We created an interface and then a bunch of classes then wire them together  often use factories.

Lambdas are lightweigth strategies

Strategies are often a single method or function.
Inner classes as wrapping classes for methods(withouth any reason)
Functional interfaces and lambdas work really well.
Strategies are stateless

# Strategy
Stratregy defines a family of algorithms, encapsulates each one, and made them interchangeable.
Strategy lets the algorithm vary independently from clients that use it.

==**Identify the aspects of your application that vary and separate them from what
stays the same**==

Take the parts that vary and encapsulate them, so that later you can alter or extends the parts that vary withouth affecting those that don't.

**Program to an interface, not an implementation (Program to a supertype)**

HAS-A can be better than IS-A

**Favor composition over inheritance**
