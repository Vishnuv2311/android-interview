In Java, objects are passed by value, but it is important to understand what this means in the context of object references.

When you pass an object to a method, you are actually passing the value of the reference to that object, not the actual object itself. This means that the method receives a copy of the reference, which still points to the same object in memory. As a result, changes made to the object's fields inside the method will affect the original object. However, if you reassign the reference inside the method, it will not affect the original reference outside the method.

### Example:
```java
class Example {
    public static void modifyObject(MyObject obj) {
        obj.value = 10; // This changes the original object's field
        obj = new MyObject(); // This reassigns the local reference, not the original reference
        obj.value = 20; // This does not affect the original object
    }

    public static void main(String[] args) {
        MyObject myObj = new MyObject();
        myObj.value = 5;

        modifyObject(myObj);

        System.out.println(myObj.value); // Output will be 10
    }
}

class MyObject {
    int value;
}
```

### Key Points:
1. Java always passes arguments by value.
2. For objects, the value passed is the reference to the object.
3. Modifying the object's fields inside a method affects the original object.
4. Reassigning the reference inside a method does not affect the original reference.
