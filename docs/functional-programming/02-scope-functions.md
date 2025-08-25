# 🔧 Scope Functions in Kotlin

Scope functions are a set of functions that allow you to execute a block of code within the context of an object. They provide a temporary scope where you can access the object without using its name, making your code more concise and readable.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand the five main scope functions: `let`, `run`, `with`, `apply`, and `also`
- ✅ Choose the right scope function for different use cases
- ✅ Use scope functions to make your code more readable and concise
- ✅ Understand the differences between scope functions
- ✅ Apply scope functions in real-world scenarios

## 🔍 What You'll Learn

- **Scope function types** - Understanding the five main scope functions
- **Context and return values** - How each function handles the context object
- **Use cases** - When to use each scope function
- **Best practices** - Guidelines for effective scope function usage
- **Real-world examples** - Practical applications in everyday coding

## 📝 Prerequisites

- Understanding of [Lambdas and Higher-Order Functions](01-lambdas.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Object-Oriented Programming](../oop/01-classes-constructors.md)

## 💻 The Code

Let's examine the scope functions examples:

**📁 File:** [39_with_apply_functions.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/39_with_apply_functions.kt)

## 🔍 Code Breakdown

### **1. The `let` Function**

#### **Basic Usage**
```kotlin
// let provides the object as 'it' and returns the lambda result
val name: String? = "Alice"
val length = name?.let { 
    println("Name: $it")
    it.length  // Return value
}

// Safe call with let
val nullableName: String? = null
val result = nullableName?.let { 
    "Hello, $it!" 
} ?: "Hello, Guest!"
```

#### **Chaining with let**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val result = numbers
    .filter { it % 2 == 0 }
    .let { evenNumbers ->
        println("Even numbers: $evenNumbers")
        evenNumbers.sum()
    }
```

### **2. The `run` Function**

#### **Basic Usage**
```kotlin
// run provides the object as 'this' and returns the lambda result
val person = Person("Alice", 25)
val description = person.run {
    println("Processing: $name")
    "Name: $name, Age: $age"  // Return value
}
```

#### **Extension Function Style**
```kotlin
val result = "Hello, World!".run {
    println("Original: $this")
    uppercase()
    length
}
```

#### **Non-Extension run**
```kotlin
val result = run {
    val name = "Alice"
    val age = 25
    "$name is $age years old"
}
```

### **3. The `with` Function**

#### **Basic Usage**
```kotlin
// with provides the object as 'this' and returns the lambda result
val person = Person("Bob", 30)
val description = with(person) {
    println("Name: $name")
    println("Age: $age")
    "Person: $name ($age years old)"  // Return value
}
```

#### **Multiple Operations**
```kotlin
val numbers = mutableListOf(1, 2, 3, 4, 5)
with(numbers) {
    add(6)
    add(7)
    remove(1)
    println("Size: $size")
    sum()  // Return value
}
```

### **4. The `apply` Function**

#### **Basic Usage**
```kotlin
// apply provides the object as 'this' and returns the object itself
val person = Person("Charlie", 35).apply {
    println("Setting up: $name")
    // Can modify properties if they're mutable
}

// Common use case: object configuration
val button = Button().apply {
    text = "Click Me"
    color = "Blue"
    size = 100
    onClick = { println("Button clicked!") }
}
```

#### **Builder Pattern**
```kotlin
val email = EmailBuilder().apply {
    to = "user@example.com"
    subject = "Hello"
    body = "This is a test email"
    priority = "High"
}.build()
```

### **5. The `also` Function**

#### **Basic Usage**
```kotlin
// also provides the object as 'it' and returns the object itself
val numbers = mutableListOf(1, 2, 3)
val result = numbers.also {
    println("Original list: $it")
    it.add(4)
    println("After adding 4: $it")
}
// result is the same list, not the println result
```

#### **Logging and Side Effects**
```kotlin
val person = Person("David", 40).also {
    println("Created person: ${it.name}")
    println("Age: ${it.age}")
}
```

### **6. Comparing Scope Functions**

#### **Function Comparison Table**
```kotlin
data class Person(var name: String, var age: Int)

fun demonstrateScopeFunctions() {
    val person = Person("Alice", 25)
    
    // let - returns lambda result, object as 'it'
    val letResult = person.let { 
        "Name: ${it.name}" 
    }
    
    // run - returns lambda result, object as 'this'
    val runResult = person.run { 
        "Name: $name" 
    }
    
    // with - returns lambda result, object as 'this'
    val withResult = with(person) { 
        "Name: $name" 
    }
    
    // apply - returns object, object as 'this'
    val applyResult = person.apply { 
        age = 26 
    }
    
    // also - returns object, object as 'it'
    val alsoResult = person.also { 
        println("Person: ${it.name}") 
    }
    
    println("let: $letResult")
    println("run: $runResult")
    println("with: $withResult")
    println("apply: $applyResult")
    println("also: $alsoResult")
}
```

## 🎯 Key Concepts Explained

### **1. Context Object: `this` vs `it`**
```kotlin
val person = Person("Alice", 25)

// Functions that use 'this' (run, with, apply)
person.run {
    name = "Bob"        // Direct access to properties
    age = 30
}

// Functions that use 'it' (let, also)
person.let {
    it.name = "Charlie" // Access via 'it'
    it.age = 35
}
```

### **2. Return Values**
```kotlin
val person = Person("Alice", 25)

// Functions that return lambda result
val letResult = person.let { it.name.length }      // Int
val runResult = person.run { name.length }         // Int
val withResult = with(person) { name.length }      // Int

// Functions that return the object
val applyResult = person.apply { age = 26 }        // Person
val alsoResult = person.also { println(it.name) }  // Person
```

### **3. When to Use Each Function**

#### **Use `let` when:**
- Executing a lambda on non-null values
- Introducing local variables with limited scope
- Chaining operations

#### **Use `run` when:**
- Initializing objects and computing the return value
- Executing a block of statements where an expression is needed

#### **Use `with` when:**
- Calling multiple functions on the same object
- Grouping function calls on an object

#### **Use `apply` when:**
- Configuring objects
- Setting up object properties
- Builder pattern implementations

#### **Use `also` when:**
- Adding actions that don't affect the object
- Logging or debugging
- Side effects that don't change the object

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/39_with_apply_functions.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '39_with_apply_functionsKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Person Configuration**
Create a Person class and configure it using different scope functions.

**Solution:**
```kotlin
data class Person(
    var name: String = "",
    var age: Int = 0,
    var email: String = "",
    var city: String = ""
)

fun main() {
    // Using apply for configuration
    val person1 = Person().apply {
        name = "Alice"
        age = 25
        email = "alice@email.com"
        city = "New York"
    }
    
    // Using let for safe operations
    val person2 = Person("Bob", 30, "bob@email.com", "Boston")
    val description = person2.let {
        if (it.age >= 18) {
            "Adult: ${it.name} from ${it.city}"
        } else {
            "Minor: ${it.name}"
        }
    }
    
    // Using with for multiple operations
    val person3 = Person("Charlie", 35, "charlie@email.com", "Chicago")
    val result = with(person3) {
        println("Processing: $name")
        println("Age: $age")
        println("Location: $city")
        "Processed: $name"
    }
    
    println("Person 1: $person1")
    println("Description: $description")
    println("Result: $result")
}
```

### **Exercise 2: Collection Processing**
Use scope functions to process collections in different ways.

**Solution:**
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    // Using let for chaining
    val evenSum = numbers
        .filter { it % 2 == 0 }
        .let { evenNumbers ->
            println("Even numbers: $evenNumbers")
            evenNumbers.sum()
        }
    
    // Using run for processing
    val statistics = numbers.run {
        val count = size
        val sum = sum()
        val average = sum.toDouble() / count
        val max = maxOrNull() ?: 0
        val min = minOrNull() ?: 0
        
        mapOf(
            "count" to count,
            "sum" to sum,
            "average" to average,
            "max" to max,
            "min" to min
        )
    }
    
    // Using with for multiple operations
    val processed = with(numbers) {
        val doubled = map { it * 2 }
        val filtered = doubled.filter { it > 10 }
        val sorted = filtered.sortedDescending()
        sorted.take(3)
    }
    
    println("Even sum: $evenSum")
    println("Statistics: $statistics")
    println("Processed: $processed")
}
```

### **Exercise 3: Builder Pattern**
Implement a builder pattern using scope functions.

**Solution:**
```kotlin
class HTMLBuilder {
    private val content = StringBuilder()
    
    fun tag(name: String, content: String) {
        this.content.append("<$name>$content</$name>")
    }
    
    fun tag(name: String, init: HTMLBuilder.() -> Unit) {
        this.content.append("<$name>")
        init()
        this.content.append("</$name>")
    }
    
    fun build(): String = content.toString()
}

fun html(init: HTMLBuilder.() -> Unit): String {
    return HTMLBuilder().apply(init).build()
}

fun main() {
    val htmlContent = html {
        tag("html") {
            tag("head") {
                tag("title", "My Page")
            }
            tag("body") {
                tag("h1", "Welcome")
                tag("p", "This is a paragraph")
                tag("div") {
                    tag("span", "Nested content")
                }
            }
        }
    }
    
    println(htmlContent)
}
```

### **Exercise 4: Configuration Management**
Create a configuration system using scope functions.

**Solution:**
```kotlin
data class DatabaseConfig(
    var host: String = "localhost",
    var port: Int = 5432,
    var username: String = "",
    var password: String = "",
    var database: String = ""
)

data class AppConfig(
    var name: String = "",
    var version: String = "",
    var debug: Boolean = false,
    var database: DatabaseConfig = DatabaseConfig()
)

fun createConfig(init: AppConfig.() -> Unit): AppConfig {
    return AppConfig().apply(init)
}

fun main() {
    val config = createConfig {
        name = "MyApp"
        version = "1.0.0"
        debug = true
        database.apply {
            host = "production.db.com"
            port = 5432
            username = "admin"
            password = "secret"
            database = "myapp_prod"
        }
    }
    
    // Using let for safe operations
    config.database.let { db ->
        if (db.host != "localhost") {
            println("Production database: ${db.host}:${db.port}")
        }
    }
    
    // Using with for multiple operations
    with(config) {
        println("App: $name v$version")
        println("Debug mode: $debug")
        println("Database: ${database.host}:${database.port}")
    }
    
    // Using also for logging
    config.also {
        println("Configuration created successfully")
        println("Total config size: ${it.name.length + it.version.length}")
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Overusing scope functions**: Don't use them when simple property access is clearer ✅
2. **Confusing return values**: Remember which functions return the object vs lambda result ✅
3. **Nesting scope functions**: Can make code hard to read - use sparingly ✅
4. **Ignoring context**: Choose the right function based on whether you need `this` or `it` ✅

## 🎯 What's Next?

Now that you understand scope functions, continue with:

1. **Collections** → [Collections Overview](../collections/README.md)
2. **Null Safety** → [Null Safety](../null-safety/01-null-safety.md)
3. **Coroutines** → [Coroutines](../coroutines/01-introduction.md)
4. **Advanced OOP** → [Object-Oriented Programming](../oop/README.md)

## 📚 Additional Resources

- [Official Kotlin Scope Functions Documentation](https://kotlinlang.org/docs/scope-functions.html)
- [Scope Functions Guide](https://kotlinlang.org/docs/scope-functions.html#scope-functions)
- [Kotlin Standard Library](https://kotlinlang.org/api/latest/jvm/stdlib/)

## 🏆 Summary

- ✅ You understand the five main scope functions and their differences
- ✅ You can choose the right scope function for different use cases
- ✅ You know when to use `this` vs `it` context
- ✅ You can apply scope functions to make code more readable
- ✅ You're ready to write more concise and expressive Kotlin code!

**Scope functions are powerful tools for making your code more readable and concise. Use them wisely! 🎉**
