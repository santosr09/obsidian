Iterator pattern
In FUNCTIONAL programming we Don't have statements, we have expressions.

names.stream()
	.filter(name -> name.length() == 4)
	.map(String::UpperCase)
	.limit(2)
	//.takeWhile(predicate)
	.forEach(name -> result2.add(name)) //BAD IDEA
limit()  and takeWhile() are the functional equivalent of break from the imperative style.

I quit saying "code works"
I often now say "the code behaves"

Anti-pattern: SHARED MUTABILITY
var reults = new ArrayList<String>();
names.stream()
	.filter(name -> name.length() == 4)
	.map(String::UpperCase)
	.forEach(name -> result2.add(name)) //BAD IDEA
The functional pipeline is *not* pure, we are doing shared mutability

Functional pipeline offers internal iterators: 
is less complex
easy to modify
easy to understand
but... it is very important that we make the functional pipeline pure. Avoid shared mutable variables.

What is a pure function:
A pure function is indempotent, it returns the same result for the same input and does not have any side-effects.
1. It does not change any state that is visible outside
2. It does not depend on anything outside that may possible change.

Functional programming relies on lazy evaluation for efficiency.
Lazy evaluation and parallel execution rely on immutability and purity of functions for correctness.
FP emphasizes immutability and purity, not because it is fashionable, but because it is essential to it survival.
