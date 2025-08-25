# 🏗️ INIT Block in Kotlin

The `init` block in Kotlin is a special initialization block that runs when an object is created. It's part of the primary constructor and allows you to execute initialization logic during object creation.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what the init block is
- ✅ Create and use init blocks effectively
- ✅ Know when to use init blocks
- ✅ Understand the execution order
- ✅ Apply init blocks in real-world scenarios

## 🔍 What You'll Learn

- **Init block syntax** - How to declare and use init blocks
- **Initialization order** - Understanding when init blocks execute
- **Use cases** - When and where to use init blocks
- **Best practices** - Guidelines for effective usage
- **Common patterns** - Typical initialization scenarios

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of constructors
- ✅ Familiarity with Kotlin syntax
- ✅ Understanding of object-oriented programming

## 💻 The Code

Let's examine the init block examples:

**📁 File:** [26_class_and_constructor.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/26_class_and_constructor.kt)

## 🔍 Code Breakdown

### **Basic Init Block Declaration**
```kotlin
class Person(val name: String, val age: Int) {
    init {
        println("Creating a new Person: $name, age $age")
    }
}
```

**Key Components:**
- `class Person` - Class declaration
- `val name: String, val age: Int` - Primary constructor parameters
- `init { }` - Initialization block
- `println(...)` - Initialization logic

### **Init Block with Validation**
```kotlin
class Student(val name: String, val age: Int) {
    init {
        require(age >= 0) { "Age cannot be negative" }
        require(name.isNotBlank()) { "Name cannot be empty" }
        println("Student $name created successfully")
    }
}
```

## 🎯 Key Concepts Explained

### **1. What is the Init Block?**

The `init` block is:
- **Part of the primary constructor** - runs when object is created
- **An initialization block** - executes setup code
- **Executed in order** - multiple init blocks run sequentially
- **Access to constructor parameters** - can use all constructor values

### **2. When Init Blocks Execute**

Init blocks execute:
- **During object creation** - when constructor is called
- **After constructor parameters** - have been assigned
- **Before object is ready** - for use
- **In declaration order** - multiple init blocks run sequentially

### **3. Execution Order**

```kotlin
class Example(val param: String) {
    init {
        println("First init block: $param")
    }
    
    val property = "Property initialized"
    
    init {
        println("Second init block: $param, $property")
    }
}

// Execution order:
// 1. Constructor parameters assigned
// 2. First init block executes
// 3. Properties initialized
// 4. Second init block executes
// 5. Object ready for use
```

## 🧪 Examples and Exercises

### **Example 1: Basic Initialization**
```kotlin
class Rectangle(val width: Int, val height: Int) {
    init {
        println("Creating rectangle: ${width}x${height}")
    }
    
    val area: Int = width * height
    
    init {
        println("Rectangle area: $area")
    }
}

// Usage
val rect = Rectangle(5, 3)
// Output:
// Creating rectangle: 5x3
// Rectangle area: 15
```

### **Example 2: Parameter Validation**
```kotlin
class BankAccount(val accountNumber: String, val initialBalance: Double) {
    init {
        require(accountNumber.isNotBlank()) { "Account number cannot be empty" }
        require(initialBalance >= 0) { "Initial balance cannot be negative" }
        require(accountNumber.length >= 8) { "Account number must be at least 8 characters" }
    }
    
    var balance = initialBalance
        private set
    
    fun deposit(amount: Double) {
        require(amount > 0) { "Deposit amount must be positive" }
        balance += amount
    }
    
    fun withdraw(amount: Double) {
        require(amount > 0) { "Withdrawal amount must be positive" }
        require(amount <= balance) { "Insufficient funds" }
        balance -= amount
    }
}

// Usage
val account = BankAccount("12345678", 1000.0)
account.deposit(500.0)
account.withdraw(200.0)
println("Balance: ${account.balance}")  // 1300.0
```

### **Example 3: Complex Initialization**
```kotlin
class DatabaseConnection(
    val host: String,
    val port: Int,
    val database: String,
    val username: String,
    val password: String
) {
    private val connectionString: String
    
    init {
        // Validate connection parameters
        require(host.isNotBlank()) { "Host cannot be empty" }
        require(port in 1..65535) { "Port must be between 1 and 65535" }
        require(database.isNotBlank()) { "Database name cannot be empty" }
        
        // Build connection string
        connectionString = "jdbc:postgresql://$host:$port/$database"
        
        // Log connection attempt
        println("Attempting to connect to: $connectionString")
    }
    
    fun connect(): Boolean {
        // Simulate connection logic
        println("Connected to database: $database on $host:$port")
        return true
    }
}

// Usage
val db = DatabaseConnection("localhost", 5432, "mydb", "user", "pass")
db.connect()
```

### **Example 4: Lazy Initialization with Init**
```kotlin
class Configuration(val configFile: String) {
    private val config: Map<String, String>
    
    init {
        // Load configuration from file
        config = try {
            readConfigFile(configFile)
        } catch (e: Exception) {
            println("Failed to load config file: ${e.message}")
            emptyMap()
        }
        
        // Validate required configuration
        val requiredKeys = listOf("database_url", "api_key", "timeout")
        val missingKeys = requiredKeys.filter { !config.containsKey(it) }
        
        if (missingKeys.isNotEmpty()) {
            println("Warning: Missing required configuration keys: $missingKeys")
        }
    }
    
    fun get(key: String): String? = config[key]
    
    private fun readConfigFile(filename: String): Map<String, String> {
        // Simulate reading config file
        return mapOf(
            "database_url" to "jdbc:postgresql://localhost:5432/mydb",
            "api_key" to "abc123",
            "timeout" to "30"
        )
    }
}

// Usage
val config = Configuration("app.conf")
println("Database URL: ${config.get("database_url")}")
```

## ⚠️ Important Considerations

### **1. Init Block Execution Order**
```kotlin
class Example {
    init {
        println("Init block 1")
    }
    
    val property1 = "Property 1".also { println("Property 1 initialized") }
    
    init {
        println("Init block 2")
    }
    
    val property2 = "Property 2".also { println("Property 2 initialized") }
    
    init {
        println("Init block 3")
    }
}

// Execution order:
// Init block 1
// Property 1 initialized
// Init block 2
// Property 2 initialized
// Init block 3
```

### **2. Access to Constructor Parameters**
```kotlin
class Person(val name: String, val age: Int) {
    init {
        // ✅ Can access constructor parameters
        println("Name: $name, Age: $age")
        
        // ✅ Can perform validation
        require(age >= 0) { "Age cannot be negative" }
        
        // ✅ Can initialize derived properties
        val isAdult = age >= 18
        println("Is adult: $isAdult")
    }
}
```

### **3. Multiple Init Blocks**
```kotlin
class ComplexClass(val param: String) {
    init {
        println("First init: $param")
    }
    
    val property1 = "Property 1"
    
    init {
        println("Second init: $param, $property1")
    }
    
    val property2 = "Property 2"
    
    init {
        println("Third init: $param, $property1, $property2")
    }
}
```

## 🎯 Best Practices

### **1. Use for Validation**
```kotlin
// ✅ Good - validation in init block
class User(val email: String, val age: Int) {
    init {
        require(email.contains("@")) { "Invalid email format" }
        require(age >= 13) { "User must be at least 13 years old" }
    }
}

// ❌ Avoid - validation in separate method
class User(val email: String, val age: Int) {
    fun validate() {
        require(email.contains("@")) { "Invalid email format" }
        require(age >= 13) { "User must be at least 13 years old" }
    }
}
```

### **2. Keep Init Blocks Focused**
```kotlin
// ✅ Good - focused initialization
class Product(val name: String, val price: Double) {
    init {
        require(name.isNotBlank()) { "Product name cannot be empty" }
        require(price >= 0) { "Price cannot be negative" }
    }
    
    val formattedPrice = "$${String.format("%.2f", price)}"
}

// ❌ Avoid - complex logic in init
class Product(val name: String, val price: Double) {
    init {
        // Complex business logic...
        val marketAnalysis = analyzeMarket()
        val competitorPricing = getCompetitorPrices()
        val optimalPrice = calculateOptimalPrice(marketAnalysis, competitorPricing)
        // ... more complex logic
    }
}
```

### **3. Document Complex Initialization**
```kotlin
/**
 * Represents a network connection with validation and setup
 * @param host The server hostname
 * @param port The server port number
 * @param timeout Connection timeout in milliseconds
 */
class NetworkConnection(val host: String, val port: Int, val timeout: Long) {
    init {
        // Validate network parameters
        require(host.isNotBlank()) { "Host cannot be empty" }
        require(port in 1..65535) { "Port must be between 1 and 65535" }
        require(timeout > 0) { "Timeout must be positive" }
        
        // Log connection setup
        println("Setting up connection to $host:$port with ${timeout}ms timeout")
    }
}
```

## 🔧 Practical Applications

### **1. Configuration Classes**
```kotlin
class AppConfig(val configPath: String) {
    private val properties: Properties
    
    init {
        properties = Properties()
        try {
            FileInputStream(configPath).use { properties.load(it) }
        } catch (e: Exception) {
            println("Using default configuration: ${e.message}")
            loadDefaultConfig()
        }
    }
    
    private fun loadDefaultConfig() {
        properties.setProperty("database.url", "jdbc:default")
        properties.setProperty("database.user", "default")
        properties.setProperty("database.password", "default")
    }
    
    fun getProperty(key: String): String? = properties.getProperty(key)
}
```

### **2. Data Validation Classes**
```kotlin
class EmailValidator(val email: String) {
    private val isValid: Boolean
    
    init {
        val emailRegex = Regex("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}\$")
        isValid = emailRegex.matches(email)
        
        if (!isValid) {
            println("Warning: Invalid email format: $email")
        }
    }
    
    fun isValidEmail(): Boolean = isValid
}
```

### **3. Resource Management**
```kotlin
class FileProcessor(val filePath: String) {
    private val file: File
    
    init {
        file = File(filePath)
        require(file.exists()) { "File does not exist: $filePath" }
        require(file.canRead()) { "File is not readable: $filePath" }
        require(file.length() > 0) { "File is empty: $filePath" }
        
        println("Processing file: ${file.name} (${file.length()} bytes)")
    }
    
    fun process(): String {
        return file.readText()
    }
}
```

## 📚 Summary

**Init blocks** in Kotlin provide:
- **Automatic execution** during object creation
- **Parameter validation** at construction time
- **Initialization logic** in a clean, organized way
- **Execution order control** for complex initialization

## 🎯 Key Takeaways

1. **Use `init { }` blocks** for initialization logic
2. **Execute in declaration order** - multiple init blocks run sequentially
3. **Access constructor parameters** directly in init blocks
4. **Use for validation** and setup logic
5. **Keep focused** - avoid complex business logic in init blocks

## 🚀 Next Steps

- Practice creating classes with init blocks
- Learn about secondary constructors
- Explore property initialization
- Understand object creation lifecycle

---

**📁 Source Code:** [26_class_and_constructor.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/26_class_and_constructor.kt)

**🔗 Related Topics:**
- [Classes and Constructors](../oop/01-classes-constructors.md)
- [Inheritance](../oop/02-inheritance.md)
- [Properties](../oop/06-properties.md)
