# 🎯 Object Declaration in Kotlin

Object declarations in Kotlin are a way to create singleton objects that are declared and initialized at the same time. They provide a convenient way to implement the Singleton pattern and organize utility functions and constants.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what object declarations are in Kotlin
- ✅ Create and use object declarations effectively
- ✅ Know when to use object declarations
- ✅ Implement singleton patterns
- ✅ Apply object declarations in real-world scenarios

## 🔍 What You'll Learn

- **Object declaration syntax** - How to declare and use object declarations
- **Singleton pattern** - Understanding singleton implementation
- **Utility objects** - Creating objects for utility functions
- **Companion objects** - Understanding companion object relationship
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of constructors and properties
- ✅ Familiarity with Kotlin syntax
- ✅ Understanding of object-oriented programming

## 💻 The Code

Let's examine the object declaration examples:

**📁 File:** [33_object_declaration.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/33_object_declaration.kt)

## 🔍 Code Breakdown

### **Basic Object Declaration**
```kotlin
object DatabaseConnection {
    private var connection: String? = null
    
    fun connect(url: String) {
        connection = url
        println("Connected to: $url")
    }
    
    fun disconnect() {
        connection = null
        println("Disconnected")
    }
}
```

**Key Components:**
- `object DatabaseConnection` - Object declaration
- `private var connection` - Private property
- `fun connect()` - Method for connecting
- `fun disconnect()` - Method for disconnecting

### **Object Usage**
```kotlin
// Usage
DatabaseConnection.connect("jdbc:postgresql://localhost:5432/mydb")
DatabaseConnection.disconnect()
```

## 🎯 Key Concepts Explained

### **1. What are Object Declarations?**

Object declarations in Kotlin:
- **Create singleton objects** - only one instance exists
- **Are initialized lazily** - when first accessed
- **Cannot have constructors** - they're instantiated automatically
- **Can inherit from classes** - but not from other objects
- **Provide thread-safe initialization** - by default

### **2. Object Declaration vs Class**

| Feature | Object Declaration | Class |
|---------|-------------------|-------|
| **Instances** | Single (singleton) | Multiple |
| **Constructor** | No | Yes |
| **Inheritance** | Can inherit from class | Can inherit from class |
| **Initialization** | Lazy, thread-safe | Manual |
| **Usage** | Direct access | Instantiation required |

### **3. Singleton Pattern Implementation**

```kotlin
object Singleton {
    private var instance: Singleton? = null
    
    fun getInstance(): Singleton {
        if (instance == null) {
            instance = Singleton
        }
        return instance!!
    }
}

// In Kotlin, this is automatic - no need for manual singleton pattern
```

## 🧪 Examples and Exercises

### **Example 1: Utility Object**
```kotlin
object StringUtils {
    fun reverse(text: String): String = text.reversed()
    
    fun capitalize(text: String): String = text.replaceFirstChar { it.uppercase() }
    
    fun countWords(text: String): Int = text.split("\\s+".toRegex()).size
    
    fun isPalindrome(text: String): Boolean {
        val cleanText = text.lowercase().replace(Regex("[^a-z0-9]"), "")
        return cleanText == cleanText.reversed()
    }
    
    fun truncate(text: String, maxLength: Int): String {
        return if (text.length <= maxLength) text else text.take(maxLength) + "..."
    }
}

// Usage
fun demonstrateStringUtils() {
    val text = "Hello World from Kotlin"
    
    println("Original: $text")
    println("Reversed: ${StringUtils.reverse(text)}")
    println("Capitalized: ${StringUtils.capitalize(text)}")
    println("Word count: ${StringUtils.countWords(text)}")
    println("Is palindrome: ${StringUtils.isPalindrome("racecar")}")
    println("Truncated: ${StringUtils.truncate(text, 15)}")
}
```

### **Example 2: Configuration Object**
```kotlin
object AppConfig {
    val appName: String = "Kotlin Tutorial App"
    val version: String = "1.0.0"
    val debug: Boolean = true
    
    val database: DatabaseConfig = DatabaseConfig()
    val api: ApiConfig = ApiConfig()
    
    fun getInfo(): String {
        return """
            App: $appName
            Version: $version
            Debug: $debug
            Database: ${database.getInfo()}
            API: ${api.getInfo()}
        """.trimIndent()
    }
}

data class DatabaseConfig(
    val host: String = "localhost",
    val port: Int = 5432,
    val name: String = "mydb"
) {
    fun getInfo(): String = "$host:$port/$name"
}

data class ApiConfig(
    val baseUrl: String = "https://api.example.com",
    val timeout: Int = 5000
) {
    fun getInfo(): String = "$baseUrl (timeout: ${timeout}ms)"
}

// Usage
fun demonstrateConfig() {
    println(AppConfig.getInfo())
    
    // Access specific configuration
    println("Database host: ${AppConfig.database.host}")
    println("API timeout: ${AppConfig.api.timeout}")
}
```

### **Example 3: Logger Object**
```kotlin
object Logger {
    private val logs: MutableList<LogEntry> = mutableListOf()
    private var logLevel: LogLevel = LogLevel.INFO
    
    enum class LogLevel {
        DEBUG, INFO, WARNING, ERROR
    }
    
    data class LogEntry(
        val level: LogLevel,
        val message: String,
        val timestamp: Long = System.currentTimeMillis()
    )
    
    fun setLogLevel(level: LogLevel) {
        logLevel = level
    }
    
    fun debug(message: String) = log(LogLevel.DEBUG, message)
    fun info(message: String) = log(LogLevel.INFO, message)
    fun warning(message: String) = log(LogLevel.WARNING, message)
    fun error(message: String) = log(LogLevel.ERROR, message)
    
    private fun log(level: LogLevel, message: String) {
        if (level.ordinal >= logLevel.ordinal) {
            val entry = LogEntry(level, message)
            logs.add(entry)
            println("[${level.name}] $message")
        }
    }
    
    fun getLogs(): List<LogEntry> = logs.toList()
    
    fun clearLogs() {
        logs.clear()
    }
    
    fun exportLogs(): String {
        return logs.joinToString("\n") { entry ->
            "[${entry.timestamp}] ${entry.level.name}: ${entry.message}"
        }
    }
}

// Usage
fun demonstrateLogger() {
    Logger.setLogLevel(Logger.LogLevel.DEBUG)
    
    Logger.debug("Application starting...")
    Logger.info("User logged in: john@example.com")
    Logger.warning("Low memory warning")
    Logger.error("Database connection failed")
    
    println("\nAll logs:")
    Logger.getLogs().forEach { println(it) }
    
    println("\nExported logs:")
    println(Logger.exportLogs())
}
```

### **Example 4: Cache Object**
```kotlin
object Cache {
    private val cache: MutableMap<String, CacheEntry> = mutableMapOf()
    private val maxSize: Int = 100
    private val defaultExpiry: Long = 300000 // 5 minutes
    
    data class CacheEntry(
        val value: Any,
        val timestamp: Long = System.currentTimeMillis(),
        val expiry: Long = defaultExpiry
    )
    
    fun put(key: String, value: Any, expiry: Long = defaultExpiry) {
        if (cache.size >= maxSize) {
            cleanup()
        }
        cache[key] = CacheEntry(value, System.currentTimeMillis(), expiry)
    }
    
    fun get(key: String): Any? {
        val entry = cache[key] ?: return null
        
        if (isExpired(entry)) {
            cache.remove(key)
            return null
        }
        
        return entry.value
    }
    
    fun remove(key: String) {
        cache.remove(key)
    }
    
    fun clear() {
        cache.clear()
    }
    
    fun size(): Int = cache.size
    
    private fun isExpired(entry: CacheEntry): Boolean {
        return System.currentTimeMillis() - entry.timestamp > entry.expiry
    }
    
    private fun cleanup() {
        val expiredKeys = cache.filter { isExpired(it.value) }.keys
        expiredKeys.forEach { cache.remove(it) }
        
        if (cache.size >= maxSize) {
            val oldestKey = cache.minByOrNull { it.value.timestamp }?.key
            oldestKey?.let { cache.remove(it) }
        }
    }
}

// Usage
fun demonstrateCache() {
    Cache.put("user:123", "John Doe")
    Cache.put("user:456", "Jane Smith", 600000) // 10 minutes expiry
    
    println("User 123: ${Cache.get("user:123")}")
    println("User 456: ${Cache.get("user:456")}")
    println("Cache size: ${Cache.size()}")
    
    Cache.remove("user:123")
    println("After removal - User 123: ${Cache.get("user:123")}")
    println("Cache size: ${Cache.size()}")
}
```

## ⚠️ Important Considerations

### **1. Object Declaration Limitations**
```kotlin
// ❌ Won't work - object cannot have constructor
object MyObject(val param: String) {
    // Error: Object cannot have constructor
}

// ❌ Won't work - object cannot be instantiated
val obj = MyObject()  // Error: Cannot create instance of object

// ❌ Won't work - object cannot inherit from object
object ParentObject
object ChildObject : ParentObject  // Error: Object cannot inherit from object

// ✅ Will work - object can inherit from class
open class ParentClass
object ChildObject : ParentClass  // This works
```

### **2. Thread Safety**
```kotlin
object ThreadSafeObject {
    private var counter: Int = 0
    
    @Synchronized
    fun increment() {
        counter++
    }
    
    fun getCount(): Int = counter
}

// Alternative using @Volatile
object VolatileObject {
    @Volatile
    private var flag: Boolean = false
    
    fun setFlag(value: Boolean) {
        flag = value
    }
    
    fun getFlag(): Boolean = flag
}
```

### **3. Object vs Companion Object**
```kotlin
class MyClass {
    companion object {
        fun create(): MyClass = MyClass()
        const val CONSTANT = "value"
    }
}

object MyObject {
    fun create(): MyClass = MyClass()
    const val CONSTANT = "value"
}

// Usage differences
val obj1 = MyClass.create()  // Through companion object
val obj2 = MyObject.create()  // Through object declaration
```

## 🎯 Best Practices

### **1. Use for Utility Functions**
```kotlin
// ✅ Good - utility functions
object MathUtils {
    fun factorial(n: Int): Long = if (n <= 1) 1 else n * factorial(n - 1)
    fun fibonacci(n: Int): Long = if (n <= 1) n else fibonacci(n - 1) + fibonacci(n - 2)
}

// ❌ Avoid - complex business logic
object BusinessLogic {
    fun processOrder(order: Order): OrderResult {
        // Complex business logic...
        return OrderResult()
    }
}
```

### **2. Use for Configuration**
```kotlin
// ✅ Good - configuration
object AppConfig {
    val databaseUrl: String = System.getenv("DB_URL") ?: "jdbc:default"
    val maxConnections: Int = System.getenv("MAX_CONN")?.toIntOrNull() ?: 10
}

// ❌ Avoid - mutable configuration
object BadConfig {
    var databaseUrl: String = "jdbc:default"  // Mutable
    var maxConnections: Int = 10  // Mutable
}
```

### **3. Use for Singleton Services**
```kotlin
// ✅ Good - singleton service
object DatabaseService {
    private var connection: Connection? = null
    
    fun getConnection(): Connection {
        if (connection == null || connection!!.isClosed) {
            connection = createConnection()
        }
        return connection!!
    }
    
    private fun createConnection(): Connection {
        // Connection creation logic
        return Connection()
    }
}

// ❌ Avoid - complex object with many responsibilities
object GodObject {
    fun doEverything() {
        // Too many responsibilities
    }
}
```

## 🔧 Practical Applications

### **1. Service Locator Pattern**
```kotlin
object ServiceLocator {
    private val services: MutableMap<Class<*>, Any> = mutableMapOf()
    
    fun <T> register(serviceClass: Class<T>, implementation: T) {
        services[serviceClass] = implementation
    }
    
    fun <T> get(serviceClass: Class<T>): T {
        return services[serviceClass] as T? 
            ?: throw IllegalStateException("Service not found: ${serviceClass.name}")
    }
}

// Usage
interface UserService {
    fun getUser(id: String): User
}

class UserServiceImpl : UserService {
    override fun getUser(id: String): User = User(id, "John Doe")
}

ServiceLocator.register(UserService::class.java, UserServiceImpl())
val userService = ServiceLocator.get(UserService::class.java)
```

### **2. Factory Pattern**
```kotlin
object AnimalFactory {
    fun createAnimal(type: String, name: String): Animal {
        return when (type.lowercase()) {
            "dog" -> Dog(name)
            "cat" -> Cat(name)
            "bird" -> Bird(name)
            else -> throw IllegalArgumentException("Unknown animal type: $type")
        }
    }
}

// Usage
val dog = AnimalFactory.createAnimal("dog", "Buddy")
val cat = AnimalFactory.createAnimal("cat", "Whiskers")
```

### **3. Registry Pattern**
```kotlin
object PluginRegistry {
    private val plugins: MutableMap<String, Plugin> = mutableMapOf()
    
    fun register(name: String, plugin: Plugin) {
        plugins[name] = plugin
    }
    
    fun get(name: String): Plugin? = plugins[name]
    
    fun getAll(): List<Plugin> = plugins.values.toList()
    
    fun unregister(name: String) {
        plugins.remove(name)
    }
}

interface Plugin {
    fun execute()
}

class DatabasePlugin : Plugin {
    override fun execute() = println("Database plugin executed")
}

class FilePlugin : Plugin {
    override fun execute() = println("File plugin executed")
}

// Usage
PluginRegistry.register("database", DatabasePlugin())
PluginRegistry.register("file", FilePlugin())

PluginRegistry.getAll().forEach { it.execute() }
```

## 📚 Summary

**Object declarations** in Kotlin provide:
- **Singleton pattern** implementation
- **Utility organization** for functions and constants
- **Thread-safe initialization** by default
- **Clean syntax** for single-instance objects
- **Configuration management** capabilities

## 🎯 Key Takeaways

1. **Use `object` keyword** for singleton declarations
2. **Objects are initialized lazily** when first accessed
3. **Objects cannot have constructors** or be instantiated
4. **Use for utilities, configuration, and services**
5. **Objects provide thread-safe initialization**

## 🚀 Next Steps

- Practice creating object declarations for different scenarios
- Learn about companion objects
- Explore object expressions
- Understand when to use objects vs classes

---

**📁 Source Code:** [33_object_declaration.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/33_object_declaration.kt)

**🔗 Related Topics:**
- [Data Class](../oop/10-data-class.md)
- [Companion Object](../oop/12-companion-object.md)
- [Classes and Constructors](../oop/01-classes-constructors.md)
