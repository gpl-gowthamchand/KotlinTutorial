# 🚀 Launch and Async Coroutines in Kotlin

`launch` and `async` are the two main coroutine builders in Kotlin. They allow you to start coroutines in different ways depending on whether you need to return a result or just execute some work in the background.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Use `launch` for fire-and-forget coroutines
- ✅ Use `async` for coroutines that return results
- ✅ Understand the difference between `launch` and `async`
- ✅ Handle coroutine jobs and deferred results
- ✅ Implement parallel execution patterns

## 🔍 What You'll Learn

- **Launch coroutines** - Fire-and-forget background execution
- **Async coroutines** - Coroutines that return results
- **Job management** - Controlling coroutine lifecycle
- **Parallel execution** - Running multiple coroutines simultaneously
- **Result handling** - Working with deferred results

## 📝 Prerequisites

- Understanding of [Introduction to Coroutines](01-introduction.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Collections](../collections/01-arrays.md)

## 💻 The Code

Let's examine the launch and async examples:

**📁 File:** [64_launch_coroutine_builder.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/64_launch_coroutine_builder.kt)

## 🔍 Code Breakdown

### **1. The `launch` Coroutine Builder**

#### **Basic Launch Usage**
```kotlin
fun main() {
    println("Starting main function")
    
    // Launch a coroutine that doesn't return a value
    val job = GlobalScope.launch {
        println("Coroutine started")
        delay(1000)
        println("Coroutine completed")
    }
    
    println("Main function continues")
    job.join()  // Wait for coroutine to complete
    println("Main function finished")
}
```

#### **Launch with Different Dispatchers**
```kotlin
fun main() {
    runBlocking {
        println("Main thread: ${Thread.currentThread().name}")
        
        // Launch on IO dispatcher
        val ioJob = launch(Dispatchers.IO) {
            println("IO coroutine on: ${Thread.currentThread().name}")
            delay(1000)
            println("IO work completed")
        }
        
        // Launch on Default dispatcher
        val defaultJob = launch(Dispatchers.Default) {
            println("Default coroutine on: ${Thread.currentThread().name}")
            delay(500)
            println("Default work completed")
        }
        
        // Launch on Main dispatcher
        val mainJob = launch(Dispatchers.Main) {
            println("Main coroutine on: ${Thread.currentThread().name}")
            delay(300)
            println("Main work completed")
        }
        
        // Wait for all to complete
        ioJob.join()
        defaultJob.join()
        mainJob.join()
    }
}
```

#### **Launch with Job Management**
```kotlin
fun main() {
    runBlocking {
        // Create a parent job
        val parentJob = Job()
        
        // Launch child coroutines
        val child1 = launch(parentJob) {
            println("Child 1 started")
            delay(1000)
            println("Child 1 completed")
        }
        
        val child2 = launch(parentJob) {
            println("Child 2 started")
            delay(1500)
            println("Child 2 completed")
        }
        
        // Cancel parent job after 500ms
        delay(500)
        parentJob.cancel()
        
        try {
            child1.join()
            child2.join()
        } catch (e: CancellationException) {
            println("Coroutines were cancelled")
        }
    }
}
```

### **2. The `async` Coroutine Builder**

#### **Basic Async Usage**
```kotlin
fun main() {
    runBlocking {
        println("Starting async operations")
        
        // Launch async coroutine that returns a result
        val deferred = async {
            println("Async operation started")
            delay(1000)
            "Async result"
        }
        
        println("Main continues while async runs")
        val result = deferred.await()  // Wait for result
        println("Got result: $result")
    }
}
```

#### **Multiple Async Operations**
```kotlin
fun main() {
    runBlocking {
        println("Starting multiple async operations")
        
        val startTime = System.currentTimeMillis()
        
        // Launch multiple async coroutines
        val deferred1 = async { fetchData(1) }
        val deferred2 = async { fetchData(2) }
        val deferred3 = async { fetchData(3) }
        
        // Wait for all results
        val result1 = deferred1.await()
        val result2 = deferred2.await()
        val result3 = deferred3.await()
        
        val endTime = System.currentTimeMillis()
        
        println("Results: $result1, $result2, $result3")
        println("Total time: ${endTime - startTime}ms")
    }
}

suspend fun fetchData(id: Int): String {
    delay(1000)  // Simulate network call
    return "Data for ID: $id"
}
```

#### **Async with Error Handling**
```kotlin
fun main() {
    runBlocking {
        try {
            val deferred = async {
                // Simulate operation that might fail
                if (Math.random() < 0.5) {
                    throw RuntimeException("Random failure")
                }
                "Success result"
            }
            
            val result = deferred.await()
            println("Operation succeeded: $result")
            
        } catch (e: Exception) {
            println("Operation failed: ${e.message}")
        }
    }
}
```

### **3. Comparing Launch vs Async**

#### **Key Differences**
```kotlin
fun demonstrateDifferences() {
    runBlocking {
        println("=== Launch vs Async Comparison ===")
        
        // Launch - fire and forget, returns Job
        val launchJob = launch {
            delay(1000)
            println("Launch coroutine completed")
        }
        
        // Async - returns result, returns Deferred
        val asyncDeferred = async {
            delay(1000)
            "Async coroutine result"
        }
        
        // Launch doesn't return a value
        println("Launch job type: ${launchJob::class.simpleName}")
        
        // Async returns a Deferred<T>
        println("Async deferred type: ${asyncDeferred::class.simpleName}")
        
        // Wait for both to complete
        launchJob.join()
        val result = asyncDeferred.await()
        println("Async result: $result")
    }
}
```

#### **Use Case Examples**
```kotlin
class UseCaseExamples {
    // Use launch when:
    // - You don't need a return value
    // - You want fire-and-forget execution
    // - You need to perform side effects
    
    fun performBackgroundTask() {
        GlobalScope.launch {
            // Perform some background work
            delay(1000)
            println("Background task completed")
        }
    }
    
    // Use async when:
    // - You need a return value
    // - You want to compose results
    // - You need to run operations in parallel
    
    suspend fun fetchUserData(userId: Int): User {
        val userDeferred = async { fetchUser(userId) }
        val postsDeferred = async { fetchUserPosts(userId) }
        val settingsDeferred = async { fetchUserSettings(userId) }
        
        val user = userDeferred.await()
        val posts = postsDeferred.await()
        val settings = settingsDeferred.await()
        
        return user.copy(posts = posts, settings = settings)
    }
    
    private suspend fun fetchUser(id: Int): User = User(id, "User $id")
    private suspend fun fetchUserPosts(id: Int): List<Post> = listOf(Post("Post 1"))
    private suspend fun fetchUserSettings(id: Int): UserSettings = UserSettings()
}

// Mock classes
data class User(val id: Int, val name: String, val posts: List<Post> = emptyList(), val settings: UserSettings = UserSettings())
data class Post(val title: String)
class UserSettings
```

### **4. Advanced Patterns**

#### **Structured Concurrency**
```kotlin
fun main() {
    runBlocking {
        // Create a coroutine scope
        coroutineScope {
            val deferred1 = async { fetchData(1) }
            val deferred2 = async { fetchData(2) }
            
            // If any coroutine fails, all are cancelled
            try {
                val result1 = deferred1.await()
                val result2 = deferred2.await()
                println("Both succeeded: $result1, $result2")
            } catch (e: Exception) {
                println("One or both failed: ${e.message}")
            }
        }
    }
}

suspend fun fetchData(id: Int): String {
    delay(1000)
    if (id == 2 && Math.random() < 0.5) {
        throw RuntimeException("Random failure for ID 2")
    }
    return "Data $id"
}
```

#### **Supervisor Scope**
```kotlin
fun main() {
    runBlocking {
        // Supervisor scope - child failures don't affect siblings
        supervisorScope {
            val deferred1 = async { fetchData(1) }
            val deferred2 = async { fetchData(2) }
            val deferred3 = async { fetchData(3) }
            
            // Collect results, ignoring failures
            val results = listOf(deferred1, deferred2, deferred3)
                .mapNotNull { deferred ->
                    try {
                        deferred.await()
                    } catch (e: Exception) {
                        println("Failed: ${e.message}")
                        null
                    }
                }
            
            println("Successful results: $results")
        }
    }
}
```

#### **Lazy Async**
```kotlin
fun main() {
    runBlocking {
        // Lazy async - only starts when awaited
        val lazyDeferred = async(start = CoroutineStart.LAZY) {
            println("Lazy async started")
            delay(1000)
            "Lazy result"
        }
        
        println("Lazy async created but not started")
        delay(500)
        
        println("Now starting lazy async")
        val result = lazyDeferred.await()
        println("Got result: $result")
    }
}
```

### **5. Practical Examples**

#### **Parallel Data Processing**
```kotlin
fun main() {
    runBlocking {
        val items = (1..10).toList()
        
        println("Processing ${items.size} items sequentially...")
        val sequentialStart = System.currentTimeMillis()
        val sequentialResults = items.map { processItem(it) }
        val sequentialTime = System.currentTimeMillis() - sequentialStart
        
        println("Sequential time: ${sequentialTime}ms")
        
        println("Processing ${items.size} items in parallel...")
        val parallelStart = System.currentTimeMillis()
        val deferredResults = items.map { async { processItem(it) } }
        val parallelResults = deferredResults.awaitAll()
        val parallelTime = System.currentTimeMillis() - parallelStart
        
        println("Parallel time: ${parallelTime}ms")
        println("Speedup: ${sequentialTime.toDouble() / parallelTime}")
    }
}

suspend fun processItem(item: Int): String {
    delay(100)  // Simulate processing time
    return "Processed item $item"
}
```

#### **Concurrent API Calls**
```kotlin
fun main() {
    runBlocking {
        val userIds = listOf(1, 2, 3, 4, 5)
        
        println("Fetching user data for ${userIds.size} users...")
        
        // Fetch all user data concurrently
        val userDeferreds = userIds.map { id ->
            async {
                fetchUserData(id)
            }
        }
        
        // Wait for all results
        val users = userDeferreds.awaitAll()
        
        // Process results
        users.forEach { user ->
            println("User: ${user.name}, Posts: ${user.postCount}")
        }
    }
}

suspend fun fetchUserData(userId: Int): UserData {
    delay(500)  // Simulate API call
    return UserData("User $userId", (1..5).random())
}

data class UserData(val name: String, val postCount: Int)
```

## 🎯 Key Concepts Explained

### **1. Launch vs Async Summary**
```kotlin
// Launch:
// - Returns Job
// - Fire and forget
// - No return value
// - Good for side effects

// Async:
// - Returns Deferred<T>
// - Returns a result
// - Can be awaited
// - Good for parallel execution
```

### **2. Job Lifecycle**
```kotlin
val job = launch {
    // Coroutine body
}

// Job states: New -> Active -> Completing -> Completed
// Can be cancelled at any time

job.cancel()  // Cancel the job
job.join()    // Wait for completion
job.isActive  // Check if active
job.isCompleted  // Check if completed
```

### **3. Deferred Results**
```kotlin
val deferred = async {
    "Result"
}

// Deferred is a Job that can return a value
deferred.await()  // Wait for and get the result
deferred.isCompleted  // Check if completed
deferred.getCompleted()  // Get result if completed
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/64_launch_coroutine_builder.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '64_launch_coroutine_builderKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Basic Launch and Async**
Create and manage basic launch and async coroutines.

**Solution:**
```kotlin
fun main() {
    runBlocking {
        println("Starting exercise")
        
        // Launch a background task
        val backgroundJob = launch {
            repeat(5) {
                delay(200)
                println("Background task iteration $it")
            }
        }
        
        // Async task that returns a result
        val resultDeferred = async {
            delay(1000)
            "Async computation result"
        }
        
        // Wait for background task
        backgroundJob.join()
        println("Background task completed")
        
        // Get async result
        val result = resultDeferred.await()
        println("Async result: $result")
        
        println("Exercise completed")
    }
}
```

### **Exercise 2: Parallel Processing**
Process multiple items in parallel using async.

**Solution:**
```kotlin
fun main() {
    runBlocking {
        val items = listOf("Apple", "Banana", "Cherry", "Date", "Elderberry")
        
        println("Processing items: $items")
        
        // Process all items in parallel
        val processingDeferreds = items.map { item ->
            async {
                processItem(item)
            }
        }
        
        // Wait for all results
        val results = processingDeferreds.awaitAll()
        
        println("Processing results:")
        results.forEach { (item, processed) ->
            println("$item -> $processed")
        }
    }
}

suspend fun processItem(item: String): Pair<String, String> {
    delay(500)  // Simulate processing time
    val processed = item.uppercase().reversed()
    return item to processed
}
```

### **Exercise 3: Error Handling with Async**
Handle errors in async coroutines gracefully.

**Solution:**
```kotlin
fun main() {
    runBlocking {
        val operations = listOf(1, 2, 3, 4, 5)
        
        println("Starting operations: $operations")
        
        // Launch operations with error handling
        val results = operations.map { id ->
            async {
                try {
                    performOperation(id)
                } catch (e: Exception) {
                    "Failed: ${e.message}"
                }
            }
        }
        
        // Collect all results
        val completedResults = results.awaitAll()
        
        println("Operation results:")
        completedResults.forEachIndexed { index, result ->
            println("Operation ${operations[index]}: $result")
        }
    }
}

suspend fun performOperation(id: Int): String {
    delay(200)
    
    // Simulate random failures
    if (id % 3 == 0) {
        throw RuntimeException("Operation $id failed")
    }
    
    return "Operation $id completed successfully"
}
```

### **Exercise 4: Structured Concurrency**
Implement structured concurrency patterns.

**Solution:**
```kotlin
fun main() {
    runBlocking {
        println("Starting structured concurrency example")
        
        // Use coroutineScope for structured concurrency
        val result = coroutineScope {
            val userDeferred = async { fetchUser(123) }
            val postsDeferred = async { fetchPosts(123) }
            val settingsDeferred = async { fetchSettings(123) }
            
            // All coroutines must complete successfully
            val user = userDeferred.await()
            val posts = postsDeferred.await()
            val settings = settingsDeferred.await()
            
            UserProfile(user, posts, settings)
        }
        
        println("User profile created: ${result.user.name}")
        println("Posts count: ${result.posts.size}")
        println("Settings: ${result.settings}")
    }
}

suspend fun fetchUser(id: Int): User {
    delay(300)
    return User(id, "User $id")
}

suspend fun fetchPosts(userId: Int): List<Post> {
    delay(400)
    return listOf(Post("Post 1"), Post("Post 2"))
}

suspend fun fetchSettings(userId: Int): UserSettings {
    delay(200)
    return UserSettings(theme = "dark", notifications = true)
}

data class UserProfile(val user: User, val posts: List<Post>, val settings: UserSettings)
data class User(val id: Int, val name: String)
data class Post(val title: String)
data class UserSettings(val theme: String, val notifications: Boolean)
```

## 🚨 Common Mistakes to Avoid

1. **Forgetting to await async results**: Results won't be available ✅
2. **Using GlobalScope in production**: Can lead to memory leaks ✅
3. **Not handling exceptions**: Async coroutines can fail ✅
4. **Ignoring structured concurrency**: Use coroutineScope for proper lifecycle management ✅

## 🎯 What's Next?

Now that you understand launch and async, continue with:

1. **Exception Handling** → [Coroutine Exception Handling](03-exception-handling.md)
2. **Coroutine Context** → [Coroutine Context and Dispatchers](04-context-dispatchers.md)
3. **Advanced Patterns** → [Advanced Coroutine Patterns](05-advanced-patterns.md)
4. **Collections** → [Collections Overview](../collections/README.md)

## 📚 Additional Resources

- [Official Kotlin Coroutines Documentation](https://kotlinlang.org/docs/coroutines-overview.html)
- [Coroutine Builders](https://kotlinlang.org/docs/coroutines-basics.html#coroutine-builders)
- [Async Coroutines](https://kotlinlang.org/docs/coroutines-basics.html#async-coroutines)

## 🏆 Summary

- ✅ You can use `launch` for fire-and-forget coroutines
- ✅ You can use `async` for coroutines that return results
- ✅ You understand the difference between `launch` and `async`
- ✅ You can handle coroutine jobs and deferred results
- ✅ You're ready to implement parallel execution patterns!

**Launch and async are the foundation of coroutine programming. Use them to build responsive, concurrent applications! 🎉**
