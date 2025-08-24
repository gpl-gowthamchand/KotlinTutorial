# 🏷️ Named Parameters in Kotlin

Welcome to the world of named parameters! Named parameters make your function calls more readable and self-documenting. They allow you to specify which parameter each argument corresponds to, eliminating confusion about parameter order and making your code more maintainable.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Use named parameters in function calls
- ✅ Understand the benefits of named parameters
- ✅ Combine named and positional parameters
- ✅ Use default values with named parameters
- ✅ Write more readable and maintainable code

## 🔍 What You'll Learn

- **Named parameter syntax** - How to specify parameter names
- **Parameter order flexibility** - Freedom from strict ordering
- **Default values** - Combining with named parameters
- **Best practices** - When and how to use named parameters
- **Real-world applications** - Practical use cases

## 📝 Prerequisites

- Basic understanding of functions
- Completed [Functions as Expressions](02-functions-as-expressions.md) lesson
- Knowledge of function parameters and default values

## 💻 The Code

Let's examine the named parameters example:

```kotlin
fun findTheVolume(length: Int, breadth: Int, height: Int = 10): Int {
    return length * breadth * height
}

fun main(args: Array<String>) {
    var result = findTheVolume(breadth = 2, length = 3)
    print(result)
}
```

**📁 File:** [21_named_parameters.kt](src/21_named_parameters.kt)

## 🔍 Code Breakdown

### **Function Definition**

```kotlin
fun findTheVolume(length: Int, breadth: Int, height: Int = 10): Int {
    return length * breadth * height
}
```

- **`length: Int`**: First parameter for length
- **`breadth: Int`**: Second parameter for breadth  
- **`height: Int = 10`**: Third parameter with default value 10
- **Return type**: `Int` (volume calculation)

### **Function Call with Named Parameters**

```kotlin
var result = findTheVolume(breadth = 2, length = 3)
```

- **`breadth = 2`**: Explicitly assigns 2 to breadth parameter
- **`length = 3`**: Explicitly assigns 3 to length parameter
- **`height`**: Not specified, uses default value 10
- **Result**: 3 × 2 × 10 = 60

## 🎯 Key Concepts Explained

### **1. Named Parameter Syntax**

#### **Basic Named Parameter Usage**

```kotlin
fun greet(firstName: String, lastName: String, title: String = "Mr.") {
    println("Hello, $title $firstName $lastName!")
}

// Using named parameters
greet(firstName = "John", lastName = "Doe")
greet(lastName = "Smith", firstName = "Jane", title = "Dr.")
```

**Benefits:**
- **Clear intent**: Each argument's purpose is obvious
- **Order flexibility**: Parameters can be in any order
- **Self-documenting**: Code reads like natural language

#### **Positional vs Named Parameters**

```kotlin
// Positional parameters (traditional)
greet("John", "Doe", "Mr.")

// Named parameters
greet(firstName = "John", lastName = "Doe", title = "Mr.")

// Mixed approach
greet("John", lastName = "Doe", title = "Dr.")
```

### **2. Default Values with Named Parameters**

#### **Function with Default Values**

```kotlin
fun createUser(
    username: String,
    email: String,
    age: Int = 18,
    isActive: Boolean = true,
    role: String = "user"
) {
    println("User: $username, Email: $email, Age: $age, Active: $isActive, Role: $role")
}
```

#### **Calling with Named Parameters**

```kotlin
// Specify only required parameters
createUser(username = "john_doe", email = "john@example.com")

// Override some defaults
createUser(
    username = "admin",
    email = "admin@example.com",
    role = "administrator"
)

// Override all defaults
createUser(
    username = "moderator",
    email = "mod@example.com",
    age = 25,
    isActive = false,
    role = "moderator"
)
```

### **3. Parameter Order Flexibility**

#### **Traditional Positional Call**

```kotlin
fun calculateDistance(x1: Double, y1: Double, x2: Double, y2: Double): Double {
    return Math.sqrt((x2 - x1).pow(2) + (y2 - y1).pow(2))
}

// Must remember exact order
val distance = calculateDistance(0.0, 0.0, 3.0, 4.0)
```

#### **Named Parameter Call**

```kotlin
// Clear and readable
val distance = calculateDistance(
    x1 = 0.0,
    y1 = 0.0,
    x2 = 3.0,
    y2 = 4.0
)

// Order doesn't matter
val distance2 = calculateDistance(
    y2 = 4.0,
    x1 = 0.0,
    y1 = 0.0,
    x2 = 3.0
)
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Named Parameters**
Create a function that builds a URL with named parameters:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a buildUrl function and call it with named parameters
    // Parameters: protocol, host, port, path, query
    // Default values: protocol="https", port=443, path="/", query=""
}
```

**Solution:**
```kotlin
fun buildUrl(
    protocol: String = "https",
    host: String,
    port: Int = 443,
    path: String = "/",
    query: String = ""
): String {
    val url = "$protocol://$host"
    val portPart = if (port != 443) ":$port" else ""
    val queryPart = if (query.isNotEmpty()) "?$query" else ""
    return "$url$portPart$path$queryPart"
}

fun main(args: Array<String>) {
    // Using named parameters
    val url1 = buildUrl(
        host = "example.com",
        path = "/api/users"
    )
    
    val url2 = buildUrl(
        protocol = "http",
        host = "localhost",
        port = 8080,
        path = "/admin",
        query = "debug=true"
    )
    
    println("URL 1: $url1")
    println("URL 2: $url2")
}
```

### **Exercise 2: Configuration Object Builder**
Create a function that builds a configuration object:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a buildConfig function with named parameters
    // Parameters: database, cache, logging, timeout
    // Use sensible defaults
}
```

**Solution:**
```kotlin
fun buildConfig(
    database: String = "localhost:5432",
    cache: Boolean = true,
    logging: String = "INFO",
    timeout: Int = 30
): String {
    return """
        Configuration:
        - Database: $database
        - Cache: $cache
        - Logging: $logging
        - Timeout: ${timeout}s
    """.trimIndent()
}

fun main(args: Array<String>) {
    // Minimal configuration
    val config1 = buildConfig(database = "prod-db:5432")
    
    // Custom configuration
    val config2 = buildConfig(
        database = "test-db:5432",
        cache = false,
        logging = "DEBUG",
        timeout = 60
    )
    
    println("Config 1:\n$config1")
    println("\nConfig 2:\n$config2")
}
```

### **Exercise 3: Mixed Parameter Styles**
Create a function that demonstrates mixing named and positional parameters:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a formatMessage function that can be called in different ways
    // First parameter should be positional, others can be named
}
```

**Solution:**
```kotlin
fun formatMessage(
    message: String,
    prefix: String = "",
    suffix: String = "",
    uppercase: Boolean = false,
    repeat: Int = 1
): String {
    var result = prefix + message + suffix
    if (uppercase) result = result.uppercase()
    return result.repeat(repeat)
}

fun main(args: Array<String>) {
    // Positional first parameter, named others
    val msg1 = formatMessage(
        "Hello World",
        prefix = ">>> ",
        suffix = " <<<"
    )
    
    // All named parameters
    val msg2 = formatMessage(
        message = "Goodbye",
        uppercase = true,
        repeat = 3
    )
    
    // Mixed style
    val msg3 = formatMessage(
        "Test",
        suffix = "!",
        repeat = 2
    )
    
    println(msg1)
    println(msg2)
    println(msg3)
}
```

### **Exercise 4: Complex Named Parameters**
Create a function for building a complex data structure:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a buildPerson function with many optional parameters
    // Use named parameters to make it readable
}
```

**Solution:**
```kotlin
fun buildPerson(
    firstName: String,
    lastName: String,
    age: Int = 0,
    email: String = "",
    phone: String = "",
    address: String = "",
    occupation: String = "",
    hobbies: List<String> = emptyList(),
    isActive: Boolean = true
): String {
    return """
        Person Details:
        Name: $firstName $lastName
        Age: ${if (age > 0) age else "Not specified"}
        Email: ${if (email.isNotEmpty()) email else "Not specified"}
        Phone: ${if (phone.isNotEmpty()) phone else "Not specified"}
        Address: ${if (address.isNotEmpty()) address else "Not specified"}
        Occupation: ${if (occupation.isNotEmpty()) occupation else "Not specified"}
        Hobbies: ${if (hobbies.isNotEmpty()) hobbies.joinToString(", ") else "None"}
        Status: ${if (isActive) "Active" else "Inactive"}
    """.trimIndent()
}

fun main(args: Array<String>) {
    // Minimal person
    val person1 = buildPerson(
        firstName = "John",
        lastName = "Doe"
    )
    
    // Complete person
    val person2 = buildPerson(
        firstName = "Jane",
        lastName = "Smith",
        age = 30,
        email = "jane@example.com",
        phone = "+1-555-0123",
        address = "123 Main St, City",
        occupation = "Software Engineer",
        hobbies = listOf("Reading", "Hiking", "Cooking"),
        isActive = true
    )
    
    println("Person 1:\n$person1")
    println("\nPerson 2:\n$person2")
}
```

## 🔍 Advanced Named Parameter Patterns

### **1. Builder Pattern with Named Parameters**

```kotlin
class DatabaseConfig private constructor(
    val host: String,
    val port: Int,
    val username: String,
    val password: String,
    val database: String
) {
    companion object {
        fun build(
            host: String = "localhost",
            port: Int = 5432,
            username: String = "postgres",
            password: String = "",
            database: String = "mydb"
        ) = DatabaseConfig(host, port, username, password, database)
    }
}

// Usage
val config = DatabaseConfig.build(
    host = "prod-server.com",
    username = "admin",
    password = "secret123"
)
```

### **2. Function Overloading with Named Parameters**

```kotlin
fun createConnection(
    host: String,
    port: Int = 3306,
    database: String = "default"
) = "mysql://$host:$port/$database"

fun createConnection(
    host: String,
    database: String,
    ssl: Boolean = false
) = "postgresql://$host/$database${if (ssl) "?sslmode=require" else ""}"

// Usage
val mysqlConn = createConnection(host = "localhost", port = 3306)
val pgConn = createConnection(host = "localhost", database = "users", ssl = true)
```

### **3. DSL-like Function Calls**

```kotlin
fun html(
    head: String = "",
    body: String = "",
    title: String = "",
    charset: String = "UTF-8"
): String {
    return """
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="$charset">
            ${if (title.isNotEmpty()) "<title>$title</title>" else ""}
            $head
        </head>
        <body>
            $body
        </body>
        </html>
    """.trimIndent()
}

// Usage
val page = html(
    title = "My Page",
    head = "<link rel='stylesheet' href='style.css'>",
    body = "<h1>Hello World</h1>"
)
```

## 🔍 When to Use Named Parameters

### **✅ Use Named Parameters When:**

1. **Many parameters**:
   ```kotlin
   // ✅ Clear with named parameters
   createUser(
       username = "john",
       email = "john@example.com",
       firstName = "John",
       lastName = "Doe",
       age = 25,
       isActive = true
   )
   
   // ❌ Confusing with positional
   createUser("john", "john@example.com", "John", "Doe", 25, true)
   ```

2. **Boolean parameters**:
   ```kotlin
   // ✅ Clear meaning
   sendEmail(
       to = "user@example.com",
       subject = "Welcome",
       html = true,
       attachments = false
   )
   ```

3. **Default values**:
   ```kotlin
   // ✅ Only specify what you need
   connect(
       host = "localhost",
       database = "users"
       // port and timeout use defaults
   )
   ```

### **✅ Use Positional Parameters When:**

1. **Few parameters**:
   ```kotlin
   // ✅ Simple and clear
   add(5, 3)
   greet("John")
   ```

2. **Standard order**:
   ```kotlin
   // ✅ Conventional order
   substring(0, 5)
   sublist(1, 4)
   ```

## 🚨 Common Mistakes to Avoid

### **1. Mixing Named and Positional Incorrectly**

```kotlin
// ❌ Named parameters must come after positional
fun example(a: Int, b: Int, c: Int) { }

// ❌ Wrong order
example(a = 1, 2, c = 3)

// ✅ Correct order
example(1, b = 2, c = 3)
```

### **2. Forgetting Default Values**

```kotlin
// ❌ Function expects 3 parameters
fun process(name: String, age: Int, city: String) { }

// ❌ Missing required parameter
process(name = "John", city = "New York")

// ✅ Provide all required parameters
process(name = "John", age = 25, city = "New York")
```

### **3. Overusing Named Parameters**

```kotlin
// ❌ Overkill for simple calls
val result = add(a = 5, b = 3)

// ✅ Simple and clear
val result = add(5, 3)
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use named parameters for clarity**:
   ```kotlin
   // ✅ Clear intent
   createUser(
       username = "john_doe",
       email = "john@example.com",
       isActive = true
   )
   ```

2. **Group related parameters**:
   ```kotlin
   // ✅ Logical grouping
   sendEmail(
       to = "user@example.com",
       subject = "Welcome",
       body = "Welcome to our service!",
       // Email options
       html = true,
       attachments = false,
       priority = "high"
   )
   ```

3. **Use meaningful parameter names**:
   ```kotlin
   // ✅ Descriptive names
   fun calculateArea(
       rectangleWidth: Double,
       rectangleHeight: Double
   ): Double = rectangleWidth * rectangleHeight
   ```

### **❌ Don'ts**

1. **Don't use named parameters for simple calls**:
   ```kotlin
   // ❌ Unnecessary complexity
   val sum = add(a = 5, b = 3)
   
   // ✅ Simple and clear
   val sum = add(5, 3)
   ```

2. **Don't mix styles inconsistently**:
   ```kotlin
   // ❌ Inconsistent style
   fun example(a: Int, b: Int, c: Int) { }
   example(1, b = 2, 3)  // Mixed style
   
   // ✅ Consistent style
   example(1, 2, 3)  // All positional
   // OR
   example(a = 1, b = 2, c = 3)  // All named
   ```

## 🎯 What's Next?

Excellent! You've mastered named parameters in Kotlin. Now you're ready to:

1. **Explore extension functions** → [Extension Functions](04-extension-functions.md)
2. **Understand infix functions** → [Infix Functions](05-infix-functions.md)
3. **Master tailrec functions** → [Tailrec Functions](06-tailrec-functions.md)
4. **Learn about lambdas** → [Lambdas](../functional-programming/01-lambdas.md)

## 📚 Additional Resources

- [Kotlin Functions](https://kotlinlang.org/docs/functions.html)
- [Named Arguments](https://kotlinlang.org/docs/functions.html#named-arguments)
- [Default Arguments](https://kotlinlang.org/docs/functions.html#default-arguments)

## 🏆 Summary

- ✅ You can use named parameters in function calls
- ✅ You understand the benefits of named parameters
- ✅ You can combine named and positional parameters
- ✅ You can use default values with named parameters
- ✅ You can write more readable and maintainable code
- ✅ You're ready to create self-documenting function calls!

**Keep practicing and happy coding! 🎉**
