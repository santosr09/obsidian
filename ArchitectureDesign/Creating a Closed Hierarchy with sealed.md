#patterns-design/closed-hierarchy #sealed
Generally in applications you have interfaces for others to implement, but interfaces you to implement internally but for others to use in general.

In Java, if you crate an interface anyone can implement it.

'Sealed classes'

Code to be very deliberate very expressive and the intetion to be very clear.

Example of sealed interfaces:

```java
public sealed interface TrafficLight {}

final class RedLight implents TrafficLight {}
final class GreenLoght implements TrafficLight {}

```

