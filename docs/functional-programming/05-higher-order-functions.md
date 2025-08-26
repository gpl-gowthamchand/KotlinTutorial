# 🚀 Higher-Order Functions in Kotlin

Higher-order functions are a fundamental concept in functional programming that allows functions to take other functions as parameters or return functions as results. They enable powerful abstractions and make your code more flexible and reusable.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what higher-order functions are and their benefits
- ✅ Create functions that take other functions as parameters
- ✅ Build functions that return functions
- ✅ Use higher-order functions for common programming patterns
- ✅ Apply functional programming principles effectively

## 🔍 What You'll Learn

- **Higher-order function concepts** - Functions as first-class citizens
- **Function parameters** - Passing functions to other functions
- **Function returns** - Returning functions from functions
- **Common patterns** - Map, filter, reduce, and more
- **Real-world applications** - Practical examples and use cases

## 📝 Prerequisites

- Understanding of [Functions](../functions/01-functions-basics.md)
- Knowledge of [Lambdas](01-lambdas.md)
- Familiarity with [Collections](../collections/01-arrays.md)

## 💻 The Code

Let's examine higher-order functions in action:

**📁 File:** [35_lambdas_higher_order_functions.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/35_lambdas_higher_order_functions.kt)

## 🔍 Code Breakdown

### **1. Basic Higher-Order Functions**

#### **What are Higher-Order Functions?**
A higher-order function is a function that either:
- Takes one or more functions as parameters, OR
- Returns a function as its result

This makes functions "first-class citizens" in your programming language.

#### **Function as Parameter**
```kotlin
fun main() {
    // Function that takes another function as a parameter
    fun executeOperation(operation: (Int, Int) -> Int, a: Int, b: Int): Int {
        return operation(a, b)
    }
    
    // Pass lambda functions as parameters
    val result1 = executeOperation({ a, b -> a + b }, 5, 3)      // 8
    val result2 = executeOperation({ a, b -> a * b }, 4, 6)      // 24
    val result3 = executeOperation({ a, b -> a - b }, 10, 4)     // 6
    
    println("Addition: $result1")
    println("Multiplication: $result2")
    println("Subtraction: $result3")
}
```

#### **Function with No Parameters**
```kotlin
fun repeatAction(times: Int, action: () -> Unit) {
    repeat(times) {
        action()
    }
}

fun main() {
    // Pass a lambda that prints "Hello!"
    repeatAction(3) { println("Hello!") }
    
    // Pass a lambda that prints a random number
    repeatAction(2) { println("Random: ${(1..100).random()}") }
}
```

### **2. Function as Return Value**

#### **Returning Functions**
```kotlin
fun createMultiplier(factor: Int): (Int) -> Int {
    return { number -> number * factor }
}

fun createGreeter(greeting: String): (String) -> String {
    return { name -> "$greeting, $name!" }
}

fun main() {
    // Create specific multiplier functions
    val double = createMultiplier(2)
    val triple = createMultiplier(3)
    val quadruple = createMultiplier(4)
    
    println("Double of 5: ${double(5)}")        // 10
    println("Triple of 5: ${triple(5)}")        // 15
    println("Quadruple of 5: ${quadruple(5)}")  // 20
    
    // Create specific greeter functions
    val helloGreeter = createGreeter("Hello")
    val goodMorningGreeter = createGreeter("Good morning")
    
    println(helloGreeter("Alice"))           // Hello, Alice!
    println(goodMorningGreeter("Bob"))       // Good morning, Bob!
}
```

#### **Complex Function Factory**
```kotlin
fun createCalculator(operation: String): (Double, Double) -> Double {
    return when (operation) {
        "add" -> { a, b -> a + b }
        "subtract" -> { a, b -> a - b }
        "multiply" -> { a, b -> a * b }
        "divide" -> { a, b -> 
            if (b != 0.0) a / b else throw IllegalArgumentException("Division by zero")
        }
        else -> throw IllegalArgumentException("Unknown operation: $operation")
    }
}

fun main() {
    val add = createCalculator("add")
    val multiply = createCalculator("multiply")
    
    println("5 + 3 = ${add(5.0, 3.0)}")           // 8.0
    println("5 * 3 = ${multiply(5.0, 3.0)}")      // 15.0
}
```

### **3. Common Higher-Order Function Patterns**

#### **Map Pattern**
```kotlin
fun <T, R> customMap(list: List<T>, transform: (T) -> R): List<R> {
    val result = mutableListOf<R>()
    for (item in list) {
        result.add(transform(item))
    }
    return result
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    
    // Double each number
    val doubled = customMap(numbers) { it * 2 }
    println("Doubled: $doubled")  // [2, 4, 6, 8, 10]
    
    // Convert to string
    val strings = customMap(numbers) { "Number $it" }
    println("Strings: $strings")  // [Number 1, Number 2, Number 3, Number 4, Number 5]
}
```

#### **Filter Pattern**
```kotlin
fun <T> customFilter(list: List<T>, predicate: (T) -> Boolean): List<T> {
    val result = mutableListOf<T>()
    for (item in list) {
        if (predicate(item)) {
            result.add(item)
        }
    }
    return result
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    // Filter even numbers
    val evens = customFilter(numbers) { it % 2 == 0 }
    println("Even numbers: $evens")  // [2, 4, 6, 8, 10]
    
    // Filter numbers greater than 5
    val greaterThan5 = customFilter(numbers) { it > 5 }
    println("Greater than 5: $greaterThan5")  // [6, 7, 8, 9, 10]
}
```

#### **Reduce Pattern**
```kotlin
fun <T> customReduce(list: List<T>, initial: T, operation: (T, T) -> T): T {
    var result = initial
    for (item in list) {
        result = operation(result, item)
    }
    return result
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    
    // Sum all numbers
    val sum = customReduce(numbers, 0) { acc, num -> acc + num }
    println("Sum: $sum")  // 15
    
    // Find maximum
    val max = customReduce(numbers, numbers.first()) { acc, num -> 
        if (num > acc) num else acc 
    }
    println("Maximum: $max")  // 5
}
```

### **4. Advanced Higher-Order Functions**

#### **Function Composition**
```kotlin
fun <A, B, C> compose(f: (B) -> C, g: (A) -> B): (A) -> C {
    return { a -> f(g(a)) }
}

fun main() {
    val addOne = { x: Int -> x + 1 }
    val multiplyByTwo = { x: Int -> x * 2 }
    val square = { x: Int -> x * x }
    
    // Compose functions: f(g(x)) = (x + 1) * 2
    val addOneThenMultiply = compose(multiplyByTwo, addOne)
    println("addOneThenMultiply(3): ${addOneThenMultiply(3)}")  // 8
    
    // Compose multiple functions: square(addOne(multiplyByTwo(x)))
    val complexFunction = compose(square, compose(addOne, multiplyByTwo))
    println("complexFunction(2): ${complexFunction(2)}")  // 25
}
```

#### **Partial Application**
```kotlin
fun <A, B, C> partialApply(f: (A, B) -> C, a: A): (B) -> C {
    return { b -> f(a, b) }
}

fun main() {
    val add = { a: Int, b: Int -> a + b }
    
    // Partially apply the first parameter
    val addFive = partialApply(add, 5)
    println("addFive(3): ${addFive(3)}")  // 8
    println("addFive(7): ${addFive(7)}")  // 12
    
    // Create a function that always adds 10
    val addTen = partialApply(add, 10)
    println("addTen(5): ${addTen(5)}")    // 15
}
```

#### **Currying**
```kotlin
fun <A, B, C> curry(f: (A, B) -> C): (A) -> (B) -> C {
    return { a -> { b -> f(a, b) } }
}

fun main() {
    val add = { a: Int, b: Int -> a + b }
    val curriedAdd = curry(add)
    
    // Apply first parameter
    val addFive = curriedAdd(5)
    // Apply second parameter
    val result = addFive(3)
    
    println("Result: $result")  // 8
    
    // Chain the calls
    val result2 = curry(add)(5)(3)
    println("Result 2: $result2")  // 8
}
```

### **5. Real-World Examples**

#### **Event Handler System**
```kotlin
typealias EventHandler<T> = (T) -> Unit

class EventSystem<T> {
    private val handlers = mutableListOf<EventHandler<T>>()
    
    fun addHandler(handler: EventHandler<T>) {
        handlers.add(handler)
    }
    
    fun removeHandler(handler: EventHandler<T>) {
        handlers.remove(handler)
    }
    
    fun fireEvent(event: T) {
        handlers.forEach { it(event) }
    }
}

fun main() {
    val eventSystem = EventSystem<String>()
    
    // Add event handlers
    eventSystem.addHandler { event -> println("Handler 1: $event") }
    eventSystem.addHandler { event -> println("Handler 2: Processing $event") }
    eventSystem.addHandler { event -> println("Handler 3: Logging $event") }
    
    // Fire an event
    eventSystem.fireEvent("User login")
}
```

#### **Configuration Builder**
```kotlin
class ConfigurationBuilder {
    private val config = mutableMapOf<String, Any>()
    
    fun <T> set(key: String, value: T): ConfigurationBuilder {
        config[key] = value as Any
        return this
    }
    
    fun <T> get(key: String, defaultValue: T): T {
        return config[key] as? T ?: defaultValue
    }
    
    fun build(): Map<String, Any> = config.toMap()
}

fun <T> withConfig(block: ConfigurationBuilder.() -> Unit): Map<String, Any> {
    val builder = ConfigurationBuilder()
    builder.block()
    return builder.build()
}

fun main() {
    val config = withConfig {
        set("database.url", "localhost:5432")
        set("database.name", "myapp")
        set("server.port", 8080)
        set("debug.enabled", true)
    }
    
    println("Configuration: $config")
}
```

#### **Retry Mechanism**
```kotlin
fun <T> retry(
    maxAttempts: Int = 3,
    delayMs: Long = 1000,
    operation: () -> T
): T {
    var lastException: Exception? = null
    
    repeat(maxAttempts) { attempt ->
        try {
            return operation()
        } catch (e: Exception) {
            lastException = e
            if (attempt < maxAttempts - 1) {
                println("Attempt ${attempt + 1} failed: ${e.message}")
                println("Retrying in ${delayMs}ms...")
                Thread.sleep(delayMs)
            }
        }
    }
    
    throw lastException ?: RuntimeException("Operation failed after $maxAttempts attempts")
}

fun main() {
    try {
        val result = retry(maxAttempts = 3, delayMs = 500) {
            // Simulate an operation that might fail
            if (Math.random() < 0.7) {
                throw RuntimeException("Random failure")
            }
            "Success!"
        }
        println("Result: $result")
    } catch (e: Exception) {
        println("All attempts failed: ${e.message}")
    }
}
```

## 🎯 Key Concepts Explained

### **1. Function Types**

**Basic Function Types:**
```kotlin
() -> Unit                    // No parameters, no return value
(Int) -> String              // One parameter, returns String
(Int, String) -> Boolean     // Two parameters, returns Boolean
() -> Int                    // No parameters, returns Int
```

**Generic Function Types:**
```kotlin
<T> (T) -> T                // Generic parameter and return
<T, R> (T) -> R             // Generic parameter and return
<T> (List<T>) -> T          // Generic list parameter
```

### **2. Higher-Order Function Benefits**

- **Reusability**: Write once, use many times
- **Flexibility**: Change behavior without changing code
- **Composability**: Combine functions in new ways
- **Testability**: Easier to test individual components
- **Readability**: More expressive and declarative code

### **3. When to Use Higher-Order Functions**

**Use Higher-Order Functions when:**
- You have common patterns that differ only in behavior
- You want to make your code more flexible
- You're implementing callback mechanisms
- You need to compose or combine functions
- You want to implement functional programming patterns

**Don't Use Higher-Order Functions when:**
- The logic is simple and straightforward
- Performance is critical (function calls have overhead)
- The code becomes harder to understand
- You're over-engineering a simple solution

## 🚀 Advanced Patterns

### **1. Monadic Operations**
```kotlin
sealed class Result<out T> {
    data class Success<T>(val value: T) : Result<T>()
    data class Error(val message: String) : Result<Nothing>()
}

fun <T, R> Result<T>.map(transform: (T) -> R): Result<R> {
    return when (this) {
        is Result.Success -> Result.Success(transform(value))
        is Result.Error -> Result.Error(message)
    }
}

fun <T, R> Result<T>.flatMap(transform: (T) -> Result<R>): Result<R> {
    return when (this) {
        is Result.Success -> transform(value)
        is Result.Error -> Result.Error(message)
    }
}
```

### **2. Builder Pattern with Functions**
```kotlin
class HTMLBuilder {
    private val content = StringBuilder()
    
    fun tag(name: String, block: HTMLBuilder.() -> Unit) {
        content.append("<$name>")
        block()
        content.append("</$name>")
    }
    
    fun text(text: String) {
        content.append(text)
    }
    
    fun build(): String = content.toString()
}

fun html(block: HTMLBuilder.() -> Unit): String {
    val builder = HTMLBuilder()
    builder.block()
    return builder.build()
}

fun main() {
    val htmlContent = html {
        tag("html") {
            tag("body") {
                tag("h1") {
                    text("Hello, World!")
                }
                tag("p") {
                    text("This is a paragraph.")
                }
            }
        }
    }
    
    println(htmlContent)
}
```

## 💡 Best Practices

### **1. Function Naming**
- Use descriptive names for function parameters
- Name functions that return functions clearly
- Use type aliases for complex function types

### **2. Performance Considerations**
- Be aware of function call overhead
- Use inline functions when appropriate
- Consider caching frequently used functions

### **3. Error Handling**
- Handle exceptions in higher-order functions
- Provide meaningful error messages
- Use Result types for functional error handling

## 🔧 Common Pitfalls

### **1. Function Call Overhead**
```kotlin
// ❌ Wrong - Unnecessary function calls
fun processList(list: List<Int>): List<Int> {
    return list.map { it * 2 }
        .filter { it > 5 }
        .map { it + 1 }
}

// ✅ Better - Single pass when possible
fun processListOptimized(list: List<Int>): List<Int> {
    return list.mapNotNull { 
        val doubled = it * 2
        if (doubled > 5) doubled + 1 else null
    }
}
```

### **2. Capturing Variables**
```kotlin
// ❌ Wrong - Capturing mutable variables
fun createCounter(): () -> Int {
    var count = 0
    return { count++ }  // Captures mutable variable
}

// ✅ Better - Use immutable state
fun createCounter(): () -> Int {
    var count = 0
    return { 
        count += 1
        count 
    }
}
```

### **3. Complex Function Types**
```kotlin
// ❌ Wrong - Hard to read complex types
fun process(f: ((Int) -> String) -> (String) -> Boolean): Boolean {
    return f({ it.toString() })("test")
}

// ✅ Better - Use type aliases
typealias IntToString = (Int) -> String
typealias StringToBoolean = (String) -> Boolean
typealias FunctionProcessor = (IntToString) -> StringToBoolean

fun process(f: FunctionProcessor): Boolean {
    return f({ it.toString() })("test")
}
```

## 📚 Summary

Higher-order functions are powerful tools that enable:
- **Function composition and combination**
- **Flexible and reusable code patterns**
- **Functional programming paradigms**
- **Cleaner, more expressive code**

## 🎯 Practice Exercises

1. **Custom Collection Operations**: Implement your own map, filter, and reduce functions
2. **Function Composition**: Create a system for composing multiple functions
3. **Event System**: Build an event handling system using higher-order functions
4. **Configuration Builder**: Create a fluent configuration builder with function parameters

## 🔗 Related Topics

- [Lambdas](01-lambdas.md) - Anonymous functions
- [Functions Basics](../functions/01-functions-basics.md) - Function fundamentals
- [Collections](../collections/01-arrays.md) - Data structures
- [Functional Programming](01-lambdas.md) - Functional concepts

## 📖 Additional Resources

- [Official Kotlin Functions Documentation](https://kotlinlang.org/docs/functions.html)
- [Higher-Order Functions](https://kotlinlang.org/docs/lambdas.html#higher-order-functions)
- [Function Types](https://kotlinlang.org/docs/lambdas.html#function-types)

---

**Next Lesson**: [Closures](06-closures.md) - Learn about closure concepts in Kotlin

**Happy coding with Higher-Order Functions! 🚀**
