# 🚀 Lambdas and Higher-Order Functions in Kotlin

Lambdas and higher-order functions are the foundation of functional programming in Kotlin. They allow you to write more concise, readable, and flexible code by treating functions as first-class citizens.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what lambdas are and how to create them
- ✅ Use higher-order functions that take functions as parameters
- ✅ Work with lambda syntax and parameter conventions
- ✅ Apply functional programming patterns in your code
- ✅ Use the `it` keyword and lambda conventions effectively

## 🔍 What You'll Learn

- **Lambda expressions** - Anonymous functions and their syntax
- **Higher-order functions** - Functions that take other functions as parameters
- **Lambda conventions** - Using `it`, single parameters, and destructuring
- **Functional patterns** - Common functional programming techniques
- **Real-world applications** - Practical examples of lambdas in action

## 📝 Prerequisites

- Understanding of [Functions](../functions/01-functions-basics.md)
- Knowledge of [Collections](../collections/01-arrays.md)
- Familiarity with [Control Flow](../control-flow/01-if-expressions.md)

## 💻 The Code

Let's examine the lambdas and higher-order functions examples:

**📁 File:** [35_lambdas_higher_order_functions.kt](../src/35_lambdas_higher_order_functions.kt)

## 🔍 Code Breakdown

### **1. Basic Lambda Expressions**

#### **Simple Lambda Syntax**
```kotlin
// Basic lambda that takes no parameters
val sayHello = { println("Hello, World!") }

// Lambda that takes a parameter
val greet = { name: String -> println("Hello, $name!") }

// Lambda that returns a value
val square = { x: Int -> x * x }

// Lambda with multiple parameters
val add = { a: Int, b: Int -> a + b }
```

#### **Lambda with Type Inference**
```kotlin
// Kotlin can infer types from context
val numbers = listOf(1, 2, 3, 4, 5)

// Type inference works here
val doubled = numbers.map { it * 2 }
val evenNumbers = numbers.filter { it % 2 == 0 }
val sum = numbers.reduce { acc, num -> acc + num }
```

### **2. Higher-Order Functions**

#### **Functions as Parameters**
```kotlin
// Function that takes another function as a parameter
fun executeOperation(operation: (Int, Int) -> Int, a: Int, b: Int): Int {
    return operation(a, b)
}

// Function that takes a function with no parameters
fun repeatAction(times: Int, action: () -> Unit) {
    repeat(times) {
        action()
    }
}

// Function that returns a function
fun createMultiplier(factor: Int): (Int) -> Int {
    return { number -> number * factor }
}
```

#### **Using Higher-Order Functions**
```kotlin
fun main() {
    // Pass lambda to executeOperation
    val result1 = executeOperation({ a, b -> a + b }, 5, 3)      // 8
    val result2 = executeOperation({ a, b -> a * b }, 4, 6)      // 24
    
    // Pass lambda to repeatAction
    repeatAction(3) { println("Hello!") }
    
    // Use returned function
    val double = createMultiplier(2)
    val triple = createMultiplier(3)
    
    println(double(5))  // 10
    println(triple(5))  // 15
}
```

### **3. Lambda with Collections**

#### **Common Collection Functions**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// forEach - execute action for each element
numbers.forEach { println("Number: $it") }

// map - transform each element
val squared = numbers.map { it * it }

// filter - select elements based on condition
val evenNumbers = numbers.filter { it % 2 == 0 }

// reduce - combine all elements into single result
val sum = numbers.reduce { acc, num -> acc + num }

// any - check if any element matches condition
val hasEven = numbers.any { it % 2 == 0 }

// all - check if all elements match condition
val allPositive = numbers.all { it > 0 }
```

#### **Chaining Lambda Operations**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Chain multiple operations
val result = numbers
    .filter { it % 2 == 0 }        // Keep even numbers
    .map { it * it }                // Square them
    .take(3)                        // Take first 3
    .sum()                          // Sum the result

println(result)  // 4 + 16 + 36 = 56
```

### **4. Lambda Conventions and `it` Keyword**

#### **Using `it` for Single Parameters**
```kotlin
val names = listOf("Alice", "Bob", "Charlie", "David")

// When lambda has single parameter, you can use 'it'
val upperNames = names.map { it.uppercase() }
val longNames = names.filter { it.length > 4 }
val nameLengths = names.map { it.length }
```

#### **Lambda with Multiple Parameters**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// Multiple parameters need explicit names
val pairs = numbers.mapIndexed { index, value -> 
    "Index $index: Value $value" 
}

// Using destructuring in lambda
val people = listOf("Alice" to 25, "Bob" to 30, "Charlie" to 35)
val descriptions = people.map { (name, age) -> 
    "$name is $age years old" 
}
```

### **5. Advanced Lambda Patterns**

#### **Lambda with Receiver (Extension Function Style)**
```kotlin
// Lambda that acts as an extension function
val buildString = buildString {
    append("Hello")
    append(" ")
    append("World")
    append("!")
}

// Using with() function
val person = Person("Alice", 25)
val description = with(person) {
    "Name: $name, Age: $age"
}
```

#### **Lambda with Local Variables**
```kotlin
fun processNumbers(numbers: List<Int>) {
    var sum = 0
    var count = 0
    
    numbers.forEach { num ->
        sum += num
        count++
    }
    
    println("Sum: $sum, Count: $count, Average: ${sum.toDouble() / count}")
}
```

#### **Lambda with Return Statements**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Using forEach with early return (using labels)
numbers.forEach { num ->
    if (num == 5) {
        return@forEach  // Return from lambda, not from function
    }
    println("Processing: $num")
}
```

### **6. Practical Examples**

#### **Custom Higher-Order Functions**
```kotlin
// Function that retries an operation
fun <T> retry(
    times: Int,
    operation: () -> T,
    onError: (Exception) -> Unit = { }
): T? {
    repeat(times) { attempt ->
        try {
            return operation()
        } catch (e: Exception) {
            onError(e)
            if (attempt == times - 1) throw e
        }
    }
    return null
}

// Function that measures execution time
fun <T> measureTime(operation: () -> T): Pair<T, Long> {
    val startTime = System.currentTimeMillis()
    val result = operation()
    val endTime = System.currentTimeMillis()
    return result to (endTime - startTime)
}
```

#### **Using Custom Functions**
```kotlin
fun main() {
    // Retry example
    val result = retry(3, {
        // Simulate operation that might fail
        if (Math.random() < 0.7) throw RuntimeException("Random failure")
        "Success!"
    }) { error ->
        println("Attempt failed: ${error.message}")
    }
    
    println("Final result: $result")
    
    // Measure time example
    val (sum, time) = measureTime {
        (1..1000000).sum()
    }
    
    println("Sum: $sum, Time: ${time}ms")
}
```

## 🎯 Key Concepts Explained

### **1. Lambda vs Function**
```kotlin
// Function declaration
fun add(a: Int, b: Int): Int = a + b

// Lambda expression
val addLambda = { a: Int, b: Int -> a + b }

// Both can be used similarly
val result1 = add(5, 3)
val result2 = addLambda(5, 3)
```

### **2. Higher-Order Function Benefits**
- **Reusability**: Write once, use many times
- **Flexibility**: Change behavior without changing function
- **Readability**: Intent is clear from function name
- **Testability**: Easy to test different behaviors

### **3. Lambda Performance**
```kotlin
// Lambdas are objects, so there's a small overhead
val numbers = (1..1000000).toList()

// For simple operations, consider inline functions
inline fun <T> List<T>.customFilter(predicate: (T) -> Boolean): List<T> {
    return filter(predicate)
}
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/35_lambdas_higher_order_functions.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '35_lambdas_higher_order_functionsKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Custom Collection Functions**
Create your own higher-order functions for collections.

**Solution:**
```kotlin
fun <T> List<T>.customForEach(action: (T) -> Unit) {
    for (item in this) {
        action(item)
    }
}

fun <T> List<T>.customMap(transform: (T) -> T): List<T> {
    val result = mutableListOf<T>()
    for (item in this) {
        result.add(transform(item))
    }
    return result
}

fun <T> List<T>.customFilter(predicate: (T) -> Boolean): List<T> {
    val result = mutableListOf<T>()
    for (item in this) {
        if (predicate(item)) {
            result.add(item)
        }
    }
    return result
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    
    numbers.customForEach { println("Number: $it") }
    
    val doubled = numbers.customMap { it * 2 }
    println("Doubled: $doubled")
    
    val evenNumbers = numbers.customFilter { it % 2 == 0 }
    println("Even: $evenNumbers")
}
```

### **Exercise 2: Function Composition**
Create functions that compose other functions.

**Solution:**
```kotlin
// Compose two functions
fun <A, B, C> compose(f: (B) -> C, g: (A) -> B): (A) -> C {
    return { a -> f(g(a)) }
}

// Compose multiple functions
fun <T> compose(vararg functions: (T) -> T): (T) -> T {
    return { value ->
        functions.fold(value) { acc, func -> func(acc) }
    }
}

fun main() {
    val addOne = { x: Int -> x + 1 }
    val multiplyByTwo = { x: Int -> x * 2 }
    val square = { x: Int -> x * x }
    
    // Compose two functions
    val addOneThenMultiply = compose(multiplyByTwo, addOne)
    println(addOneThenMultiply(5))  // (5 + 1) * 2 = 12
    
    // Compose multiple functions
    val complexOperation = compose(addOne, multiplyByTwo, square)
    println(complexOperation(3))  // ((3 + 1) * 2)^2 = 64
}
```

### **Exercise 3: Event Handling System**
Create a simple event handling system using lambdas.

**Solution:**
```kotlin
class EventHandler {
    private val listeners = mutableMapOf<String, MutableList<() -> Unit>>()
    
    fun addListener(event: String, listener: () -> Unit) {
        listeners.getOrPut(event) { mutableListOf() }.add(listener)
    }
    
    fun removeListener(event: String, listener: () -> Unit) {
        listeners[event]?.remove(listener)
    }
    
    fun triggerEvent(event: String) {
        listeners[event]?.forEach { it() }
    }
}

fun main() {
    val eventHandler = EventHandler()
    
    // Add listeners
    eventHandler.addListener("userLogin") { 
        println("User logged in - sending welcome email") 
    }
    eventHandler.addListener("userLogin") { 
        println("User logged in - updating last login time") 
    }
    eventHandler.addListener("userLogout") { 
        println("User logged out - cleaning up session") 
    }
    
    // Trigger events
    eventHandler.triggerEvent("userLogin")
    println("---")
    eventHandler.triggerEvent("userLogout")
}
```

### **Exercise 4: Data Processing Pipeline**
Create a data processing pipeline using functional programming.

**Solution:**
```kotlin
data class Person(val name: String, val age: Int, val city: String)

class DataProcessor<T> {
    private var pipeline: (List<T>) -> List<T> = { it }
    
    fun filter(predicate: (T) -> Boolean): DataProcessor<T> {
        val currentPipeline = pipeline
        pipeline = { data -> currentPipeline(data).filter(predicate) }
        return this
    }
    
    fun map(transform: (T) -> T): DataProcessor<T> {
        val currentPipeline = pipeline
        pipeline = { data -> currentPipeline(data).map(transform) }
        return this
    }
    
    fun sort(comparator: (T, T) -> Int): DataProcessor<T> {
        val currentPipeline = pipeline
        pipeline = { data -> currentPipeline(data).sortedWith(comparator) }
        return this
    }
    
    fun process(data: List<T>): List<T> = pipeline(data)
}

fun main() {
    val people = listOf(
        Person("Alice", 25, "New York"),
        Person("Bob", 30, "Boston"),
        Person("Charlie", 22, "Chicago"),
        Person("David", 35, "New York"),
        Person("Eve", 28, "Boston")
    )
    
    val processor = DataProcessor<Person>()
        .filter { it.age > 25 }
        .filter { it.city == "New York" }
        .map { Person(it.name, it.age + 1, it.city) }
        .sort { a, b -> a.name.compareTo(b.name) }
    
    val result = processor.process(people)
    result.forEach { println("${it.name} (${it.age}) from ${it.city}") }
}
```

## 🚨 Common Mistakes to Avoid

1. **Forgetting parentheses**: `numbers.map { it * 2 }` ✅ vs `numbers.map({ it * 2 })` ✅
2. **Using wrong parameter names**: Use `it` for single parameters ✅
3. **Ignoring return types**: Let Kotlin infer types when possible ✅
4. **Overusing lambdas**: Sometimes a simple function is clearer ✅

## 🎯 What's Next?

Now that you understand lambdas and higher-order functions, continue with:

1. **Scope Functions** → [Scope Functions](02-scope-functions.md)
2. **Collections** → [Collections Overview](../collections/README.md)
3. **Null Safety** → [Null Safety](../null-safety/01-null-safety.md)
4. **Coroutines** → [Coroutines](../coroutines/01-introduction.md)

## 📚 Additional Resources

- [Official Kotlin Lambdas Documentation](https://kotlinlang.org/docs/lambdas.html)
- [Higher-Order Functions](https://kotlinlang.org/docs/lambdas.html#higher-order-functions)
- [Lambda Expressions](https://kotlinlang.org/docs/lambdas.html#lambda-expressions-and-anonymous-functions)

## 🏆 Summary

- ✅ You understand lambda expressions and their syntax
- ✅ You can create and use higher-order functions
- ✅ You know how to use lambda conventions and the `it` keyword
- ✅ You can apply functional programming patterns
- ✅ You're ready to write more expressive and flexible Kotlin code!

**Lambdas and higher-order functions make your code more powerful and expressive. Embrace functional programming! 🎉**
