# 🔒 Closures in Kotlin

Closures are a powerful concept in functional programming where a function captures and remembers the environment in which it was created. In Kotlin, closures allow lambda expressions and anonymous functions to access variables from their enclosing scope, even after the original scope has finished executing.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what closures are and how they work
- ✅ Create closures that capture variables from outer scopes
- ✅ Use closures for state management and data encapsulation
- ✅ Understand closure memory management and performance implications
- ✅ Apply closures in real-world scenarios effectively

## 🔍 What You'll Learn

- **Closure fundamentals** - What closures are and how they work
- **Variable capture** - How closures capture variables from outer scopes
- **State management** - Using closures to maintain state
- **Memory considerations** - Understanding closure memory management
- **Practical applications** - Real-world use cases and examples

## 📝 Prerequisites

- Understanding of [Lambdas](01-lambdas.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Variables](../basics/02-variables-data-types.md)

## 💻 The Code

Let's examine closures in action:

**📁 File:** [37_lambdas_closures.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/37_lambdas_closures.kt)

## 🔍 Code Breakdown

### **1. Basic Closures**

#### **What are Closures?**
A closure is a function that captures variables from its enclosing scope. The function "remembers" the environment in which it was created, allowing it to access and modify those variables even after the original scope has finished executing.

#### **Simple Closure Example**
```kotlin
fun main() {
    val multiplier = 5
    
    // This lambda captures the 'multiplier' variable from outer scope
    val multiply = { x: Int -> x * multiplier }
    
    println("5 * 3 = ${multiply(3)}")  // 15
    
    // The closure still works even if we change the original variable
    // (though in Kotlin, captured variables are immutable by default)
}
```

#### **Variable Capture in Loops**
```kotlin
fun closureInLoop() {
    val functions = mutableListOf<() -> Int>()
    
    for (i in 1..3) {
        // Each lambda captures the current value of 'i'
        functions.add { i }
    }
    
    // Execute all functions
    functions.forEach { function ->
        println("Function result: ${function()}")
    }
}
```

**Output:**
```
Function result: 1
Function result: 2
Function result: 3
```

### **2. Advanced Closure Patterns**

#### **Stateful Closures**
```kotlin
fun createCounter(): () -> Int {
    var count = 0  // This variable is captured by the closure
    
    return {
        count++  // The closure can modify the captured variable
        count
    }
}

fun main() {
    val counter1 = createCounter()
    val counter2 = createCounter()
    
    println("Counter 1: ${counter1()}")  // 1
    println("Counter 1: ${counter1()}")  // 2
    println("Counter 1: ${counter1()}")  // 3
    
    println("Counter 2: ${counter2()}")  // 1 (separate state)
    println("Counter 2: ${counter2()}")  // 2
}
```

#### **Closure with Parameters**
```kotlin
fun createMultiplier(factor: Int): (Int) -> Int {
    // The 'factor' parameter is captured by the closure
    return { value -> value * factor }
}

fun main() {
    val double = createMultiplier(2)
    val triple = createMultiplier(3)
    
    println("Double of 5: ${double(5)}")    // 10
    println("Triple of 5: ${triple(5)}")    // 15
    
    // Each closure maintains its own captured 'factor' value
}
```

### **3. Closure with Complex Data**

#### **Object Capture**
```kotlin
data class User(val name: String, var age: Int)

fun createAgeUpdater(): (User) -> Unit {
    var updateCount = 0  // Captured variable
    
    return { user ->
        user.age += 1
        updateCount++
        println("Updated ${user.name}'s age to ${user.age} (update #$updateCount)")
    }
}

fun main() {
    val alice = User("Alice", 25)
    val bob = User("Bob", 30)
    
    val ageUpdater = createAgeUpdater()
    
    ageUpdater(alice)  // Updated Alice's age to 26 (update #1)
    ageUpdater(bob)    // Updated Bob's age to 31 (update #2)
    ageUpdater(alice)  // Updated Alice's age to 27 (update #3)
}
```

#### **Collection Processing with Closures**
```kotlin
fun createFilter<T>(predicate: (T) -> Boolean): (List<T>) -> List<T> {
    var filterCount = 0  // Captured variable
    
    return { list ->
        filterCount++
        val result = list.filter(predicate)
        println("Filter #$filterCount: ${list.size} items -> ${result.size} items")
        result
    }
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    val evenFilter = createFilter<Int> { it % 2 == 0 }
    val oddFilter = createFilter<Int> { it % 2 != 0 }
    
    evenFilter(numbers)  // Filter #1: 10 items -> 5 items
    oddFilter(numbers)   // Filter #2: 10 items -> 5 items
    evenFilter(numbers)  // Filter #3: 10 items -> 5 items
}
```

### **4. Closure Memory Management**

#### **Understanding Closure Lifecycle**
```kotlin
fun demonstrateClosureLifecycle() {
    var heavyData = "Large data string" * 1000  // Large data
    
    val closure = {
        println("Accessing: ${heavyData.length}")  // Captures heavyData
    }
    
    // The closure keeps a reference to heavyData
    println("Closure created")
    
    // Even after heavyData goes out of scope in the function,
    // the closure still holds a reference to it
    return closure
}

fun main() {
    val closure = demonstrateClosureLifecycle()
    
    // heavyData is still accessible through the closure
    closure()  // Accessing: 13000
    
    // The closure and its captured data will be garbage collected
    // when the closure is no longer referenced
}
```

#### **Avoiding Memory Leaks**
```kotlin
class DataProcessor {
    private var data: String? = null
    private var processor: (() -> Unit)? = null
    
    fun setData(newData: String) {
        data = newData
    }
    
    fun createProcessor(): () -> Unit {
        // Capture only what's needed, not the entire class
        val currentData = data ?: return { println("No data set") }
        
        return {
            println("Processing: $currentData")
        }
    }
    
    fun cleanup() {
        // Clear references to avoid memory leaks
        data = null
        processor = null
    }
}

fun main() {
    val processor = DataProcessor()
    processor.setData("Sample data")
    
    val processFunction = processor.createProcessor()
    processFunction()  // Processing: Sample data
    
    // Clean up when done
    processor.cleanup()
}
```

### **5. Real-World Closure Examples**

#### **Configuration Manager**
```kotlin
class ConfigurationManager {
    private val config = mutableMapOf<String, Any>()
    private val listeners = mutableListOf<(String, Any?) -> Unit>()
    
    fun set(key: String, value: Any) {
        val oldValue = config[key]
        config[key] = value
        
        // Notify all listeners
        listeners.forEach { listener ->
            listener(key, oldValue)
        }
    }
    
    fun addListener(listener: (String, Any?) -> Unit) {
        listeners.add(listener)
    }
    
    fun get(key: String): Any? = config[key]
}

fun main() {
    val configManager = ConfigurationManager()
    
    // Add a listener that captures the manager's state
    configManager.addListener { key, oldValue ->
        val newValue = configManager.get(key)
        println("Config changed: $key = $oldValue -> $newValue")
    }
    
    configManager.set("database.url", "localhost:5432")
    configManager.set("server.port", 8080)
}
```

#### **Event Handler with State**
```kotlin
class EventHandler {
    private val handlers = mutableMapOf<String, MutableList<() -> Unit>>()
    private var eventCount = 0  // State maintained by closures
    
    fun on(event: String, handler: () -> Unit) {
        handlers.getOrPut(event) { mutableListOf() }.add(handler)
    }
    
    fun fire(event: String) {
        eventCount++
        println("Firing event '$event' (total events: $eventCount)")
        
        handlers[event]?.forEach { handler ->
            try {
                handler()
            } catch (e: Exception) {
                println("Handler error: ${e.message}")
            }
        }
    }
}

fun main() {
    val eventHandler = EventHandler()
    
    // Each handler is a closure that can access the eventHandler's state
    eventHandler.on("user.login") {
        println("User logged in")
    }
    
    eventHandler.on("user.logout") {
        println("User logged out")
    }
    
    eventHandler.fire("user.login")   // Firing event 'user.login' (total events: 1)
    eventHandler.fire("user.logout")  // Firing event 'user.logout' (total events: 2)
}
```

#### **Retry Mechanism with Closure**
```kotlin
fun <T> createRetryMechanism(
    maxAttempts: Int,
    delayMs: Long = 1000
): (() -> T) -> T {
    var attemptCount = 0  // Captured state
    
    return { operation ->
        while (attemptCount < maxAttempts) {
            try {
                attemptCount++
                return operation()
            } catch (e: Exception) {
                if (attemptCount >= maxAttempts) {
                    throw e
                }
                println("Attempt $attemptCount failed: ${e.message}")
                println("Retrying in ${delayMs}ms...")
                Thread.sleep(delayMs)
            }
        }
        throw RuntimeException("All attempts failed")
    }
}

fun main() {
    val retry = createRetryMechanism(maxAttempts = 3, delayMs = 500)
    
    try {
        val result = retry {
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

### **1. Closure Definition**

**A closure is:**
- A function that captures variables from its enclosing scope
- A function that "remembers" its creation environment
- A way to maintain state between function calls
- A powerful tool for functional programming

### **2. Variable Capture Rules**

**In Kotlin:**
- **Local variables** are captured by value (immutable)
- **Mutable variables** can be captured and modified
- **Objects** are captured by reference
- **Primitive types** are captured by value

### **3. Closure Benefits**

- **State encapsulation** - Maintain state without global variables
- **Data privacy** - Control access to captured variables
- **Function composition** - Combine functions with shared state
- **Event handling** - Maintain context across event calls

## 🚀 Advanced Closure Patterns

### **1. Closure Factories**
```kotlin
fun createClosureFactory<T>(initialValue: T): () -> T {
    var value = initialValue
    
    return { value }
}

fun createMutableClosureFactory<T>(initialValue: T): () -> T {
    var value = initialValue
    
    return { 
        value = value  // This creates a mutable closure
        value 
    }
}
```

### **2. Closure Composition**
```kotlin
fun <T> composeClosures(vararg closures: (T) -> T): (T) -> T {
    return { value ->
        var result = value
        closures.forEach { closure ->
            result = closure(result)
        }
        result
    }
}

fun main() {
    val addOne = { x: Int -> x + 1 }
    val double = { x: Int -> x * 2 }
    val square = { x: Int -> x * x }
    
    val composed = composeClosures(addOne, double, square)
    println("Result: ${composed(2)}")  // ((2 + 1) * 2)² = 36
}
```

### **3. Closure with Generics**
```kotlin
class ClosureContainer<T>(private val initialValue: T) {
    private var value = initialValue
    
    fun createGetter(): () -> T = { value }
    
    fun createSetter(): (T) -> Unit = { newValue -> value = newValue }
    
    fun createUpdater(update: (T) -> T): () -> T = {
        value = update(value)
        value
    }
}

fun main() {
    val container = ClosureContainer("Hello")
    
    val getter = container.createGetter()
    val setter = container.createSetter()
    val updater = container.createUpdater { it + " World" }
    
    println(getter())        // Hello
    setter("Hi")
    println(getter())        // Hi
    println(updater())       // Hi World
}
```

## 💡 Best Practices

### **1. Minimize Captured Variables**
- Only capture what's necessary
- Avoid capturing large objects unnecessarily
- Use local variables when possible

### **2. Memory Management**
- Be aware of what your closures capture
- Clear references when closures are no longer needed
- Use weak references for long-lived closures

### **3. Closure Design**
- Keep closures focused and single-purpose
- Document what variables are captured
- Consider the lifecycle of captured variables

## 🔧 Common Pitfalls

### **1. Capturing Mutable State**
```kotlin
// ❌ Wrong - Capturing mutable state can lead to unexpected behavior
fun createCounter(): () -> Int {
    var count = 0
    return { count++ }
}

// ✅ Better - Be explicit about state management
fun createCounter(): () -> Int {
    var count = 0
    return { 
        count += 1
        count 
    }
}
```

### **2. Memory Leaks**
```kotlin
// ❌ Wrong - Capturing entire objects can cause memory leaks
class HeavyObject {
    val data = "Large data" * 1000
    
    fun createClosure(): () -> Unit {
        return { println(data) }  // Captures entire object
    }
}

// ✅ Better - Capture only what's needed
class HeavyObject {
    val data = "Large data" * 1000
    
    fun createClosure(): () -> Unit {
        val dataLength = data.length  // Capture only the length
        return { println("Data length: $dataLength") }
    }
}
```

### **3. Closure in Loops**
```kotlin
// ❌ Wrong - Common mistake with closures in loops
fun wrongWay() {
    val functions = mutableListOf<() -> Int>()
    for (i in 1..3) {
        functions.add { i }  // All closures capture the same 'i'
    }
    // All functions return 3!
}

// ✅ Correct - Use local variables
fun correctWay() {
    val functions = mutableListOf<() -> Int>()
    for (i in 1..3) {
        val localI = i  // Create local copy
        functions.add { localI }
    }
    // Functions return 1, 2, 3 as expected
}
```

## 📚 Summary

Closures are powerful tools that enable:
- **State management** without global variables
- **Function composition** with shared context
- **Event handling** with persistent state
- **Functional programming** patterns

## 🎯 Practice Exercises

1. **Stateful Counter**: Create a closure that maintains a counter state
2. **Configuration Manager**: Build a system that uses closures to manage configuration changes
3. **Event Handler**: Implement an event system using closures for state management
4. **Closure Factory**: Create a factory that generates closures with different behaviors

## 🔗 Related Topics

- [Lambdas](01-lambdas.md) - Anonymous functions
- [Higher-Order Functions](05-higher-order-functions.md) - Functions that take/return functions
- [Functions Basics](../functions/01-functions-basics.md) - Function fundamentals
- [Variables](../basics/02-variables-data-types.md) - Variable concepts

## 📖 Additional Resources

- [Official Kotlin Lambdas Documentation](https://kotlinlang.org/docs/lambdas.html)
- [Closure Concepts](https://kotlinlang.org/docs/lambdas.html#closures)
- [Function References](https://kotlinlang.org/docs/reflection.html#function-references)

---

**Next Lesson**: ['it' keyword](07-it-keyword.md) - Learn about the 'it' keyword in lambdas

**Happy coding with Closures! 🔒**
