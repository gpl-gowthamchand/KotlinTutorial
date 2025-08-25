# ⏰ Lateinit and Lazy in Kotlin

The `lateinit` and `lazy` keywords are Kotlin's solutions for handling properties that need to be initialized later or on-demand. They provide different approaches to delayed initialization, each with their own use cases and benefits.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand when and how to use `lateinit` for delayed initialization
- ✅ Use `lazy` for on-demand initialization with caching
- ✅ Choose between `lateinit` and `lazy` for different scenarios
- ✅ Handle initialization checks and error cases
- ✅ Apply these patterns in real-world scenarios

## 🔍 What You'll Learn

- **Lateinit keyword** - Properties initialized after declaration
- **Lazy initialization** - Properties initialized on first access
- **Initialization timing** - When each approach initializes values
- **Use case scenarios** - When to use each approach
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- Understanding of [Null Safety](01-null-safety.md)
- Knowledge of [Variables and Data Types](../basics/02-variables-data-types.md)
- Familiarity with [Classes](../oop/01-classes-constructors.md)

## 💻 The Code

Let's examine the lateinit and lazy examples:

**📁 File:** [47_lateinit_keyword.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/47_lateinit_keyword.kt)

## 🔍 Code Breakdown

### **1. The `lateinit` Keyword**

#### **Basic Usage**
```kotlin
class UserManager {
    // Property declared but not initialized
    lateinit var userName: String
    
    // Property declared but not initialized
    lateinit var userEmail: String
    
    fun initializeUser(name: String, email: String) {
        // Initialize the properties later
        userName = name
        userEmail = email
    }
    
    fun getUserInfo(): String {
        // Check if initialized before use
        if (::userName.isInitialized && ::userEmail.isInitialized) {
            return "User: $userName, Email: $userEmail"
        }
        return "User not initialized"
    }
}
```

#### **Lateinit with Different Types**
```kotlin
class Configuration {
    // String properties
    lateinit var appName: String
    lateinit var version: String
    
    // Custom object properties
    lateinit var database: Database
    lateinit var logger: Logger
    
    // Array and collection properties
    lateinit var settings: Array<String>
    lateinit var users: List<User>
}
```

#### **Initialization Checks**
```kotlin
class DataProcessor {
    lateinit var dataSource: DataSource
    
    fun processData() {
        // Check if initialized before use
        if (::dataSource.isInitialized) {
            dataSource.process()
        } else {
            throw IllegalStateException("DataSource not initialized")
        }
    }
    
    fun safeProcessData() {
        // Safe access with initialization check
        if (::dataSource.isInitialized) {
            dataSource.process()
        } else {
            println("DataSource not ready, skipping processing")
        }
    }
}
```

### **2. The `lazy` Delegate**

#### **Basic Lazy Initialization**
```kotlin
class ExpensiveObject {
    // Property initialized on first access
    val expensiveValue by lazy {
        println("Computing expensive value...")
        // Simulate expensive computation
        Thread.sleep(1000)
        "Expensive computed result"
    }
    
    // Another lazy property
    val configuration by lazy {
        println("Loading configuration...")
        mapOf(
            "timeout" to 5000,
            "retries" to 3,
            "cacheSize" to 1000
        )
    }
}
```

#### **Lazy with Different Initialization Logic**
```kotlin
class UserService {
    // Lazy property with custom logic
    val userCache by lazy {
        println("Initializing user cache...")
        mutableMapOf<Int, User>()
    }
    
    // Lazy property with parameters
    val defaultUser by lazy {
        User(
            id = 0,
            name = "Default User",
            email = "default@example.com"
        )
    }
    
    // Lazy property with computation
    val userCount by lazy {
        println("Counting users...")
        userCache.size
    }
}
```

#### **Lazy with Thread Safety**
```kotlin
class ThreadSafeService {
    // Thread-safe lazy initialization
    val sharedResource by lazy(LazyThreadSafetyMode.SYNCHRONIZED) {
        println("Initializing shared resource...")
        "Thread-safe resource"
    }
    
    // Publication-safe lazy initialization (default)
    val safeResource by lazy(LazyThreadSafetyMode.PUBLICATION) {
        println("Initializing publication-safe resource...")
        "Publication-safe resource"
    }
    
    // Non-thread-safe lazy initialization
    val fastResource by lazy(LazyThreadSafetyMode.NONE) {
        println("Initializing fast resource...")
        "Fast resource"
    }
}
```

### **3. Comparing Lateinit vs Lazy**

#### **Initialization Timing**
```kotlin
class ComparisonExample {
    // Lateinit - must be initialized manually
    lateinit var lateinitProperty: String
    
    // Lazy - initialized on first access
    val lazyProperty by lazy {
        println("Lazy property initialized")
        "Lazy value"
    }
    
    fun demonstrateTiming() {
        println("1. Function started")
        
        // Lateinit property not accessed yet
        println("2. Lateinit property declared but not initialized")
        
        // Lazy property not accessed yet
        println("3. Lazy property declared but not initialized")
        
        // Access lazy property - triggers initialization
        println("4. Accessing lazy property: $lazyProperty")
        
        // Initialize lateinit property
        lateinitProperty = "Lateinit value"
        println("5. Lateinit property initialized: $lateinitProperty")
    }
}
```

#### **Use Case Examples**
```kotlin
class UseCaseExamples {
    // Use lateinit when:
    // - Property will be initialized by dependency injection
    // - Property will be set by external framework
    // - You need to control initialization timing
    
    lateinit var database: Database
    lateinit var networkService: NetworkService
    lateinit var userPreferences: UserPreferences
    
    // Use lazy when:
    // - Property is expensive to compute
    // - Property is not always needed
    // - You want automatic caching
    
    val expensiveCalculation by lazy {
        performExpensiveCalculation()
    }
    
    val cachedData by lazy {
        loadDataFromCache()
    }
    
    val defaultSettings by lazy {
        loadDefaultSettings()
    }
    
    private fun performExpensiveCalculation(): String {
        // Simulate expensive operation
        Thread.sleep(2000)
        return "Expensive result"
    }
    
    private fun loadDataFromCache(): Map<String, Any> {
        return mapOf("cached" to true, "timestamp" to System.currentTimeMillis())
    }
    
    private fun loadDefaultSettings(): Map<String, Any> {
        return mapOf("theme" to "dark", "language" to "en")
    }
}
```

### **4. Practical Examples**

#### **Dependency Injection Pattern**
```kotlin
class UserController {
    // Dependencies injected later
    lateinit var userService: UserService
    lateinit var authService: AuthService
    lateinit var logger: Logger
    
    fun initializeDependencies(
        userService: UserService,
        authService: AuthService,
        logger: Logger
    ) {
        this.userService = userService
        this.authService = authService
        this.logger = logger
    }
    
    fun createUser(userData: UserData): User {
        // Check if dependencies are initialized
        if (!::userService.isInitialized || !::authService.isInitialized) {
            throw IllegalStateException("Dependencies not initialized")
        }
        
        logger.log("Creating user: ${userData.name}")
        return userService.createUser(userData)
    }
}
```

#### **Configuration Management**
```kotlin
class AppConfiguration {
    // Configuration loaded on demand
    val databaseConfig by lazy {
        loadDatabaseConfig()
    }
    
    val apiConfig by lazy {
        loadApiConfig()
    }
    
    val featureFlags by lazy {
        loadFeatureFlags()
    }
    
    private fun loadDatabaseConfig(): DatabaseConfig {
        println("Loading database configuration...")
        return DatabaseConfig(
            host = "localhost",
            port = 5432,
            database = "myapp"
        )
    }
    
    private fun loadApiConfig(): ApiConfig {
        println("Loading API configuration...")
        return ApiConfig(
            baseUrl = "https://api.example.com",
            timeout = 30000,
            retries = 3
        )
    }
    
    private fun loadFeatureFlags(): Map<String, Boolean> {
        println("Loading feature flags...")
        return mapOf(
            "newUI" to true,
            "betaFeatures" to false,
            "analytics" to true
        )
    }
}
```

#### **Resource Management**
```kotlin
class ResourceManager {
    // Resources created on demand
    val connectionPool by lazy {
        createConnectionPool()
    }
    
    val cache by lazy {
        createCache()
    }
    
    val threadPool by lazy {
        createThreadPool()
    }
    
    private fun createConnectionPool(): ConnectionPool {
        println("Creating connection pool...")
        return ConnectionPool(maxConnections = 10)
    }
    
    private fun createCache(): Cache {
        println("Creating cache...")
        return Cache(maxSize = 1000)
    }
    
    private fun createThreadPool(): ThreadPool {
        println("Creating thread pool...")
        return ThreadPool(coreSize = 4, maxSize = 8)
    }
}

// Mock classes for demonstration
class ConnectionPool(val maxConnections: Int)
class Cache(val maxSize: Int)
class ThreadPool(val coreSize: Int, val maxSize: Int)
```

## 🎯 Key Concepts Explained

### **1. Lateinit Characteristics**
```kotlin
// Lateinit properties:
// - Must be declared as 'var' (mutable)
// - Cannot be nullable
// - Must be initialized before use
// - Can be changed after initialization
// - Use ::property.isInitialized to check status

class LateinitExample {
    lateinit var property: String
    
    fun initialize() {
        property = "Initial value"
    }
    
    fun changeValue() {
        property = "New value"  // Can be changed
    }
    
    fun checkStatus() {
        if (::property.isInitialized) {
            println("Property is initialized: $property")
        } else {
            println("Property is not initialized")
        }
    }
}
```

### **2. Lazy Characteristics**
```kotlin
// Lazy properties:
// - Must be declared as 'val' (immutable)
// - Initialized on first access
// - Cached for subsequent accesses
// - Thread-safe by default
// - Cannot be changed after initialization

class LazyExample {
    val property by lazy {
        println("Initializing...")
        "Computed value"
    }
    
    fun accessProperty() {
        println("First access: $property")  // Triggers initialization
        println("Second access: $property") // Uses cached value
    }
}
```

### **3. When to Use Each**

#### **Use `lateinit` when:**
- Property will be initialized by external code (DI, framework)
- You need to control initialization timing
- Property value will change after initialization
- Property is not always needed

#### **Use `lazy` when:**
- Property is expensive to compute
- Property should be cached after first access
- Property is not always needed
- You want automatic initialization

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/47_lateinit_keyword.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '47_lateinit_keywordKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Lateinit Property Management**
Create a class with lateinit properties and manage their lifecycle.

**Solution:**
```kotlin
class TaskManager {
    lateinit var taskExecutor: TaskExecutor
    lateinit var taskQueue: TaskQueue
    lateinit var logger: Logger
    
    fun initialize(executor: TaskExecutor, queue: TaskQueue, log: Logger) {
        taskExecutor = executor
        taskQueue = queue
        logger = log
    }
    
    fun executeTask(task: Task) {
        if (!::taskExecutor.isInitialized || !::taskQueue.isInitialized) {
            throw IllegalStateException("TaskManager not initialized")
        }
        
        logger.log("Executing task: ${task.name}")
        taskQueue.add(task)
        taskExecutor.execute(task)
    }
    
    fun isReady(): Boolean {
        return ::taskExecutor.isInitialized && 
               ::taskQueue.isInitialized && 
               ::logger.isInitialized
    }
}

// Mock classes
class Task(val name: String)
class TaskExecutor { fun execute(task: Task) {} }
class TaskQueue { fun add(task: Task) {} }
class Logger { fun log(message: String) {} }

fun main() {
    val manager = TaskManager()
    
    println("Manager ready: ${manager.isReady()}")
    
    try {
        manager.executeTask(Task("Test Task"))
    } catch (e: Exception) {
        println("Error: ${e.message}")
    }
    
    manager.initialize(TaskExecutor(), TaskQueue(), Logger())
    println("Manager ready: ${manager.isReady()}")
    
    manager.executeTask(Task("Test Task"))
}
```

### **Exercise 2: Lazy Configuration Loading**
Implement a configuration system using lazy initialization.

**Solution:**
```kotlin
class ConfigurationLoader {
    val databaseConfig by lazy {
        println("Loading database config...")
        loadFromFile("database.properties")
    }
    
    val apiConfig by lazy {
        println("Loading API config...")
        loadFromFile("api.properties")
    }
    
    val userConfig by lazy {
        println("Loading user config...")
        loadFromFile("user.properties")
    }
    
    private fun loadFromFile(filename: String): Map<String, String> {
        // Simulate file loading
        Thread.sleep(500)
        return mapOf(
            "filename" to filename,
            "loaded" to "true",
            "timestamp" to System.currentTimeMillis().toString()
        )
    }
}

fun main() {
    val config = ConfigurationLoader()
    
    println("Configuration object created")
    
    // Access properties - triggers lazy initialization
    println("Database config: ${config.databaseConfig}")
    println("API config: ${config.apiConfig}")
    
    // Second access uses cached values
    println("Database config again: ${config.databaseConfig}")
    println("User config: ${config.userConfig}")
}
```

### **Exercise 3: Resource Management with Lazy**
Create a resource manager that initializes resources on demand.

**Solution:**
```kotlin
class ResourceManager {
    val database by lazy {
        println("Initializing database connection...")
        Database("localhost", 5432)
    }
    
    val cache by lazy {
        println("Initializing cache...")
        Cache(1000)
    }
    
    val httpClient by lazy {
        println("Initializing HTTP client...")
        HttpClient("https://api.example.com")
    }
    
    fun processRequest(request: String) {
        // Resources are initialized only when needed
        if (request.startsWith("db:")) {
            database.query(request.substring(3))
        } else if (request.startsWith("cache:")) {
            cache.get(request.substring(6))
        } else if (request.startsWith("http:")) {
            httpClient.get(request.substring(5))
        }
    }
}

// Mock classes
class Database(val host: String, val port: Int) {
    fun query(query: String) = println("Database query: $query")
}
class Cache(val size: Int) {
    fun get(key: String) = println("Cache get: $key")
}
class HttpClient(val baseUrl: String) {
    fun get(path: String) = println("HTTP GET: $baseUrl$path")
}

fun main() {
    val manager = ResourceManager()
    
    println("Resource manager created")
    
    // Process different types of requests
    manager.processRequest("db:SELECT * FROM users")
    manager.processRequest("cache:user:123")
    manager.processRequest("http:/api/users")
    
    // Process another database request - uses existing connection
    manager.processRequest("db:SELECT COUNT(*) FROM users")
}
```

### **Exercise 4: Combined Lateinit and Lazy**
Create a service that uses both lateinit and lazy properties.

**Solution:**
```kotlin
class UserService {
    // Dependencies injected later
    lateinit var userRepository: UserRepository
    lateinit var emailService: EmailService
    
    // Computed properties initialized on demand
    val userCache by lazy {
        println("Initializing user cache...")
        mutableMapOf<Int, User>()
    }
    
    val defaultUser by lazy {
        println("Creating default user...")
        User(0, "Default", "default@example.com")
    }
    
    fun initialize(repository: UserRepository, emailService: EmailService) {
        this.userRepository = repository
        this.emailService = emailService
    }
    
    fun createUser(name: String, email: String): User {
        if (!::userRepository.isInitialized) {
            throw IllegalStateException("UserRepository not initialized")
        }
        
        val user = userRepository.createUser(name, email)
        userCache[user.id] = user
        emailService.sendWelcomeEmail(user.email)
        
        return user
    }
    
    fun getUser(id: Int): User? {
        return userCache[id] ?: userRepository.getUser(id)
    }
    
    fun getDefaultUser(): User {
        return defaultUser
    }
}

// Mock classes
class User(val id: Int, val name: String, val email: String)
class UserRepository {
    fun createUser(name: String, email: String) = User(1, name, email)
    fun getUser(id: Int) = User(id, "Unknown", "unknown@example.com")
}
class EmailService {
    fun sendWelcomeEmail(email: String) = println("Welcome email sent to $email")
}

fun main() {
    val service = UserService()
    
    try {
        service.createUser("Alice", "alice@example.com")
    } catch (e: Exception) {
        println("Error: ${e.message}")
    }
    
    // Initialize dependencies
    service.initialize(UserRepository(), EmailService())
    
    // Now it should work
    val user = service.createUser("Alice", "alice@example.com")
    println("Created user: ${user.name}")
    
    // Access lazy properties
    val defaultUser = service.getDefaultUser()
    println("Default user: ${defaultUser.name}")
}
```

## 🚨 Common Mistakes to Avoid

1. **Using lateinit with nullable types**: `lateinit var property: String?` ❌
   - **Correct**: `lateinit var property: String` ✅

2. **Forgetting to initialize lateinit properties**: Accessing before initialization ❌
   - **Correct**: Always check `::property.isInitialized` ✅

3. **Using lazy with var**: `var property by lazy { ... }` ❌
   - **Correct**: `val property by lazy { ... }` ✅

4. **Ignoring thread safety**: Using lazy in multi-threaded environments without considering thread safety ✅

## 🎯 What's Next?

Now that you understand lateinit and lazy, continue with:

1. **Scope Functions** → [Scope Functions](../functional-programming/02-scope-functions.md)
2. **Collections** → [Collections Overview](../collections/README.md)
3. **Coroutines** → [Coroutines](../coroutines/01-introduction.md)
4. **Advanced OOP** → [Object-Oriented Programming](../oop/README.md)

## 📚 Additional Resources

- [Official Kotlin Lateinit Documentation](https://kotlinlang.org/docs/properties.html#late-initialized-properties-and-variables)
- [Official Kotlin Lazy Documentation](https://kotlinlang.org/docs/delegated-properties.html#lazy-properties)
- [Kotlin Properties Guide](https://kotlinlang.org/docs/properties.html)

## 🏆 Summary

- ✅ You understand when and how to use `lateinit` for delayed initialization
- ✅ You can use `lazy` for on-demand initialization with caching
- ✅ You know how to choose between `lateinit` and `lazy` for different scenarios
- ✅ You can handle initialization checks and error cases
- ✅ You're ready to implement efficient initialization patterns!

**Lateinit and lazy provide powerful ways to manage property initialization. Use them to create more efficient and flexible code! 🎉**
