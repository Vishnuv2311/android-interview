# How to Create a Custom Annotation in Android

In Java and Android, annotations provide metadata about the code. You can create custom annotations to add specific behaviors, enforce constraints, or generate code at compile-time.

## Steps to Create a Custom Annotation

1. **Define the Annotation**
   Create an annotation using the `@interface` keyword.
   
   ```java
   import java.lang.annotation.ElementType;
   import java.lang.annotation.Retention;
   import java.lang.annotation.RetentionPolicy;
   import java.lang.annotation.Target;

   @Retention(RetentionPolicy.RUNTIME) // Specifies if the annotation is available at runtime
   @Target(ElementType.METHOD) // Specifies the applicable element type
   public @interface LogExecutionTime {
   }
   ```

2. **Use the Annotation**
   Apply the annotation to methods, classes, or fields.

   ```java
   public class ExampleClass {
       @LogExecutionTime
       public void performTask() {
           System.out.println("Task executed");
       }
   }
   ```

3. **Process the Annotation**
   Use reflection to process the annotation at runtime.

   ```java
   import java.lang.reflect.Method;

   public class AnnotationProcessor {
       public static void main(String[] args) throws Exception {
           ExampleClass example = new ExampleClass();
           for (Method method : ExampleClass.class.getDeclaredMethods()) {
               if (method.isAnnotationPresent(LogExecutionTime.class)) {
                   long start = System.currentTimeMillis();
                   method.invoke(example);
                   long end = System.currentTimeMillis();
                   System.out.println("Execution Time: " + (end - start) + "ms");
               }
           }
       }
   }
   ```

## Conclusion
Custom annotations in Android can help in logging, validation, and code generation. They are a powerful tool for creating reusable and maintainable code.
