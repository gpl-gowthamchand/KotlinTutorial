# 🚨 Coroutine Exception Handling

This lesson covers how to handle exceptions in Kotlin coroutines. Exception handling in coroutines is crucial for building robust asynchronous applications that can gracefully handle errors and failures.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Handle exceptions in coroutines using try-catch blocks
- ✅ Use CoroutineExceptionHandler for global exception handling
- ✅ Understand exception propagation in coroutine hierarchies
- ✅ Implement proper error handling strategies
- ✅ Debug coroutine exceptions effectively

## 🔍 What You'll Learn

- **Exception handling basics** - Try-catch in coroutines
- **CoroutineExceptionHandler** - Global exception handling
- **Exception propagation** - How exceptions flow through coroutine scopes
- **Error recovery strategies** - Retry mechanisms and fallbacks
- **Debugging techniques** - Tools and best practices

## 📝 Prerequisites

- Understanding of [Coroutines Introduction](../coroutines/01-introduction.md)
- Knowledge of [Launch and Async](../coroutines/02-launch-async.md)
- Familiarity with [Basic Exception Handling](../basics/README.md)

## 💻 The Code

Let's examine the exception handling examples:

**📁 File:** [70_exception_handling.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/70_exception_handling.kt)

## 🔍 Code Breakdown

### **1. Basic Exception Handling in Coroutines**

#### **Try-Catch with Coroutines**
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    try {
        val result = async {
            delay(1000)
            throw RuntimeException("Something went wrong!")
        }.await()
        
        println("Result: $result")
    } catch (e: Exception) {
        println("Caught exception: ${e.message}")
    }
}
```

#### **Exception Handling with Launch**
```kotlin
fun main() = runBlocking {
    val job = launch {
        try {
            delay(1000)
            throw RuntimeException("Error in coroutine")
        } catch (e: Exception) {
            println("Caught in coroutine: ${e.message}")
        }
    }
    
    job.join()
    println("Coroutine completed")
}
```

### **2. CoroutineExceptionHandler**

#### **Global Exception Handler**
```kotlin
val exceptionHandler = CoroutineExceptionHandler { _, exception ->
    println("Coroutine exception: ${exception.message}")
    // Log the exception, send to monitoring service, etc.
}

fun main() = runBlocking {
    val job = GlobalScope.launch(exceptionHandler) {
        delay(1000)
        throw RuntimeException("Unhandled exception")
    }
    
    job.join()
    println("Main function completed")
}
```

#### **Exception Handler with Different Dispatchers**
```kotlin
val ioExceptionHandler = CoroutineExceptionHandler { _, exception ->
    println("IO Coroutine exception: ${exception.message}")
    // Handle IO-specific exceptions
}

val defaultExceptionHandler = CoroutineExceptionHandler { _, exception ->
    println("Default Coroutine exception: ${exception.message}")
    // Handle general exceptions
}

fun main() = runBlocking {
    // IO operations with specific exception handling
    val ioJob = launch(Dispatchers.IO + ioExceptionHandler) {
        delay(1000)
        throw IOException("IO operation failed")
    }
    
    // General operations with default exception handling
    val defaultJob = launch(Dispatchers.Default + defaultExceptionHandler) {
        delay(500)
        throw RuntimeException("General error")
    }
    
    ioJob.join()
    defaultJob.join()
}
```

### **3. Exception Propagation**

#### **Exception Propagation in Coroutine Hierarchy**
```kotlin
fun main() = runBlocking {
    val parentJob = launch {
        println("Parent coroutine started")
        
        val childJob = launch {
            println("Child coroutine started")
            delay(1000)
            throw RuntimeException("Child exception")
        }
        
        try {
            childJob.join()
        } catch (e: Exception) {
            println("Parent caught: ${e.message}")
        }
        
        println("Parent coroutine completed")
    }
    
    parentJob.join()
    println("All coroutines completed")
}
```

#### **Supervisor Scope Exception Handling**
```kotlin
fun main() = runBlocking {
    supervisorScope {
        val job1 = launch {
            delay(1000)
            throw RuntimeException("Job 1 failed")
        }
        
        val job2 = launch {
            delay(2000)
            println("Job 2 completed successfully")
        }
        
        try {
            job1.join()
        } catch (e: Exception) {
            println("Caught job1 exception: ${e.message}")
        }
        
        job2.join()
        println("Supervisor scope completed")
    }
}
```

### **4. Advanced Exception Handling Patterns**

#### **Retry Mechanism with Exponential Backoff**
```kotlin
suspend fun <T> retryWithBackoff(
    times: Int,
    initialDelay: Long = 100,
    factor: Double = 2.0,
    block: suspend () -> T
): T {
    var currentDelay = initialDelay
    repeat(times - 1) { attempt ->
        try {
            return block()
        } catch (e: Exception) {
            println("Attempt ${attempt + 1} failed: ${e.message}")
            if (attempt < times - 2) {
                delay(currentDelay)
                currentDelay = (currentDelay * factor).toLong()
            }
        }
    }
    return block() // Last attempt
}

fun main() = runBlocking {
    val result = retryWithBackoff(3) {
        delay(100)
        if (Math.random() < 0.7) {
            throw RuntimeException("Random failure")
        }
        "Success!"
    }
    
    println("Final result: $result")
}
```

#### **Exception Recovery with Fallback**
```kotlin
suspend fun fetchDataWithFallback(): String {
    return try {
        // Try primary data source
        fetchFromPrimarySource()
    } catch (e: Exception) {
        println("Primary source failed: ${e.message}")
        
        try {
            // Try secondary data source
            fetchFromSecondarySource()
        } catch (e2: Exception) {
            println("Secondary source failed: ${e2.message}")
            // Return default data
            "Default data"
        }
    }
}

suspend fun fetchFromPrimarySource(): String {
    delay(1000)
    throw RuntimeException("Primary source unavailable")
}

suspend fun fetchFromSecondarySource(): String {
    delay(500)
    throw RuntimeException("Secondary source unavailable")
}

fun main() = runBlocking {
    val data = fetchDataWithFallback()
    println("Final data: $data")
}
```

### **5. Exception Handling Best Practices**

#### **Structured Exception Handling**
```kotlin
class DataService {
    suspend fun processData(data: String): String {
        return withContext(Dispatchers.IO) {
            try {
                // Simulate data processing
                delay(1000)
                if (data.isEmpty()) {
                    throw IllegalArgumentException("Data cannot be empty")
                }
                "Processed: $data"
            } catch (e: Exception) {
                // Log the exception
                println("Data processing failed: ${e.message}")
                // Re-throw or return default value
                throw e
            }
        }
    }
}

fun main() = runBlocking {
    val service = DataService()
    
    try {
        val result = service.processData("")
        println("Result: $result")
    } catch (e: Exception) {
        println("Service error: ${e.message}")
    }
}
```

#### **Exception Handling in Parallel Operations**
```kotlin
suspend fun processItemsParallel(items: List<String>): List<String> {
    return items.map { item ->
        async {
            try {
                processItem(item)
            } catch (e: Exception) {
                println("Failed to process $item: ${e.message}")
                "Error processing $item"
            }
        }
    }.awaitAll()
}

suspend fun processItem(item: String): String {
    delay(100)
    if (item == "error") {
        throw RuntimeException("Cannot process error item")
    }
    return "Processed: $item"
}

fun main() = runBlocking {
    val items = listOf("item1", "error", "item3", "item4")
    val results = processItemsParallel(items)
    
    println("Results: $results")
}
```

## 🎯 Key Concepts Explained

### **1. Exception Propagation Rules**
- Exceptions in coroutines propagate to their parent
- Unhandled exceptions can crash the entire coroutine scope
- Use try-catch or CoroutineExceptionHandler to prevent crashes

### **2. CoroutineExceptionHandler vs Try-Catch**
```kotlin
// CoroutineExceptionHandler - handles uncaught exceptions
val handler = CoroutineExceptionHandler { _, exception ->
    println("Uncaught: ${exception.message}")
}

// Try-catch - handles exceptions within the coroutine
launch {
    try {
        // risky operation
    } catch (e: Exception) {
        // handle exception
    }
}
```

### **3. Exception Handling in Different Scopes**
- **GlobalScope**: Use CoroutineExceptionHandler
- **Structured concurrency**: Exceptions propagate to parent
- **SupervisorScope**: Exceptions don't affect siblings

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/70_exception_handling.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '70_exception_handlingKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Basic Exception Handling**
Create a coroutine that simulates a network call and handles exceptions.

**Solution:**
```kotlin
import kotlinx.coroutines.*

suspend fun simulateNetworkCall(url: String): String {
    delay(1000)
    if (url.contains("error")) {
        throw RuntimeException("Network error for $url")
    }
    return "Response from $url"
}

fun main() = runBlocking {
    val urls = listOf("https://api.example.com", "https://error.example.com", "https://success.example.com")
    
    urls.forEach { url ->
        try {
            val response = simulateNetworkCall(url)
            println("Success: $response")
        } catch (e: Exception) {
            println("Failed to fetch $url: ${e.message}")
        }
    }
}
```

### **Exercise 2: CoroutineExceptionHandler**
Implement a global exception handler for your application.

**Solution:**
```kotlin
import kotlinx.coroutines.*

class ApplicationExceptionHandler : CoroutineExceptionHandler {
    override val key = CoroutineExceptionHandler.Key
    
    override fun handleException(context: CoroutineContext, exception: Throwable) {
        when (exception) {
            is RuntimeException -> {
                println("Runtime error: ${exception.message}")
                // Log to monitoring service
            }
            is IOException -> {
                println("IO error: ${exception.message}")
                // Retry logic
            }
            else -> {
                println("Unknown error: ${exception.message}")
                // General error handling
            }
        }
    }
}

fun main() = runBlocking {
    val handler = ApplicationExceptionHandler()
    
    val job = GlobalScope.launch(handler) {
        delay(1000)
        throw RuntimeException("Application error")
    }
    
    job.join()
    println("Application completed")
}
```

### **Exercise 3: Exception Recovery**
Create a resilient data processing system that can recover from failures.

**Solution:**
```kotlin
import kotlinx.coroutines.*

class ResilientDataProcessor {
    suspend fun processWithRetry(data: String, maxRetries: Int = 3): String {
        var lastException: Exception? = null
        
        repeat(maxRetries) { attempt ->
            try {
                return processData(data)
            } catch (e: Exception) {
                lastException = e
                println("Attempt ${attempt + 1} failed: ${e.message}")
                if (attempt < maxRetries - 1) {
                    delay(1000 * (attempt + 1)) // Exponential backoff
                }
            }
        }
        
        throw lastException ?: RuntimeException("Unknown error")
    }
    
    private suspend fun processData(data: String): String {
        delay(500)
        if (Math.random() < 0.6) {
            throw RuntimeException("Processing failed")
        }
        return "Processed: $data"
    }
}

fun main() = runBlocking {
    val processor = ResilientDataProcessor()
    
    try {
        val result = processor.processWithRetry("important data")
        println("Success: $result")
    } catch (e: Exception) {
        println("All retries failed: ${e.message}")
    }
}
```

### **Exercise 4: Exception Handling in Parallel Operations**
Handle exceptions in multiple concurrent operations without failing the entire batch.

**Solution:**
```kotlin
import kotlinx.coroutines.*

data class ProcessingResult(val item: String, val success: Boolean, val result: String?, val error: String?)

suspend fun processBatchResilient(items: List<String>): List<ProcessingResult> {
    return items.map { item ->
        async {
            try {
                val result = processItem(item)
                ProcessingResult(item, true, result, null)
            } catch (e: Exception) {
                ProcessingResult(item, false, null, e.message)
            }
        }
    }.awaitAll()
}

suspend fun processItem(item: String): String {
    delay(200)
    if (item == "fail") {
        throw RuntimeException("Cannot process $item")
    }
    return "Processed: $item"
}

fun main() = runBlocking {
    val items = listOf("item1", "fail", "item3", "item4", "fail2")
    val results = processBatchResilient(items)
    
    results.forEach { result ->
        if (result.success) {
            println("✅ ${result.item}: ${result.result}")
        } else {
            println("❌ ${result.item}: ${result.error}")
        }
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Ignoring exceptions**: Always handle exceptions in coroutines ✅
2. **Using GlobalScope without exception handler**: Can crash your application ✅
3. **Not propagating exceptions**: Handle exceptions at the appropriate level ✅
4. **Forgetting structured concurrency**: Use proper coroutine scopes ✅

## 🎯 What's Next?

Now that you understand exception handling, continue with:

1. **Coroutine Context and Dispatchers** → [Coroutine Context and Dispatchers](../coroutines/04-context-dispatchers.md)
2. **Advanced Coroutines** → [Sequential vs Concurrent](../coroutines/05-sequential-concurrent.md)
3. **Scope Functions** → [Advanced Scope Functions](../functional-programming/03-let-also-run.md)
4. **Collections** → [Collections Overview](../collections/README.md)

## 📚 Additional Resources

- [Official Coroutines Exception Handling](https://kotlinlang.org/docs/exception-handling.html)
- [Coroutines Guide](https://kotlinlang.org/docs/coroutines-guide.html)
- [Exception Handling Best Practices](https://kotlinlang.org/docs/exception-handling.html#exception-handling)

## 🏆 Summary

- ✅ You can handle exceptions in coroutines using try-catch blocks
- ✅ You understand how to use CoroutineExceptionHandler for global handling
- ✅ You know how exceptions propagate in coroutine hierarchies
- ✅ You can implement proper error handling strategies
- ✅ You're ready to build robust asynchronous applications!

**Exception handling is crucial for production-ready coroutine applications. Master these patterns for bulletproof async code! 🎉**
