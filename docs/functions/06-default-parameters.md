# 🎯 Default Parameters in Kotlin

Default parameters in Kotlin allow you to specify default values for function parameters, making your functions more flexible and reducing the need for multiple overloaded versions.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand how default parameters work
- ✅ Create functions with default parameters
- ✅ Use default parameters effectively
- ✅ Know when and how to use them
- ✅ Apply default parameters in real-world scenarios

## 🔍 What You'll Learn

- **Default parameter syntax** - How to declare parameters with default values
- **Function overloading** - How default parameters reduce the need for multiple functions
- **Parameter order** - Understanding the importance of parameter positioning
- **Use cases** - When and where to use default parameters
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of functions in Kotlin
- ✅ Knowledge of function parameters and return types
- ✅ Familiarity with Kotlin syntax

## 💻 The Code

Let's examine the default parameters examples:

**📁 File:** [10_default_functions.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/10_default_functions.kt)

## 🔍 Code Breakdown

### **Basic Default Parameter Declaration**
```kotlin
fun greet(name: String, greeting: String = "Hello") {
    println("$greeting, $name!")
}
```

**Key Components:**
- `fun greet` - Function declaration
- `name: String` - Required parameter (no default)
- `greeting: String = "Hello"` - Parameter with default value
- `"Hello"` - Default value for the greeting parameter

### **Function Calls with Default Parameters**
```kotlin
// Using default parameter
greet("John")  // Prints: Hello, John!

// Overriding default parameter
greet("John", "Good morning")  // Prints: Good morning, John!
```

## 🎯 Key Concepts Explained

### **1. How Default Parameters Work**

Default parameters allow you to:
- **Skip parameters** when calling functions
- **Reduce function overloads** - one function instead of many
- **Provide sensible defaults** for common use cases
- **Maintain backward compatibility** when adding new parameters

### **2. Parameter Order and Defaults**

```kotlin
fun createUser(
    name: String,
    email: String = "",
    age: Int = 18,
    isActive: Boolean = true
) {
    // Function implementation
}

// Valid calls
createUser("John")  // Uses all defaults
createUser("John", "john@email.com")  // Overrides email, uses defaults for age and isActive
createUser("John", "john@email.com", 25)  // Overrides email and age, uses default for isActive
createUser("John", "john@email.com", 25, false)  // Overrides all parameters
```

### **3. Named Parameters with Defaults**

```kotlin
fun createUser(
    name: String,
    email: String = "",
    age: Int = 18,
    isActive: Boolean = true
) {
    // Function implementation
}

// Using named parameters to skip some defaults
createUser(
    name = "John",
    age = 25,
    isActive = false
    // email will use default value ""
)
```

## 🧪 Examples and Exercises

### **Example 1: String Formatting Function**
```kotlin
fun formatText(
    text: String,
    prefix: String = "",
    suffix: String = "",
    maxLength: Int = 100
): String {
    val formatted = "$prefix$text$suffix"
    return if (formatted.length <= maxLength) formatted else formatted.take(maxLength) + "..."
}

// Usage
val result1 = formatText("Hello World")  // Uses all defaults
val result2 = formatText("Hello World", ">>> ", " <<<")  // Overrides prefix and suffix
val result3 = formatText("Very long text that exceeds the maximum length", maxLength = 20)  // Named parameter
```

### **Example 2: Configuration Function**
```kotlin
fun configureDatabase(
    host: String = "localhost",
    port: Int = 5432,
    username: String = "admin",
    password: String = "",
    database: String = "mydb"
) {
    println("Connecting to $host:$port/$database as $username")
}

// Usage
configureDatabase()  // Uses all defaults
configureDatabase(host = "192.168.1.100", password = "secret123")  // Named parameters
```

### **Example 3: Collection Processing**
```kotlin
fun processList(
    items: List<String>,
    separator: String = ", ",
    prefix: String = "[",
    suffix: String = "]",
    maxItems: Int = 10
): String {
    val limitedItems = items.take(maxItems)
    return "$prefix${limitedItems.joinToString(separator)}$suffix"
}

// Usage
val list = listOf("apple", "banana", "cherry", "date", "elderberry")
val result1 = processList(list)  // [apple, banana, cherry, date, elderberry]
val result2 = processList(list, separator = " | ", maxItems = 3)  // [apple | banana | cherry]
```

## ⚠️ Important Considerations

### **1. Parameter Order Matters**
```kotlin
// ❌ Won't work - can't skip required parameters
fun greet(greeting: String = "Hello", name: String) {
    println("$greeting, $name!")
}

// ❌ This call will fail
greet("John")  // Error: missing required parameter 'name'

// ✅ Correct order - required parameters first
fun greet(name: String, greeting: String = "Hello") {
    println("$greeting, $name!")
}

// ✅ This call works
greet("John")  // Prints: Hello, John!
```

### **2. Default Values Are Evaluated Once**
```kotlin
fun createId(prefix: String = "ID_", timestamp: Long = System.currentTimeMillis()): String {
    return "$prefix$timestamp"
}

// Both calls will have different timestamps
val id1 = createId()  // ID_1234567890
val id2 = createId()  // ID_1234567891
```

### **3. Mutable Default Parameters**
```kotlin
// ⚠️ Be careful with mutable default parameters
fun addToList(item: String, list: MutableList<String> = mutableListOf()): MutableList<String> {
    list.add(item)
    return list
}

// This can lead to unexpected behavior
val list1 = addToList("first")
val list2 = addToList("second")
// list1 and list2 might reference the same list!
```

## 🎯 Best Practices

### **1. Put Required Parameters First**
```kotlin
// ✅ Good - required parameters first
fun sendEmail(to: String, subject: String, body: String = "", cc: List<String> = emptyList())

// ❌ Avoid - required parameters after defaults
fun sendEmail(subject: String = "", body: String = "", to: String, cc: List<String> = emptyList())
```

### **2. Use Sensible Defaults**
```kotlin
// ✅ Good - sensible defaults
fun createFile(name: String, extension: String = "txt", overwrite: Boolean = false)

// ❌ Avoid - confusing defaults
fun createFile(name: String, extension: String = "xyz", overwrite: Boolean = true)
```

### **3. Document Complex Defaults**
```kotlin
/**
 * Creates a user with default values
 * @param name User's full name (required)
 * @param email User's email address (defaults to empty string)
 * @param age User's age (defaults to 18)
 * @param isActive Whether the user account is active (defaults to true)
 */
fun createUser(
    name: String,
    email: String = "",
    age: Int = 18,
    isActive: Boolean = true
) {
    // Implementation
}
```

## 🔧 Practical Applications

### **1. Builder Pattern Alternative**
```kotlin
// Instead of builder pattern
fun createPerson(
    name: String,
    age: Int = 0,
    city: String = "",
    occupation: String = "",
    hobbies: List<String> = emptyList()
) = Person(name, age, city, occupation, hobbies)

// Usage
val person = createPerson(
    name = "John Doe",
    age = 30,
    city = "New York"
    // occupation and hobbies use defaults
)
```

### **2. Configuration Functions**
```kotlin
fun configureLogger(
    level: String = "INFO",
    format: String = "JSON",
    output: String = "console",
    maxSize: Int = 100
) {
    // Logger configuration logic
}
```

### **3. Utility Functions**
```kotlin
fun formatCurrency(
    amount: Double,
    currency: String = "USD",
    locale: String = "en_US",
    decimalPlaces: Int = 2
): String {
    // Currency formatting logic
}
```

## 📚 Summary

**Default parameters** in Kotlin provide:
- **Flexibility** in function calls
- **Reduced code duplication** through fewer overloaded functions
- **Better readability** with sensible defaults
- **Maintainability** when adding new parameters

## 🎯 Key Takeaways

1. **Use `parameter = value`** syntax for default parameters
2. **Required parameters first** - put parameters with defaults after required ones
3. **Named parameters** help when skipping some defaults
4. **Sensible defaults** make functions easier to use
5. **Document complex defaults** for better understanding

## 🚀 Next Steps

- Practice creating functions with default parameters
- Learn about function overloading
- Explore named parameters in detail
- Understand parameter order and its importance

---

**📁 Source Code:** [10_default_functions.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/10_default_functions.kt)

**🔗 Related Topics:**
- [Functions Basics](../functions/01-functions-basics.md)
- [Named Parameters](../functions/03-named-parameters.md)
- [Function Expressions](../functions/02-functions-as-expressions.md)
