Sonar squid: S2696

Correctly updating a `**static**` field from a non-static method is tricky to get right and could easily lead to bugs if there are multiple class instances and/or **multiple threads** in play. Ideally, **`static`** fields are only updated from **`synchronized static`** methods.

This rule raises an issue each time a `static` field is updated from a non-static method.



## Noncompliant Code Example

```java
public class MyClass {

  private static int count = 0;

  public void doSomething() {
    //...
    count++;  // Noncompliant
  }
}
```

## Compliant Code Example