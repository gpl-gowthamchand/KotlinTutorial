# 🎭 Companion Object in Kotlin

Companion objects in Kotlin are a way to define static members that belong to a class rather than to instances of the class. They provide a way to organize class-level functionality and constants, similar to static members in Java.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what companion objects are in Kotlin
- ✅ Create and use companion objects effectively
- ✅ Know when to use companion objects vs object declarations
- ✅ Use companion object properties and methods
- ✅ Apply companion objects in real-world scenarios

## 🔍 What You'll Learn

- **Companion object syntax** - How to declare and use companion objects
- **Static-like behavior** - Understanding class-level members
- **Factory methods** - Creating objects through companion objects
- **Constants and utilities** - Organizing class-level data
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of object declarations
- ✅ Familiarity with Kotlin syntax
- ✅ Understanding of object-oriented programming

## 💻 The Code

Let's examine the companion object examples:

**📁 File:** [34_companion_object.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/34_companion_object.kt)

## 🔍 Code Breakdown

### **Basic Companion Object Declaration**
```kotlin
class MyClass {
    companion object {
        const val CONSTANT = "value"
        fun create(): MyClass = MyClass()
    }
}
```

**Key Components:**
- `class MyClass` - Class declaration
- `companion object` - Companion object declaration
- `const val CONSTANT` - Constant property
- `fun create()` - Factory method

### **Companion Object Usage**
```kotlin
// Usage
val constant = MyClass.CONSTANT
val instance = MyClass.create()
```

## 🎯 Key Concepts Explained

### **1. What are Companion Objects?**

Companion objects in Kotlin:
- **Belong to a class** - not to instances
- **Provide static-like behavior** - accessible without instantiation
- **Can have names** - or be anonymous
- **Support inheritance** - can implement interfaces
- **Organize class-level functionality** - constants, factory methods, utilities

### **2. Companion Object vs Object Declaration**

| Feature | Companion Object | Object Declaration |
|---------|------------------|-------------------|
| **Scope** | Belongs to class | Global singleton |
| **Access** | ClassName.member | ObjectName.member |
| **Inheritance** | Can implement interfaces | Can inherit from classes |
| **Usage** | Class-level members | Global utilities |
| **Naming** | Can be named or anonymous | Must have name |

### **3. Companion Object vs Static Members**

```kotlin
// Kotlin - Companion Object
class MyClass {
    companion object {
        const val CONSTANT = "value"
        fun utility() = "utility"
    }
}

// Java equivalent
class MyClass {
    public static final String CONSTANT = "value";
    public static String utility() { return "utility"; }
}
```

## 🧪 Examples and Exercises

### **Example 1: Basic Companion Object**
```kotlin
class User private constructor(
    val id: String,
    val name: String,
    val email: String
) {
    companion object {
        const val DEFAULT_ROLE = "user"
        const val MAX_NAME_LENGTH = 50
        
        fun create(id: String, name: String, email: String): User {
            require(name.length <= MAX_NAME_LENGTH) { "Name too long" }
            require(email.contains("@")) { "Invalid email" }
            return User(id, name, email)
        }
        
        fun createGuest(): User {
            return User("guest_${System.currentTimeMillis()}", "Guest User", "guest@example.com")
        }
        
        fun validateEmail(email: String): Boolean {
            return email.contains("@") && email.contains(".")
        }
    }
    
    override fun toString(): String = "User(id=$id, name=$name, email=$email)"
}

// Usage
fun demonstrateBasicCompanion() {
    val user = User.create("U001", "John Doe", "john@example.com")
    val guest = User.createGuest()
    
    println("Regular user: $user")
    println("Guest user: $guest")
    println("Default role: ${User.DEFAULT_ROLE}")
    println("Max name length: ${User.MAX_NAME_LENGTH}")
    println("Valid email: ${User.validateEmail("test@example.com")}")
}
```

### **Example 2: Named Companion Object**
```kotlin
class DatabaseConnection private constructor(
    val host: String,
    val port: Int,
    val database: String
) {
    companion object Factory {
        const val DEFAULT_PORT = 5432
        const val DEFAULT_HOST = "localhost"
        
        fun create(host: String = DEFAULT_HOST, port: Int = DEFAULT_PORT, database: String): DatabaseConnection {
            require(port in 1..65535) { "Invalid port number" }
            require(database.isNotBlank()) { "Database name cannot be empty" }
            return DatabaseConnection(host, port, database)
        }
        
        fun createLocal(database: String): DatabaseConnection {
            return create(database = database)
        }
        
        fun createRemote(host: String, database: String): DatabaseConnection {
            return create(host = host, database = database)
        }
    }
    
    fun getConnectionString(): String = "jdbc:postgresql://$host:$port/$database"
}

// Usage
fun demonstrateNamedCompanion() {
    val localDb = DatabaseConnection.Factory.createLocal("mydb")
    val remoteDb = DatabaseConnection.Factory.createRemote("192.168.1.100", "production")
    val customDb = DatabaseConnection.Factory.create("custom.host", 5433, "customdb")
    
    println("Local: ${localDb.getConnectionString()}")
    println("Remote: ${remoteDb.getConnectionString()}")
    println("Custom: ${customDb.getConnectionString()}")
    println("Default port: ${DatabaseConnection.Factory.DEFAULT_PORT}")
}
```

### **Example 3: Companion Object with Interface**
```kotlin
interface Factory<T> {
    fun create(): T
    fun createWithParams(vararg params: Any): T
}

class Product private constructor(
    val id: String,
    val name: String,
    val price: Double
) {
    companion object : Factory<Product> {
        const val MIN_PRICE = 0.0
        const val MAX_NAME_LENGTH = 100
        
        override fun create(): Product {
            return Product("P${System.currentTimeMillis()}", "Default Product", 0.0)
        }
        
        override fun createWithParams(vararg params: Any): Product {
            require(params.size >= 3) { "Need id, name, and price" }
            val id = params[0] as String
            val name = params[1] as String
            val price = params[2] as Double
            
            require(price >= MIN_PRICE) { "Price cannot be negative" }
            require(name.length <= MAX_NAME_LENGTH) { "Name too long" }
            
            return Product(id, name, price)
        }
        
        fun createFromMap(data: Map<String, Any>): Product {
            return createWithParams(
                data["id"] ?: "P${System.currentTimeMillis()}",
                data["name"] ?: "Unknown Product",
                data["price"] ?: 0.0
            )
        }
    }
    
    override fun toString(): String = "Product(id=$id, name=$name, price=$$price)"
}

// Usage
fun demonstrateCompanionWithInterface() {
    val defaultProduct = Product.create()
    val customProduct = Product.createWithParams("P001", "Laptop", 999.99)
    val mapProduct = Product.createFromMap(mapOf(
        "id" to "P002",
        "name" to "Mouse",
        "price" to 29.99
    ))
    
    println("Default: $defaultProduct")
    println("Custom: $customProduct")
    println("From Map: $mapProduct")
    println("Min price: ${Product.MIN_PRICE}")
}
```

### **Example 4: Utility Companion Object**
```kotlin
class StringProcessor {
    companion object Utils {
        const val DEFAULT_SEPARATOR = ", "
        const val MAX_LENGTH = 1000
        
        fun reverse(text: String): String = text.reversed()
        
        fun capitalize(text: String): String = text.replaceFirstChar { it.uppercase() }
        
        fun truncate(text: String, maxLength: Int = MAX_LENGTH): String {
            return if (text.length <= maxLength) text else text.take(maxLength) + "..."
        }
        
        fun join(items: List<String>, separator: String = DEFAULT_SEPARATOR): String {
            return items.joinToString(separator)
        }
        
        fun split(text: String, separator: String = DEFAULT_SEPARATOR): List<String> {
            return text.split(separator)
        }
        
        fun countWords(text: String): Int {
            return text.split("\\s+".toRegex()).size
        }
        
        fun isPalindrome(text: String): Boolean {
            val cleanText = text.lowercase().replace(Regex("[^a-z0-9]"), "")
            return cleanText == cleanText.reversed()
        }
    }
}

// Usage
fun demonstrateUtilityCompanion() {
    val text = "Hello World from Kotlin Programming Language"
    
    println("Original: $text")
    println("Reversed: ${StringProcessor.Utils.reverse(text)}")
    println("Capitalized: ${StringProcessor.Utils.capitalize(text)}")
    println("Truncated: ${StringProcessor.Utils.truncate(text, 20)}")
    println("Word count: ${StringProcessor.Utils.countWords(text)}")
    println("Is palindrome: ${StringProcessor.Utils.isPalindrome("racecar")}")
    
    val items = listOf("apple", "banana", "cherry")
    val joined = StringProcessor.Utils.join(items)
    val split = StringProcessor.Utils.split(joined)
    
    println("Joined: $joined")
    println("Split: $split")
}
```

## ⚠️ Important Considerations

### **1. Companion Object Access**
```kotlin
class MyClass {
    companion object {
        const val CONSTANT = "value"
        fun method() = "method"
    }
}

// ✅ Access through class name
val constant = MyClass.CONSTANT
val result = MyClass.method()

// ✅ Access through companion object reference
val companion = MyClass.Companion
val constant2 = companion.CONSTANT
val result2 = companion.method()

// ❌ Won't work - cannot access through instance
val instance = MyClass()
// val constant3 = instance.CONSTANT  // Error
```

### **2. Companion Object Inheritance**
```kotlin
interface Factory<T> {
    fun create(): T
}

class MyClass {
    companion object : Factory<MyClass> {
        override fun create(): MyClass = MyClass()
    }
}

// Usage
val instance = MyClass.create()  // Through interface
val instance2 = MyClass.Companion.create()  // Direct access
```

### **3. Companion Object vs Object Declaration**
```kotlin
// Companion Object - belongs to class
class MyClass {
    companion object {
        fun create(): MyClass = MyClass()
    }
}

// Object Declaration - global singleton
object MyObject {
    fun create(): MyClass = MyClass()
}

// Usage differences
val obj1 = MyClass.create()  // Through companion object
val obj2 = MyObject.create()  // Through object declaration
```

## 🎯 Best Practices

### **1. Use for Factory Methods**
```kotlin
// ✅ Good - factory methods in companion object
class User private constructor(val name: String) {
    companion object {
        fun create(name: String): User {
            require(name.isNotBlank()) { "Name cannot be empty" }
            return User(name)
        }
    }
}

// ❌ Avoid - factory methods in object declaration
object UserFactory {
    fun create(name: String): User {
        require(name.isNotBlank()) { "Name cannot be empty" }
        return User(name)
    }
}
```

### **2. Use for Constants**
```kotlin
// ✅ Good - constants in companion object
class Configuration {
    companion object {
        const val MAX_CONNECTIONS = 100
        const val TIMEOUT = 5000
        const val DEFAULT_HOST = "localhost"
    }
}

// ❌ Avoid - constants in object declaration
object Constants {
    const val MAX_CONNECTIONS = 100
    const val TIMEOUT = 5000
    const val DEFAULT_HOST = "localhost"
}
```

### **3. Use for Class-Level Utilities**
```kotlin
// ✅ Good - class-specific utilities
class StringUtils {
    companion object {
        fun reverse(text: String): String = text.reversed()
        fun capitalize(text: String): String = text.replaceFirstChar { it.uppercase() }
    }
}

// ❌ Avoid - global utilities in companion object
class SomeClass {
    companion object {
        fun globalUtility() = "This doesn't belong here"
    }
}
```

## 🔧 Practical Applications

### **1. Builder Pattern**
```kotlin
class DatabaseConfig private constructor(
    val host: String,
    val port: Int,
    val database: String,
    val username: String,
    val password: String
) {
    companion object Builder {
        fun build(block: DatabaseConfigBuilder.() -> Unit): DatabaseConfig {
            val builder = DatabaseConfigBuilder()
            builder.block()
            return builder.build()
        }
    }
    
    class DatabaseConfigBuilder {
        var host: String = "localhost"
        var port: Int = 5432
        var database: String = "mydb"
        var username: String = "admin"
        var password: String = ""
        
        fun build(): DatabaseConfig = DatabaseConfig(host, port, database, username, password)
    }
}

// Usage
val config = DatabaseConfig.Builder.build {
    host = "192.168.1.100"
    port = 5433
    database = "production"
    username = "prod_user"
    password = "secret123"
}
```

### **2. Serialization/Deserialization**
```kotlin
class User private constructor(
    val id: String,
    val name: String,
    val email: String
) {
    companion object Serializer {
        fun fromJson(json: String): User {
            // JSON parsing logic
            val data = json.trim('{', '}').split(",")
            val id = data[0].split(":")[1].trim('"')
            val name = data[1].split(":")[1].trim('"')
            val email = data[2].split(":")[1].trim('"')
            return User(id, name, email)
        }
        
        fun toJson(user: User): String {
            return """{"id":"${user.id}","name":"${user.name}","email":"${user.email}"}"""
        }
    }
}

// Usage
val user = User.Serializer.fromJson("""{"id":"U001","name":"John Doe","email":"john@example.com"}""")
val json = User.Serializer.toJson(user)
```

### **3. Validation and Creation**
```kotlin
class Email private constructor(val value: String) {
    companion object Validator {
        private val EMAIL_REGEX = Regex("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}\$")
        
        fun create(email: String): Email {
            require(email.isNotBlank()) { "Email cannot be empty" }
            require(EMAIL_REGEX.matches(email)) { "Invalid email format" }
            return Email(email)
        }
        
        fun isValid(email: String): Boolean {
            return EMAIL_REGEX.matches(email)
        }
        
        fun getDomain(email: String): String? {
            return if (isValid(email)) email.substringAfter("@") else null
        }
    }
    
    override fun toString(): String = value
}

// Usage
val email = Email.Validator.create("user@example.com")
val isValid = Email.Validator.isValid("invalid-email")
val domain = Email.Validator.getDomain("admin@company.com")
```

## 📚 Summary

**Companion objects** in Kotlin provide:
- **Class-level functionality** similar to static members
- **Factory methods** for object creation
- **Constants and utilities** organized within classes
- **Interface implementation** capabilities
- **Clean organization** of class-related functionality

## 🎯 Key Takeaways

1. **Use `companion object`** for class-level members
2. **Access through class name** (ClassName.member)
3. **Support factory methods** and constants
4. **Can implement interfaces** and inherit
5. **Organize class-related functionality** cleanly

## 🚀 Next Steps

- Practice creating companion objects for different scenarios
- Learn about object expressions
- Explore companion object inheritance
- Understand when to use companion objects vs object declarations

---

**📁 Source Code:** [34_companion_object.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/34_companion_object.kt)

**🔗 Related Topics:**
- [Object Declaration](../oop/11-object-declaration.md)
- [Classes and Constructors](../oop/01-classes-constructors.md)
- [Data Class](../oop/10-data-class.md)
