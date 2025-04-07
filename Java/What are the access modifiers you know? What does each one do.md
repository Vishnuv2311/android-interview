# Access Modifiers in Java

Access modifiers in Java determine the visibility and accessibility of classes, methods, and variables. The four main access modifiers are:

## 1. **public**
- Accessible from any other class or package.
- There are no restrictions on the visibility.
- Used when you want your code to be accessible everywhere.

**Example:**
```java
public class MyClass {
    public void myMethod() {
        // accessible from anywhere
    }
}
```

## 2. **protected**
- Accessible within the same package and by subclasses (even if they are in different packages).
- Commonly used in inheritance scenarios.

**Example:**
```java
class MyClass {
    protected void myMethod() {
        // accessible within package and subclasses
    }
}
```

## 3. **default (package-private)**
- If no access modifier is specified, the member has default access.
- Accessible only within the same package.
- Not accessible from classes in different packages.

**Example:**
```java
class MyClass {
    void myMethod() {
        // package-private access
    }
}
```

## 4. **private**
- Accessible only within the same class.
- Provides the highest level of encapsulation.

**Example:**
```java
class MyClass {
    private void myMethod() {
        // accessible only within MyClass
    }
}
```

## Summary Table

| Modifier    | Same Class | Same Package | Subclass | Other Packages |
|-------------|------------|--------------|----------|----------------|
| public      | Yes        | Yes          | Yes      | Yes            |
| protected   | Yes        | Yes          | Yes      | No             |
| default     | Yes        | Yes          | No       | No             |
| private     | Yes        | No           | No       | No             |
