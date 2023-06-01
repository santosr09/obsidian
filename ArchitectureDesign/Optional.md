NULL is a smell
Avoid null in the code
A good design reads like a story and not like a puzzle
Make the obvious
Effective Java: Collections: Do not return Null, instead return an empty collection.
Single Value: We should return Optional<T>
You don't need to do null check, the code force you to avoid Null
Optional make Code safer
Don't do this: result.get() //Optional.get() doesn't reveal its intetations, Will blowUp if not present, throwing a Null.
If you need to use get(), insetad use result.orThrow()

Instead use: result.orElse("not found")
Removing surprise for the programmers

If a method will always have a single value as a result, DONOT use Optional (Reveal intentions)
If a method may or MAY not have a single value as a result then use Optional.
If the result is a Collection, then Don't use Optional. (You can return an Empty Collection)

A good design has EMPATHY:
How will they feel using your code, it will be fun or punishment

Don't use Optional<T> as a parameter to methods
If needed, instead use overloading:
static void setName();
static void setName(string name);

There is little reason to use Optional as a field.
The purpose of Optional is to unadvertanly end up with a runtime Exception
Return Optional only when the object mwy or may not exist, and don't use it as a Parameter

Being a Paranoid - Anti-pattern
Check for Null in every single parameter they received
