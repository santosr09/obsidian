Cascade method pattern(like a builder pattern)
cascading through

```java
class Mailer {
  private Mailer() {}
  public Mailer from(String addr) { sout.("from..."); return this; }
  public Mailer to(String addr) { sout.("to.."); return this; }
  public Mailer subject(String line) { sout.("subject..."); return this; }
  public Mailer body(String content) { sout.("body..."); return this; }

  public static void send(Consumer<Mailer> block) {
    var mailer = new Mailer();
    block.accept(mailer);
    sout.("sending...");
  }
}

public class Sample {
  public static void main(String[] args) {
    Mailer.send(mailer -> 
    mailer
      .from("youremail@email.com")
      .to("receiver@mail.com")
      .subject("Your code sucks")
      .body("...details..."));
  }
}

```



