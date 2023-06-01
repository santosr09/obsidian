Delegating responsability to code

Lazy evaluation is to functional programming as polymorphism is to object-oriented programming

Laziness is implemented in streams. (or libraries like vaver)

Eager evaluation is when the function is called when is invoked, it doesn't wait to see if if you're actually going to use the result eventually or not.

Eager evaluation is the default behaivor in languages like Java

David Wheeler:
In CS(Computer Scince) we can solve almost any problem by introducing one more level of indirection.

In procedural code, pointers given the power of indirection.
In OO code, overriding functions given the power of indirection(The functions will be called on ral object at runtime).

In FP, lambdas give the power of indirection. (Postpone a call until you no longer can postpone it)

When a Lambda is given to you: 
* you could call the lambda right away, 
* or you can take the Lambda and save it for later a call,
* or you could throw it away  not use it at all,
* or you can pass the Lambda to another function.

---
myFunction1(Type value) - Eager evaluation.
myFunction2(Supplier<Type> supplier) - lazy evaluation
---

Differeing evaluation to another time.

Ask these quetions:
Do I really want to be evaluated now or ?
Do I want to postpone the evaluation until the point I really need it ?


*When do we pass value vs. a functional interface to a method?

*One consideration is Lazy evaluation*

