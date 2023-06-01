ARM - Automatic Resource Management
or Try-with-resources (implements Autoclosable)

Because there's a piece of code that's executed before on a piece of code that is executed after 

Execute Around Method:  with a before and after part.
This is more of a civilized AOP

class Resource {
  private Resource () { sout("created...");}
  public Resource op1() {
    sout("op1...");
    return this;
  }
  public Resource op2() {
    sout("op2...");
    return this;
  }
  private void close() {
    sout("release external resource");
  }
public static void use(Consumer<Resource> block) {
  Resource resource = new Resource();  //This is the BEFORE part
  try{
    block.accept(resource);
  } finally {
    resource.close(); // This is the AFTER part
  }
}
}

public class Sample {
  public static void main(String[] args) {
    Resource.use(resource ->
      resource.op1()
        .op2());
  }
}

You cannot forget and used it in a different way, this forces you to go in a certain path

Example to managing transactions:
  Transaction.runInTransaction(tx -> ...);
