# Defensive copy
Tags: #java/immutability

You must program defensively, with the assumption that clients of your class will do their best to destroy its [[invariants]].

While it is impossible for another class to modify an object’s internal state without some assistance from the object, it is surprisingly easy to provide such assistance without meaning to do so
}
```java
**// Broken "immutable" time period class**
public final class Period {
    private final Date start;
    private final Date end;

    /**
     * @param  start the beginning of the period
     * @param  end the end of the period; must not precede start
     * @throws IllegalArgumentException if start is after end
     * @throws NullPointerException if start or end is null
     */
    public Period(Date start, Date end) {
        if (start.compareTo(end) > 0)
            throw new IllegalArgumentException(
                start + " after " + end);
        this.start = start;
        this.end   = end;
    }

    public Date start() {
        return start;
    }

    public Date end() {
        return end;
    }

    ...    // Remainder omitted
}
```

It is, however, easy to violate this invariant by exploiting the fact that **Date is mutable**:

```java
// Attack the internals of a Period instance
Date start = new Date();
Date end = new Date();
Period p = new Period(start, end);
end.setYear(78);  // Modifies internals of p!
```

As of Java 8, the obvious way to fix this problem is to use `Instant` (or `Local-DateTime` or `ZonedDateTime`) in place of a `Date` because `Instant` (and the other `java.time` classes) are [[Immutable]]  **Date** **is obsolete and should no longer be used in new code.** That said, the problem still exists: there are times when you’ll have to use mutable value types in your APIs and internal representations, and the techniques discussed in this item are appropriate for those times.

To protect the internals of a Period instance from this sort of attack, **it is essential to make a defensive copy of each mutable parameter to the constructor** and to use the copies as components of the Period instance in place of the originals:

```java
// Repaired constructor - makes defensive copies of parameters
public Period(Date start, Date end) {
    this.start = new Date(start.getTime());
    this.end   = new Date(end.getTime());

    if (this.start.compareTo(this.end) > 0)
      throw new IllegalArgumentException(
          this.start + " after " + this.end);
}
```

Note that **defensive copies are made before checking the validity of the parameters, and the validity check is performed on the copies rather than the originals**.
This protects the class against changes to the parameters from another thread during the *window of vulnerability* between the time the parameters are checked and the time are copied; known as a **time-of-check/time-of-use** or **TOCTOU attack**.

We did not use Date's **clone** method to make the defensive copies. Because **Date** is nonfinal, the **clone** method is not guaranteed to return an object whose class is **java.util.Date** it could return an instance of an unstrusted subclass that is specifically designed for malicious mischief. 
To Prevent this sort of attack, **do not use the ==clone==  mehod to make a defensive copy of a parameter whose type is subclassable by untrusted parties.** 

It is still possible to mutate, because its accesors offer access to its mutable internals

```java
**// Second attack on the internals of a Period instance**
Date start = new Date();
Date end = new Date();
Period p = new Period(start, end);
p.end().setYear(78);  **// Modifies internals of p!**
```

To defend againts the second attack, merely modify the accesors to **return defensive copies of mutable internal fields**

```java
**// Repaired accessors - make defensive copies of internal fields**
public Date start() {
    return new Date(start.getTime());
}

public Date end() {
    return new Date(end.getTime());
}
```


if a class has mutable components that it gets from or returns to its clients, the class must defensively copy these components. If the cost of the copy would be prohibitive and the class trusts its clients not to modify the components inappropriately, then the defensive copy may be replaced by documentation outlining the client’s responsibility not to modify the affected components

## Related Ideas [[]]
## Source [[Effective Java, 3rd Edition]]