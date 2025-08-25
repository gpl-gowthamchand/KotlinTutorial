# 🏷️ Properties (Field Variables) in Kotlin

Properties in Kotlin are a powerful feature that combines fields, getters, and setters into a single declaration. They provide a clean, concise way to define class attributes with automatic backing fields and custom access logic.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what properties are in Kotlin
- ✅ Create different types of properties
- ✅ Use custom getters and setters
- ✅ Know when to use properties vs fields
- ✅ Apply properties in real-world scenarios

## 🔍 What You'll Learn

- **Property syntax** - How to declare and use properties
- **Backing fields** - Understanding automatic field generation
- **Custom accessors** - Creating custom getters and setters
- **Property types** - Val, var, and computed properties
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of constructors
- ✅ Familiarity with Kotlin syntax
- ✅ Understanding of object-oriented programming

## 💻 The Code

Let's examine the properties examples:

**📁 File:** [26_class_and_constructor.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/26_class_and_constructor.kt)

## 🔍 Code Breakdown

### **Basic Property Declaration**
```kotlin
class Person(val name: String, var age: Int) {
    var email: String = ""
    val isAdult: Boolean
        get() = age >= 18
}
```

**Key Components:**
- `val name: String` - Read-only property (immutable)
- `var age: Int` - Mutable property
- `var email: String = ""` - Property with default value
- `val isAdult: Boolean` - Computed property with custom getter

### **Property with Custom Getter**
```kotlin
class Rectangle(val width: Int, val height: Int) {
    val area: Int
        get() = width * height
    
    val perimeter: Int
        get() = 2 * (width + height)
}
```

## 🎯 Key Concepts Explained

### **1. What are Properties?**

Properties in Kotlin:
- **Combine fields and accessors** in a single declaration
- **Automatically generate backing fields** when needed
- **Provide clean syntax** for class attributes
- **Support custom logic** through getters and setters

### **2. Property Types**

| Type | Declaration | Mutability | Backing Field |
|------|-------------|------------|----------------|
| `val` | Read-only | Immutable | Generated automatically |
| `var` | Read-write | Mutable | Generated automatically |
| Custom | Custom logic | Depends on implementation | Optional |

### **3. Backing Fields**

```kotlin
class Example {
    var counter: Int = 0  // Backing field automatically generated
    
    var customCounter: Int = 0
        get() = field      // Access to backing field
        set(value) {
            field = value.coerceAtLeast(0)  // Modify backing field
        }
}
```

## 🧪 Examples and Exercises

### **Example 1: Basic Properties**
```kotlin
class Student(
    val studentId: String,
    var name: String,
    var grade: Double
) {
    var email: String = ""
    val isPassing: Boolean
        get() = grade >= 60.0
    
    val letterGrade: String
        get() = when {
            grade >= 90 -> "A"
            grade >= 80 -> "B"
            grade >= 70 -> "C"
            grade >= 60 -> "D"
            else -> "F"
        }
}

// Usage
val student = Student("S001", "John Doe", 85.5)
student.email = "john.doe@school.edu"
println("${student.name} has grade ${student.letterGrade}")  // John Doe has grade B
println("Is passing: ${student.isPassing}")  // Is passing: true
```

### **Example 2: Properties with Validation**
```kotlin
class BankAccount(
    val accountNumber: String,
    initialBalance: Double
) {
    var balance: Double = initialBalance
        private set  // Only class can modify balance
    
    var accountHolder: String = ""
        set(value) {
            require(value.isNotBlank()) { "Account holder name cannot be empty" }
            field = value.trim()
        }
    
    val isOverdrawn: Boolean
        get() = balance < 0
    
    val formattedBalance: String
        get() = "$${String.format("%.2f", balance)}"
    
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
val account = BankAccount("12345", 1000.0)
account.accountHolder = "  Jane Smith  "  // Trims whitespace
account.deposit(500.0)
println("${account.accountHolder}: ${account.formattedBalance}")  // Jane Smith: $1500.00
```

### **Example 3: Computed Properties**
```kotlin
class Circle(val radius: Double) {
    val diameter: Double
        get() = 2 * radius
    
    val circumference: Double
        get() = Math.PI * diameter
    
    val area: Double
        get() = Math.PI * radius * radius
    
    val isLarge: Boolean
        get() = radius > 10.0
}

class Rectangle(val width: Double, val height: Double) {
    val area: Double
        get() = width * height
    
    val perimeter: Double
        get() = 2 * (width + height)
    
    val isSquare: Boolean
        get() = width == height
    
    val diagonal: Double
        get() = Math.sqrt(width * width + height * height)
}

// Usage
val circle = Circle(5.0)
println("Circle area: ${circle.area}")  // Circle area: 78.54...
println("Is large: ${circle.isLarge}")  // Is large: false

val rect = Rectangle(4.0, 3.0)
println("Rectangle area: ${rect.area}")  // Rectangle area: 12.0
println("Is square: ${rect.isSquare}")  // Is square: false
```

### **Example 4: Lazy Properties**
```kotlin
class DataProcessor(val data: List<String>) {
    val processedData: List<String> by lazy {
        println("Processing data...")  // Only executed once
        data.map { it.trim().uppercase() }
    }
    
    val statistics: Map<String, Any> by lazy {
        println("Calculating statistics...")  // Only executed once
        mapOf(
            "count" to data.size,
            "totalLength" to data.sumOf { it.length },
            "averageLength" to data.map { it.length }.average(),
            "longest" to data.maxByOrNull { it.length } ?: "",
            "shortest" to data.minByOrNull { it.length } ?: ""
        )
    }
}

// Usage
val processor = DataProcessor(listOf("hello", "world", "kotlin"))
println("Data processor created")

// First access triggers computation
println("Processed data: ${processor.processedData}")
// Output: Processing data...
// Processed data: [HELLO, WORLD, KOTLIN]

// Second access uses cached result
println("Processed data again: ${processor.processedData}")
// Output: Processed data again: [HELLO, WORLD, KOTLIN]

// Statistics computed on first access
println("Statistics: ${processor.statistics}")
// Output: Calculating statistics...
// Statistics: {count=3, totalLength=16, averageLength=5.33..., longest=kotlin, shortest=hello}
```

## ⚠️ Important Considerations

### **1. Backing Field Access**
```kotlin
class Example {
    var counter: Int = 0
        get() = field      // Access backing field
        set(value) {
            field = value  // Modify backing field
        }
    
    // ❌ Won't work - infinite recursion
    var wrongCounter: Int = 0
        get() = wrongCounter  // Calls getter infinitely
        set(value) {
            wrongCounter = value  // Calls setter infinitely
        }
}
```

### **2. Property Initialization**
```kotlin
class Example {
    // ✅ Valid - property initialized
    var name: String = "Default"
    
    // ✅ Valid - property initialized in init block
    var description: String
    
    init {
        description = "Initial description"
    }
    
    // ❌ Invalid - property not initialized
    var status: String  // Error: Property must be initialized
}
```

### **3. Custom Setter Validation**
```kotlin
class User {
    var age: Int = 0
        set(value) {
            require(value >= 0) { "Age cannot be negative" }
            require(value <= 150) { "Age cannot exceed 150" }
            field = value
        }
    
    var email: String = ""
        set(value) {
            require(value.contains("@")) { "Invalid email format" }
            field = value.lowercase()
        }
}
```

## 🎯 Best Practices

### **1. Use Properties for Simple Access**
```kotlin
// ✅ Good - simple property
class Person(val name: String, var age: Int)

// ❌ Avoid - unnecessary getter/setter
class Person(private val _name: String, private var _age: Int) {
    fun getName(): String = _name
    fun getAge(): Int = _age
    fun setAge(age: Int) { _age = age }
}
```

### **2. Use Custom Accessors for Logic**
```kotlin
// ✅ Good - custom logic in getter
class Rectangle(val width: Int, val height: Int) {
    val area: Int
        get() = width * height
}

// ❌ Avoid - storing computed values
class Rectangle(val width: Int, val height: Int) {
    val area: Int = width * height  // Recalculated every time
}
```

### **3. Use Lazy for Expensive Operations**
```kotlin
// ✅ Good - lazy initialization
class DataProcessor(val data: List<String>) {
    val processedData: List<String> by lazy {
        // Expensive processing
        data.map { it.trim().uppercase() }
    }
}

// ❌ Avoid - immediate computation
class DataProcessor(val data: List<String>) {
    val processedData: List<String> = data.map { it.trim().uppercase() }
}
```

## 🔧 Practical Applications

### **1. Configuration Classes**
```kotlin
class AppConfig {
    var databaseUrl: String = "jdbc:default"
        set(value) {
            require(value.startsWith("jdbc:")) { "Invalid database URL format" }
            field = value
        }
    
    var maxConnections: Int = 10
        set(value) {
            require(value in 1..100) { "Max connections must be between 1 and 100" }
            field = value
        }
    
    val isConfigured: Boolean
        get() = databaseUrl != "jdbc:default"
}
```

### **2. Data Validation**
```kotlin
class EmailValidator {
    var email: String = ""
        set(value) {
            val emailRegex = Regex("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}\$")
            require(emailRegex.matches(value)) { "Invalid email format" }
            field = value.lowercase()
        }
    
    val isValid: Boolean
        get() = email.isNotBlank()
    
    val domain: String
        get() = email.substringAfter("@")
}
```

### **3. Business Logic**
```kotlin
class Order(val items: List<OrderItem>) {
    val subtotal: Double
        get() = items.sumOf { it.price * it.quantity }
    
    val tax: Double
        get() = subtotal * 0.08  // 8% tax
    
    val total: Double
        get() = subtotal + tax
    
    val isEligibleForDiscount: Boolean
        get() = subtotal >= 100.0
    
    val discount: Double
        get() = if (isEligibleForDiscount) subtotal * 0.10 else 0.0
    
    val finalTotal: Double
        get() = total - discount
}
```

## 📚 Summary

**Properties** in Kotlin provide:
- **Clean syntax** for class attributes
- **Automatic backing fields** when needed
- **Custom accessors** for validation and logic
- **Type safety** and compile-time checks
- **Performance optimization** through lazy initialization

## 🎯 Key Takeaways

1. **Use `val` for immutable** properties
2. **Use `var` for mutable** properties
3. **Custom getters/setters** for validation and logic
4. **Lazy properties** for expensive operations
5. **Backing fields** with `field` keyword

## 🚀 Next Steps

- Practice creating properties with custom accessors
- Learn about delegated properties
- Explore property delegation patterns
- Understand property initialization order

---

**📁 Source Code:** [26_class_and_constructor.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/26_class_and_constructor.kt)

**🔗 Related Topics:**
- [Classes and Constructors](../oop/01-classes-constructors.md)
- [INIT Block](../oop/05-init-block.md)
- [Inheritance](../oop/02-inheritance.md)
