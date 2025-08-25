# 🎭 Coroutine Context and Dispatchers

This lesson covers Kotlin coroutine context and dispatchers, which control how and where coroutines execute. Understanding these concepts is essential for optimizing performance and managing resources in concurrent applications.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand coroutine context and its components
- ✅ Use different dispatchers for various types of work
- ✅ Combine context elements effectively
- ✅ Manage coroutine lifecycle with context
- ✅ Optimize performance with appropriate dispatchers

## 🔍 What You'll Learn

- **Coroutine Context** - Understanding context structure and elements
- **Dispatchers** - Default, IO, Main, and Unconfined dispatchers
- **Context Combination** - Adding and removing context elements
- **Performance Optimization** - Choosing the right dispatcher for the job
- **Real-world Applications** - Practical use cases and patterns

## 📝 Prerequisites

- Understanding of [Coroutines Introduction](../coroutines/01-introduction.md)
- Knowledge of [Launch and Async](../coroutines/02-launch-async.md)
- Familiarity with [Exception Handling](../coroutines/03-exception-handling.md)

## 💻 The Code

Let's examine the context and dispatcher examples:

**📁 File:** [78_CoroutineContext_and_Dispatchers.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/78_CoroutineContext_and_Dispatchers.kt)

## 🔍 Code Breakdown

### **1. Understanding Coroutine Context**

#### **Basic Context Structure**
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    // Every coroutine has a context
    val job = launch {
        println("Coroutine context: ${coroutineContext}")
        println("Job: ${coroutineContext[Job]}")
        println("Dispatcher: ${coroutineContext[CoroutineDispatcher]}")
    }
    
    job.join()
}
```

#### **Context Elements**
```kotlin
fun main() = runBlocking {
    // Context contains various elements
    val job = launch {
        println("Context elements:")
        coroutineContext.forEach { (key, value) ->
            println("  $key -> $value")
        }
    }
    
    job.join()
}
```

### **2. Coroutine Dispatchers**

#### **Default Dispatcher**
```kotlin
fun main() = runBlocking {
    // Default dispatcher - CPU-intensive work
    val job1 = launch(Dispatchers.Default) {
        println("Running on Default dispatcher: ${Thread.currentThread().name}")
        
        // CPU-intensive computation
        var result = 0
        repeat(1000000) {
            result += it
        }
        println("Computation result: $result")
    }
    
    job1.join()
}
```

#### **IO Dispatcher**
```kotlin
fun main() = runBlocking {
    // IO dispatcher - network, file operations
    val job1 = launch(Dispatchers.IO) {
        println("Running on IO dispatcher: ${Thread.currentThread().name}")
        
        // Simulate IO operation
        delay(1000)
        println("IO operation completed")
    }
    
    val job2 = launch(Dispatchers.IO) {
        println("Another IO operation on: ${Thread.currentThread().name}")
        delay(500)
        println("Second IO operation completed")
    }
    
    job1.join()
    job2.join()
}
```

#### **Main Dispatcher**
```kotlin
fun main() = runBlocking {
    // Main dispatcher - UI updates (Android, JS)
    val job = launch(Dispatchers.Main) {
        println("Running on Main dispatcher: ${Thread.currentThread().name}")
        
        // UI update operations would go here
        println("UI updated successfully")
    }
    
    job.join()
}
```

#### **Unconfined Dispatcher**
```kotlin
fun main() = runBlocking {
    // Unconfined dispatcher - inherits context from caller
    val job = launch(Dispatchers.Unconfined) {
        println("Unconfined start: ${Thread.currentThread().name}")
        
        delay(100)
        println("Unconfined after delay: ${Thread.currentThread().name}")
    }
    
    job.join()
}
```

### **3. Context Combination and Modification**

#### **Combining Context Elements**
```kotlin
fun main() = runBlocking {
    // Combine dispatcher with exception handler
    val exceptionHandler = CoroutineExceptionHandler { _, exception ->
        println("Caught: ${exception.message}")
    }
    
    val job = launch(Dispatchers.IO + exceptionHandler) {
        println("Running on IO with exception handler: ${Thread.currentThread().name}")
        throw RuntimeException("Test exception")
    }
    
    job.join()
}
```

#### **Adding and Removing Context Elements**
```kotlin
fun main() = runBlocking {
    val parentJob = Job()
    val exceptionHandler = CoroutineExceptionHandler { _, exception ->
        println("Exception: ${exception.message}")
    }
    
    // Start with parent job and exception handler
    val job1 = launch(parentJob + Dispatchers.IO + exceptionHandler) {
        println("Job 1: ${Thread.currentThread().name}")
        delay(1000)
    }
    
    // Remove parent job for independent execution
    val job2 = launch(Dispatchers.IO + exceptionHandler) {
        println("Job 2: ${Thread.currentThread().name}")
        delay(500)
    }
    
    job1.join()
    job2.join()
    
    // Cancel parent job
    parentJob.cancel()
}
```

#### **Context Inheritance**
```kotlin
fun main() = runBlocking {
    // Parent coroutine context
    val parentContext = coroutineContext + Dispatchers.IO
    
    val job = launch(parentContext) {
        println("Child inherits IO dispatcher: ${Thread.currentThread().name}")
        
        // Child can override context
        withContext(Dispatchers.Default) {
            println("Child switches to Default: ${Thread.currentThread().name}")
        }
        
        println("Child back to inherited IO: ${Thread.currentThread().name}")
    }
    
    job.join()
}
```

### **4. Advanced Context Patterns**

#### **Custom Dispatcher**
```kotlin
import java.util.concurrent.Executors

fun main() = runBlocking {
    // Create custom dispatcher with fixed thread pool
    val customDispatcher = Executors.newFixedThreadPool(2).asCoroutineDispatcher()
    
    val jobs = List(5) { index ->
        launch(customDispatcher) {
            println("Job $index on custom dispatcher: ${Thread.currentThread().name}")
            delay(100)
        }
    }
    
    jobs.forEach { it.join() }
    
    // Clean up custom dispatcher
    customDispatcher.close()
}
```

#### **Context Switching with withContext**
```kotlin
fun main() = runBlocking {
    println("Main coroutine: ${Thread.currentThread().name}")
    
    val result = withContext(Dispatchers.IO) {
        println("Switched to IO: ${Thread.currentThread().name}")
        delay(1000)
        "Data from IO operation"
    }
    
    println("Back to main: ${Thread.currentThread().name}")
    println("Result: $result")
}
```

#### **Structured Concurrency with Context**
```kotlin
fun main() = runBlocking {
    // Parent context with IO dispatcher
    val parentContext = Dispatchers.IO + SupervisorJob()
    
    coroutineScope(parentContext) {
        val job1 = launch {
            println("Job 1 on IO: ${Thread.currentThread().name}")
            delay(1000)
            println("Job 1 completed")
        }
        
        val job2 = launch {
            println("Job 2 on IO: ${Thread.currentThread().name}")
            delay(500)
            println("Job 2 completed")
        }
        
        // Both jobs inherit parent context
        job1.join()
        job2.join()
    }
    
    println("All jobs completed")
}
```

### **5. Performance and Best Practices**

#### **Dispatcher Selection Guidelines**
```kotlin
fun main() = runBlocking {
    // CPU-intensive work
    val cpuJob = launch(Dispatchers.Default) {
        val start = System.currentTimeMillis()
        var result = 0
        repeat(1000000) {
            result += it * it
        }
        val duration = System.currentTimeMillis() - start
        println("CPU work completed in ${duration}ms: $result")
    }
    
    // IO work
    val ioJob = launch(Dispatchers.IO) {
        val start = System.currentTimeMillis()
        delay(1000) // Simulate IO
        val duration = System.currentTimeMillis() - start
        println("IO work completed in ${duration}ms")
    }
    
    cpuJob.join()
    ioJob.join()
}
```

#### **Context Optimization**
```kotlin
class DataProcessor {
    // Use IO dispatcher for data operations
    suspend fun processData(data: String): String {
        return withContext(Dispatchers.IO) {
            // Simulate data processing
            delay(500)
            "Processed: $data"
        }
    }
    
    // Use Default dispatcher for computations
    suspend fun computeResult(numbers: List<Int>): Int {
        return withContext(Dispatchers.Default) {
            // CPU-intensive computation
            numbers.sum()
        }
    }
}

fun main() = runBlocking {
    val processor = DataProcessor()
    
    val data = processor.processData("sample data")
    val result = processor.computeResult(listOf(1, 2, 3, 4, 5))
    
    println("Data: $data")
    println("Result: $result")
}
```

## 🎯 Key Concepts Explained

### **1. Dispatcher Types and Use Cases**

| Dispatcher | Use Case | Thread Pool | Characteristics |
|------------|----------|-------------|-----------------|
| **Default** | CPU-intensive work | Shared thread pool | Limited threads, efficient for computations |
| **IO** | Network, file operations | Unlimited threads | Many threads, good for blocking operations |
| **Main** | UI updates | Single thread | Main thread, UI operations only |
| **Unconfined** | Testing, special cases | Inherits from caller | No thread confinement, unpredictable |

### **2. Context Element Hierarchy**
```kotlin
// Context elements are combined with + operator
val context = Dispatchers.IO + SupervisorJob() + CoroutineName("MyCoroutine")

// Order matters for some elements
val job = launch(context) {
    // Coroutine inherits all context elements
}
```

### **3. Context Inheritance Rules**
- Child coroutines inherit parent context
- Children can override specific elements
- `withContext` temporarily changes context
- Context changes are isolated to the block

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/78_CoroutineContext_and_Dispatchers.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '78_CoroutineContext_and_DispatchersKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Dispatcher Selection**
Create a program that demonstrates when to use each dispatcher type.

**Solution:**
```kotlin
import kotlinx.coroutines.*

class TaskExecutor {
    suspend fun executeCpuTask(): String {
        return withContext(Dispatchers.Default) {
            println("CPU task on: ${Thread.currentThread().name}")
            var result = 0
            repeat(1000000) {
                result += it * it
            }
            "CPU result: $result"
        }
    }
    
    suspend fun executeIoTask(): String {
        return withContext(Dispatchers.IO) {
            println("IO task on: ${Thread.currentThread().name}")
            delay(1000) // Simulate IO
            "IO completed"
        }
    }
    
    suspend fun executeUiTask(): String {
        return withContext(Dispatchers.Main) {
            println("UI task on: ${Thread.currentThread().name}")
            "UI updated"
        }
    }
}

fun main() = runBlocking {
    val executor = TaskExecutor()
    
    val cpuResult = executor.executeCpuTask()
    val ioResult = executor.executeIoTask()
    val uiResult = executor.executeUiTask()
    
    println("Results: $cpuResult, $ioResult, $uiResult")
}
```

### **Exercise 2: Context Combination**
Create a coroutine system with custom context combinations.

**Solution:**
```kotlin
import kotlinx.coroutines.*
import java.util.concurrent.Executors

fun main() = runBlocking {
    // Custom context elements
    val customDispatcher = Executors.newFixedThreadPool(3).asCoroutineDispatcher()
    val exceptionHandler = CoroutineExceptionHandler { _, exception ->
        println("Custom handler: ${exception.message}")
    }
    val parentJob = SupervisorJob()
    
    // Combine all elements
    val context = customDispatcher + exceptionHandler + parentJob
    
    val jobs = List(5) { index ->
        launch(context) {
            println("Job $index on custom context: ${Thread.currentThread().name}")
            
            if (index == 2) {
                throw RuntimeException("Job $index failed")
            }
            
            delay(1000)
            println("Job $index completed")
        }
    }
    
    try {
        jobs.forEach { it.join() }
    } catch (e: Exception) {
        println("Caught exception: ${e.message}")
    } finally {
        customDispatcher.close()
    }
}
```

### **Exercise 3: Performance Optimization**
Create a data processing pipeline that optimizes dispatcher usage.

**Solution:**
```kotlin
import kotlinx.coroutines.*

class OptimizedDataProcessor {
    suspend fun processLargeDataset(data: List<String>): List<String> {
        return withContext(Dispatchers.IO) {
            println("Reading data on IO dispatcher: ${Thread.currentThread().name}")
            
            // Simulate reading large dataset
            delay(1000)
            
            // Process data in parallel with CPU dispatcher
            data.map { item ->
                async(Dispatchers.Default) {
                    processItem(item)
                }
            }.awaitAll()
        }
    }
    
    private suspend fun processItem(item: String): String {
        return withContext(Dispatchers.Default) {
            // CPU-intensive processing
            var result = 0
            repeat(100000) {
                result += item.hashCode() * it
            }
            "Processed: $item (hash: $result)"
        }
    }
}

fun main() = runBlocking {
    val processor = OptimizedDataProcessor()
    
    val data = List(10) { "Item$it" }
    val start = System.currentTimeMillis()
    
    val results = processor.processLargeDataset(data)
    
    val duration = System.currentTimeMillis() - start
    println("Processing completed in ${duration}ms")
    println("Results: ${results.take(3)}...")
}
```

### **Exercise 4: Context Management**
Implement a coroutine system with proper context lifecycle management.

**Solution:**
```kotlin
import kotlinx.coroutines.*
import java.util.concurrent.Executors

class ManagedCoroutineSystem {
    private val customDispatcher = Executors.newFixedThreadPool(4).asCoroutineDispatcher()
    private val exceptionHandler = CoroutineExceptionHandler { _, exception ->
        println("System exception: ${exception.message}")
    }
    
    suspend fun executeTask(taskName: String, duration: Long): String {
        return withContext(customDispatcher + exceptionHandler) {
            println("Executing $taskName on: ${Thread.currentThread().name}")
            delay(duration)
            "$taskName completed"
        }
    }
    
    suspend fun executeParallelTasks(tasks: List<Pair<String, Long>>): List<String> {
        return withContext(customDispatcher + exceptionHandler) {
            tasks.map { (name, duration) ->
                async {
                    executeTask(name, duration)
                }
            }.awaitAll()
        }
    }
    
    fun shutdown() {
        customDispatcher.close()
        println("System shutdown complete")
    }
}

fun main() = runBlocking {
    val system = ManagedCoroutineSystem()
    
    try {
        // Single task
        val result1 = system.executeTask("Quick Task", 500)
        println("Result: $result1")
        
        // Parallel tasks
        val tasks = listOf(
            "Task A" to 1000L,
            "Task B" to 800L,
            "Task C" to 1200L
        )
        
        val results = system.executeParallelTasks(tasks)
        println("Parallel results: $results")
        
    } finally {
        system.shutdown()
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Using wrong dispatcher**: Don't use IO for CPU work or Default for IO work ✅
2. **Forgetting context cleanup**: Always close custom dispatchers ✅
3. **Ignoring context inheritance**: Understand how context flows to children ✅
4. **Overusing Unconfined**: Only use for testing or special cases ✅

## 🎯 What's Next?

Now that you understand context and dispatchers, continue with:

1. **Sequential vs Concurrent** → [Sequential vs Concurrent](../coroutines/05-sequential-concurrent.md)
2. **Advanced Coroutines** → [Coroutine Scopes](../coroutines/06-coroutine-scopes.md)
3. **Exception Handling** → [Exception Handling](../coroutines/03-exception-handling.md)
4. **Functional Programming** → [Lambdas and Higher-Order Functions](../functional-programming/01-lambdas.md)

## 📚 Additional Resources

- [Official Coroutines Context Documentation](https://kotlinlang.org/docs/coroutine-context-and-dispatchers.html)
- [Dispatchers Guide](https://kotlinlang.org/docs/coroutine-context-and-dispatchers.html#dispatchers-and-threads)
- [Context Elements](https://kotlinlang.org/docs/coroutine-context-and-dispatchers.html#job-in-the-context)

## 🏆 Summary

- ✅ You understand coroutine context structure and elements
- ✅ You can use different dispatchers for various types of work
- ✅ You know how to combine context elements effectively
- ✅ You can manage coroutine lifecycle with context
- ✅ You're ready to optimize performance with appropriate dispatchers!

**Context and dispatchers are the foundation of efficient coroutine usage. Master them for optimal concurrent performance! 🎉**
