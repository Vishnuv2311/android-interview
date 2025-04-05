# How do you create a custom task in Gradle?

In Gradle, custom tasks can be created using either the Groovy DSL or Kotlin DSL. Here's how you can create a custom task using Groovy DSL:

```groovy
task myCustomTask {
    doLast {
        println 'Running my custom task!'
    }
}
```

You can run this task from the command line using:
```
./gradlew myCustomTask
```

### Creating a Task with a Type

You can also define a task with a specific type:

```groovy
task copyFiles(type: Copy) {
    from 'src'
    into 'dest'
}
```

### Registering a Task (Recommended in Kotlin DSL)

Using Kotlin DSL:

```kotlin
tasks.register("myCustomTask") {
    doLast {
        println("Running my custom task!")
    }
}
```

This approach is more idiomatic and avoids eager task configuration.

### Custom Task Class

You can define your own custom task class as well:

```groovy
class GreetingTask extends DefaultTask {
    @TaskAction
    def greet() {
        println 'Hello from custom task class!'
    }
}

task hello(type: GreetingTask)
```

### Use Cases for Custom Tasks
- Custom build logic
- File manipulation (copy, move, delete)
- Generating source code
- Running external tools or scripts

Custom tasks help you extend Gradle's functionality to fit the specific needs of your project.
