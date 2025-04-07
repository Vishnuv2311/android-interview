# SOLID Principles

The SOLID principles are a set of five design principles intended to make software designs more understandable, flexible, and maintainable.

---

## “S” - Single Responsibility Principle (SRP)

A class should have only one reason to change, meaning it should have only one responsibility.

**Example:**  
A `UserManager` class should handle only user-related operations. Logging activities should be handled by a separate `Logger` class.

---

## “O” - Open/Closed Principle (OCP)

Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.

**Example:**  
Instead of modifying an existing class to add new functionality, extend it using inheritance or composition. This ensures existing code is not broken.

---

## “L” - Liskov Substitution Principle (LSP)

Subtypes must be substitutable for their base types without affecting the correctness of the program.

**Example:**  
If a class `Bird` has a `fly()` method, then class `Penguin` (a subtype that can't fly) should not inherit `Bird` with `fly()` — instead, restructure the inheritance.

---

## “I” - Interface Segregation Principle (ISP)

Clients should not be forced to implement interfaces they do not use.

**Example:**  
Instead of a bulky interface like `Worker` with methods `code()`, `test()`, `design()`, split it into smaller interfaces like `Coder`, `Tester`, and `Designer`.

---

## “D” - Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Example:**  
A class should depend on an interface like `DatabaseService` rather than directly depending on `MySQLDatabase` or `SQLiteDatabase`. This makes it easier to swap implementations.
