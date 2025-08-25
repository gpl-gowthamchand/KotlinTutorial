# ⚡ Introduction to Coroutines in Kotlin

Coroutines are Kotlin's solution for asynchronous programming. They allow you to write asynchronous, non-blocking code in a sequential, readable manner. Coroutines are lightweight threads that can be suspended and resumed, making them perfect for handling long-running operations without blocking the main thread.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what coroutines are and why they're useful
- ✅ Create and launch basic coroutines
- ✅ Use `runBlocking` to bridge between blocking and non-blocking code
- ✅ Understand the difference between coroutines and threads
- ✅ Write simple asynchronous code using coroutines

## 🔍 What You'll Learn

- **Coroutine basics** - What coroutines are and how they work
- **Coroutine builders** - Different ways to create coroutines
- **Suspending functions** - Functions that can pause execution
- **Coroutine context** - Understanding where coroutines run
- **Basic coroutine patterns** - Common use cases and examples

## 📝 Prerequisites

- Understanding of [Functions](../functions/01-functions-basics.md)
- Knowledge of [Control Flow](../control-flow/01-if-expressions.md)
- Familiarity with [Collections](../collections/01-arrays.md)
- Basic understanding of asynchronous programming concepts

## 💻 The Code

Let's examine the coroutines examples:

**📁 File:** [61_first_coroutine.kt](../src/61_first_coroutine.kt)

## 🔍 Code Breakdown

### **1. What Are Coroutines?**

#### **Basic Definition**
```kotlin
// Coroutines are functions that can be suspended and resumed
// They allow you to write asynchronous code in a sequential manner

// Traditional approach (blocking)
fun traditionalFunction() {
    Thread.sleep(1000)  // Blocks the thread
    println("After delay")
}

// Coroutine approach (non-blocking)
suspend fun coroutineFunction() {
    delay(1000)  // Suspends the coroutine, doesn't block the thread
    println("After delay")
}
```

#### **Key Benefits**
```kotlin
// 1. Lightweight - Thousands of coroutines can run on a single thread
// 2. Non-blocking - Don't block the thread they run on
// 3. Sequential - Code looks like regular sequential code
// 4. Cancellable - Can be cancelled at any time
// 5. Exception handling - Built-in exception handling mechanisms
```

### **2. Your First Coroutine**

#### **Using `runBlocking`**
```kotlin
fun main() {
    println("Starting main function")
    
    runBlocking {
        println("Inside coroutine")
        delay(1000)  // Suspend for 1 second
        println("After delay in coroutine")
    }
    
    println("Back in main function")
}
```

#### **Using `launch`**
```kotlin
fun main() {
    println("Starting main function")
    
    // Launch a new coroutine
    GlobalScope.launch {
        println("Inside launched coroutine")
        delay(1000)
        println("After delay in launched coroutine")
    }
    
    println("Main function continues immediately")
    Thread.sleep(2000)  // Wait for coroutine to complete
}
```

### **3. Coroutine Builders**

#### **`runBlocking` - Bridge Between Blocking and Non-Blocking**
```kotlin
fun main() {
    println("Main thread: ${Thread.currentThread().name}")
    
    runBlocking {
        println("Coroutine thread: ${Thread.currentThread().name}")
        delay(1000)
        println("Coroutine completed")
    }
    
    println("Main thread continues")
}
```

#### **`launch` - Fire and Forget**
```kotlin
fun main() {
    println("Starting main")
    
    val job = GlobalScope.launch {
        println("Coroutine started")
        delay(1000)
        println("Coroutine completed")
    }
    
    println("Main continues")
    job.join()  // Wait for coroutine to complete
    println("Main finished")
}
```

#### **`async` - Return a Result**
```kotlin
fun main() {
    println("Starting main")
    
    val deferred = GlobalScope.async {
        println("Async coroutine started")
        delay(1000)
        "Result from coroutine"
    }
    
    println("Main continues")
    val result = deferred.await()  // Wait for result
    println("Got result: $result")
    println("Main finished")
}
```

### **4. Suspending Functions**

#### **Creating Suspending Functions**
```kotlin
// Regular function
fun regularFunction() {
    println("Regular function")
}

// Suspending function
suspend fun suspendingFunction() {
    println("Suspending function started")
    delay(1000)  // Can only be called from coroutines
    println("Suspending function completed")
}

// Suspending function with return value
suspend fun fetchData(): String {
    delay(1000)  // Simulate network call
    return "Data from network"
}
```

#### **Using Suspending Functions**
```kotlin
fun main() {
    runBlocking {
        println("Calling suspending function")
        val data = fetchData()
        println("Received: $data")
        
        println("Calling another suspending function")
        suspendingFunction()
        println("All done!")
    }
}
```

### **5. Coroutine Context and Dispatchers**

#### **Understanding Dispatchers**
```kotlin
fun main() {
    runBlocking {
        // Default dispatcher (shared thread pool)
        launch {
            println("Default dispatcher: ${Thread.currentThread().name}")
        }
        
        // IO dispatcher (for network/disk operations)
        launch(Dispatchers.IO) {
            println("IO dispatcher: ${Thread.currentThread().name}")
        }
        
        // Main dispatcher (for UI operations in Android)
        launch(Dispatchers.Main) {
            println("Main dispatcher: ${Thread.currentThread().name}")
        }
        
        // Unconfined dispatcher (inherits from parent)
        launch(Dispatchers.Unconfined) {
            println("Unconfined dispatcher: ${Thread.currentThread().name}")
        }
    }
}
```

#### **Custom Coroutine Context**
```kotlin
fun main() {
    runBlocking {
        // Create a custom context
        val customContext = Dispatchers.IO + SupervisorJob()
        
        launch(customContext) {
            println("Custom context: ${Thread.currentThread().name}")
            delay(1000)
            println("Custom context completed")
        }
        
        println("Main coroutine continues")
    }
}
```

### **6. Practical Examples**

#### **Simulating Network Calls**
```kotlin
suspend fun fetchUserData(userId: Int): String {
    delay(1000)  // Simulate network delay
    return "User data for ID: $userId"
}

suspend fun fetchUserPosts(userId: Int): String {
    delay(800)   // Simulate network delay
    return "Posts for user ID: $userId"
}

fun main() {
    runBlocking {
        println("Fetching user data...")
        
        val userData = fetchUserData(123)
        val userPosts = fetchUserPosts(123)
        
        println("User data: $userData")
        println("User posts: $userPosts")
        println("All data fetched!")
    }
}
```

#### **Parallel Execution**
```kotlin
fun main() {
    runBlocking {
        println("Starting parallel execution")
        
        val startTime = System.currentTimeMillis()
        
        // Launch coroutines in parallel
        val deferred1 = async { fetchUserData(1) }
        val deferred2 = async { fetchUserData(2) }
        val deferred3 = async { fetchUserData(3) }
        
        // Wait for all results
        val result1 = deferred1.await()
        val result2 = deferred2.await()
        val result3 = deferred3.await()
        
        val endTime = System.currentTimeMillis()
        
        println("Results: $result1, $result2, $result3")
        println("Total time: ${endTime - startTime}ms")
    }
}
```

## 🎯 Key Concepts Explained

### **1. Coroutines vs Threads**
```kotlin
// Threads are expensive - limited number can be created
// Coroutines are lightweight - thousands can run simultaneously

// Thread approach
fun threadExample() {
    repeat(1000) {
        Thread {
            Thread.sleep(1000)
            println("Thread $it completed")
        }.start()
    }
    // This would create 1000 threads - very expensive!
}

// Coroutine approach
fun coroutineExample() {
    runBlocking {
        repeat(1000) {
            launch {
                delay(1000)
                println("Coroutine $it completed")
            }
        }
    }
    // This creates 1000 coroutines - very lightweight!
}
```

### **2. Suspending vs Blocking**
```kotlin
// Blocking - stops the entire thread
fun blockingFunction() {
    Thread.sleep(1000)  // Thread is blocked for 1 second
}

// Suspending - only suspends the coroutine
suspend fun suspendingFunction() {
    delay(1000)  // Only this coroutine is suspended
    // Other coroutines on the same thread can continue
}
```

### **3. Coroutine Scopes**
```kotlin
// GlobalScope - lives as long as the application
GlobalScope.launch { /* ... */ }

// runBlocking - blocks the current thread until completion
runBlocking { /* ... */ }

// CoroutineScope - custom scope with lifecycle management
val scope = CoroutineScope(Dispatchers.Main)
scope.launch { /* ... */ }
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/61_first_coroutine.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '61_first_coroutineKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Basic Coroutine Operations**
Create and run basic coroutines with different delays.

**Solution:**
```kotlin
fun main() {
    runBlocking {
        println("Starting exercise")
        
        // Launch multiple coroutines
        val job1 = launch {
            delay(1000)
            println("Coroutine 1 completed")
        }
        
        val job2 = launch {
            delay(500)
            println("Coroutine 2 completed")
        }
        
        val job3 = launch {
            delay(1500)
            println("Coroutine 3 completed")
        }
        
        // Wait for all to complete
        job1.join()
        job2.join()
        job3.join()
        
        println("All coroutines completed")
    }
}
```

### **Exercise 2: Suspending Functions**
Create and use your own suspending functions.

**Solution:**
```kotlin
suspend fun processItem(item: String): String {
    delay(500)  // Simulate processing time
    return "Processed: $item"
}

suspend fun validateItem(item: String): Boolean {
    delay(200)  // Simulate validation time
    return item.length > 0
}

fun main() {
    runBlocking {
        val items = listOf("Apple", "Banana", "Cherry")
        
        items.forEach { item ->
            val isValid = validateItem(item)
            if (isValid) {
                val processed = processItem(item)
                println(processed)
            } else {
                println("Invalid item: $item")
            }
        }
        
        println("All items processed")
    }
}
```

### **Exercise 3: Parallel Processing**
Process multiple items in parallel using coroutines.

**Solution:**
```kotlin
suspend fun processItem(item: String): String {
    delay(1000)  // Simulate processing time
    return "Processed: $item"
}

fun main() {
    runBlocking {
        val items = listOf("Item1", "Item2", "Item3", "Item4", "Item5")
        
        println("Starting parallel processing")
        val startTime = System.currentTimeMillis()
        
        // Process all items in parallel
        val deferreds = items.map { item ->
            async {
                processItem(item)
            }
        }
        
        // Wait for all results
        val results = deferreds.awaitAll()
        
        val endTime = System.currentTimeMillis()
        
        results.forEach { println(it) }
        println("Total time: ${endTime - startTime}ms")
        println("Parallel processing completed")
    }
}
```

### **Exercise 4: Coroutine Context Management**
Use different dispatchers and manage coroutine contexts.

**Solution:**
```kotlin
suspend fun cpuIntensiveTask(): Int {
    var result = 0
    repeat(1000000) {
        result += it
    }
    return result
}

suspend fun ioTask(): String {
    delay(1000)  // Simulate I/O operation
    return "I/O completed"
}

fun main() {
    runBlocking {
        println("Starting context management exercise")
        
        // CPU-intensive task on Default dispatcher
        val cpuResult = withContext(Dispatchers.Default) {
            println("CPU task on: ${Thread.currentThread().name}")
            cpuIntensiveTask()
        }
        
        // I/O task on IO dispatcher
        val ioResult = withContext(Dispatchers.IO) {
            println("I/O task on: ${Thread.currentThread().name}")
            ioTask()
        }
        
        // Main thread task
        withContext(Dispatchers.Main) {
            println("Main task on: ${Thread.currentThread().name}")
        }
        
        println("CPU result: $cpuResult")
        println("I/O result: $ioResult")
        println("All tasks completed")
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Forgetting `runBlocking`**: Can't call suspending functions from regular functions ✅
2. **Using GlobalScope in production**: Can lead to memory leaks ✅
3. **Ignoring coroutine context**: Choose the right dispatcher for your use case ✅
4. **Not handling exceptions**: Coroutines can fail, handle errors appropriately ✅

## 🎯 What's Next?

Now that you understand coroutines basics, continue with:

1. **Launch and Async** → [Launch and Async Coroutines](02-launch-async.md)
2. **Exception Handling** → [Coroutine Exception Handling](03-exception-handling.md)
3. **Coroutine Context** → [Coroutine Context and Dispatchers](04-context-dispatchers.md)
4. **Advanced Patterns** → [Advanced Coroutine Patterns](05-advanced-patterns.md)

## 📚 Additional Resources

- [Official Kotlin Coroutines Documentation](https://kotlinlang.org/docs/coroutines-overview.html)
- [Coroutines Guide](https://kotlinlang.org/docs/coroutines-guide.html)
- [Coroutines Basics](https://kotlinlang.org/docs/coroutines-basics.html)

## 🏆 Summary

- ✅ You understand what coroutines are and their benefits
- ✅ You can create and launch basic coroutines
- ✅ You know how to use `runBlocking`, `launch`, and `async`
- ✅ You understand suspending functions and coroutine context
- ✅ You're ready to write asynchronous, non-blocking code!

**Coroutines make asynchronous programming simple and readable. Start building responsive applications! 🎉**
