### Can an Interface implement another Interface?

In Java, an interface **cannot implement** another interface, but it **can extend** another interface.

- The `implements` keyword is used when a class is implementing an interface.
- The `extends` keyword is used when an interface is inheriting another interface.

#### Example:

```java
interface A {
    void methodA();
}

interface B extends A {
    void methodB();
}

class C implements B {
    public void methodA() {
        System.out.println("Method A");
    }

    public void methodB() {
        System.out.println("Method B");
    }
}
```

In the above example:
- Interface `B` extends interface `A`.
- Class `C` implements `B` and provides implementation for both `methodA()` and `methodB()`.

#### Summary:
- Interface **extends** another interface.
- Class **implements** an interface.
