# 📊 Data Class in Kotlin

Data classes in Kotlin are a special type of class designed to hold data. They automatically provide useful methods like `equals()`, `hashCode()`, `toString()`, and `copy()`, making them perfect for representing data structures, DTOs, and value objects.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what data classes are in Kotlin
- ✅ Create and use data classes effectively
- ✅ Know when to use data classes vs regular classes
- ✅ Use data class features like copy and destructuring
- ✅ Apply data classes in real-world scenarios

## 🔍 What You'll Learn

- **Data class syntax** - How to declare and use data classes
- **Automatic methods** - Understanding generated methods
- **Copy functionality** - Using the copy method for immutability
- **Destructuring** - Extracting values from data classes
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of constructors and properties
- ✅ Familiarity with Kotlin syntax
- ✅ Understanding of object-oriented programming

## 💻 The Code

Let's examine the data class examples:

**📁 File:** [32_data_class.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/32_data_class.kt)

## 🔍 Code Breakdown

### **Basic Data Class Declaration**
```kotlin
data class Person(
    val name: String,
    val age: Int,
    val email: String
)
```

**Key Components:**
- `data class` - Keyword that makes this a data class
- `Person` - Class name
- `val name: String` - Immutable property
- `val age: Int` - Immutable property
- `val email: String` - Immutable property

### **Data Class Usage**
```kotlin
val person = Person("John Doe", 30, "john@example.com")
println(person)  // Person(name=John Doe, age=30, email=john@example.com)
```

## 🎯 Key Concepts Explained

### **1. What are Data Classes?**

Data classes in Kotlin:
- **Automatically generate** useful methods
- **Are designed for data storage** rather than behavior
- **Provide immutability** by default (with `val` properties)
- **Support destructuring** for easy value extraction
- **Generate copy methods** for creating modified instances

### **2. Automatically Generated Methods**

| Method | Purpose | Example |
|--------|---------|---------|
| `equals()` | Compare instances | `person1 == person2` |
| `hashCode()` | Generate hash codes | `person.hashCode()` |
| `toString()` | String representation | `person.toString()` |
| `copy()` | Create modified copy | `person.copy(age = 31)` |
| `componentN()` | Destructuring support | `val (name, age) = person` |

### **3. Data Class vs Regular Class**

| Feature | Data Class | Regular Class |
|---------|------------|---------------|
| **Generated methods** | Yes | No |
| **Copy method** | Yes | No |
| **Destructuring** | Yes | No |
| **Inheritance** | No | Yes |
| **Custom methods** | Yes | Yes |

## 🧪 Examples and Exercises

### **Example 1: Basic Data Class**
```kotlin
data class Student(
    val id: String,
    val name: String,
    val grade: Double,
    val subjects: List<String>
)

// Usage
val student = Student("S001", "Alice Johnson", 85.5, listOf("Math", "Science", "English"))
println(student)

// Copy with modifications
val updatedStudent = student.copy(grade = 90.0)
println(updatedStudent)

// Destructuring
val (id, name, grade, subjects) = student
println("Student $name (ID: $id) has grade $grade in subjects: $subjects")
```

### **Example 2: Complex Data Class**
```kotlin
data class Address(
    val street: String,
    val city: String,
    val state: String,
    val zipCode: String,
    val country: String = "USA"  // Default value
) {
    val fullAddress: String
        get() = "$street, $city, $state $zipCode, $country"
}

data class Employee(
    val id: String,
    val name: String,
    val position: String,
    val salary: Double,
    val address: Address,
    val skills: Set<String>
) {
    val isSenior: Boolean
        get() = salary > 80000
    
    val formattedSalary: String
        get() = "$${String.format("%.2f", salary)}"
}

// Usage
val address = Address("123 Main St", "New York", "NY", "10001")
val employee = Employee("E001", "Bob Smith", "Senior Developer", 95000.0, address, setOf("Kotlin", "Java", "Python"))

println(employee)
println("Address: ${employee.address.fullAddress}")
println("Is Senior: ${employee.isSenior}")
println("Salary: ${employee.formattedSalary}")

// Copy with nested modifications
val newAddress = address.copy(city = "Los Angeles", state = "CA", zipCode = "90210")
val relocatedEmployee = employee.copy(address = newAddress)
println("Relocated: $relocatedEmployee")
```

### **Example 3: Data Class with Collections**
```kotlin
data class Order(
    val orderId: String,
    val customerId: String,
    val items: List<OrderItem>,
    val orderDate: String,
    val status: OrderStatus
) {
    val totalAmount: Double
        get() = items.sumOf { it.price * it.quantity }
    
    val itemCount: Int
        get() = items.size
    
    val isCompleted: Boolean
        get() = status == OrderStatus.COMPLETED
}

data class OrderItem(
    val productId: String,
    val productName: String,
    val quantity: Int,
    val price: Double
)

enum class OrderStatus {
    PENDING, PROCESSING, SHIPPED, DELIVERED, COMPLETED, CANCELLED
}

// Usage
val items = listOf(
    OrderItem("P001", "Laptop", 1, 999.99),
    OrderItem("P002", "Mouse", 2, 29.99),
    OrderItem("P003", "Keyboard", 1, 79.99)
)

val order = Order("O001", "C001", items, "2024-01-15", OrderStatus.PROCESSING)

println("Order: $order")
println("Total Amount: $${order.totalAmount}")
println("Item Count: ${order.itemCount}")
println("Status: ${order.status}")

// Update order status
val updatedOrder = order.copy(status = OrderStatus.SHIPPED)
println("Updated Order: $updatedOrder")
```

### **Example 4: Data Class for API Responses**
```kotlin
data class ApiResponse<T>(
    val success: Boolean,
    val data: T?,
    val message: String,
    val timestamp: Long = System.currentTimeMillis()
) {
    val isError: Boolean
        get() = !success
    
    val formattedTimestamp: String
        get() = java.time.Instant.ofEpochMilli(timestamp).toString()
}

data class User(
    val id: String,
    val username: String,
    val email: String,
    val profile: UserProfile
)

data class UserProfile(
    val firstName: String,
    val lastName: String,
    val avatar: String?,
    val bio: String?
) {
    val fullName: String
        get() = "$firstName $lastName"
}

// Usage
val userProfile = UserProfile("John", "Doe", "avatar.jpg", "Software Developer")
val user = User("U001", "johndoe", "john@example.com", userProfile)

val successResponse = ApiResponse(
    success = true,
    data = user,
    message = "User retrieved successfully"
)

val errorResponse = ApiResponse<User>(
    success = false,
    data = null,
    message = "User not found"
)

println("Success Response: $successResponse")
println("Error Response: $errorResponse")
println("User Full Name: ${user.profile.fullName}")
```

## ⚠️ Important Considerations

### **1. Data Class Limitations**
```kotlin
// ❌ Won't work - data class cannot inherit from another class
data class MyDataClass : SomeOtherClass() {
    // Error: Data class cannot have a parent class
}

// ❌ Won't work - data class cannot be abstract
abstract data class AbstractDataClass {
    // Error: Data class cannot be abstract
}

// ❌ Won't work - data class cannot be sealed
sealed data class SealedDataClass {
    // Error: Data class cannot be sealed
}

// ❌ Won't work - data class cannot be inner
class OuterClass {
    inner data class InnerDataClass {
        // Error: Data class cannot be inner
    }
}
```

### **2. Property Requirements**
```kotlin
data class Example(
    val required: String,  // ✅ Required parameter
    val optional: String = "default"  // ✅ Optional parameter with default
    // var mutable: String = "mutable"  // ⚠️ Mutable properties work but not recommended
)

// ✅ Good - immutable properties
data class GoodExample(val name: String, val age: Int)

// ⚠️ Avoid - mutable properties in data classes
data class AvoidExample(var name: String, var age: Int)
```

### **3. Copy Method Behavior**
```kotlin
data class Person(val name: String, val age: Int, val email: String)

val person = Person("John", 30, "john@example.com")

// Copy with specific changes
val olderPerson = person.copy(age = 31)  // Only age changes
val newPerson = person.copy(name = "Jane", email = "jane@example.com")  // Multiple changes

// Copy without changes (creates identical copy)
val identicalPerson = person.copy()

println("Original: $person")
println("Older: $olderPerson")
println("New: $newPerson")
println("Identical: $identicalPerson")
```

## 🎯 Best Practices

### **1. Use Immutable Properties**
```kotlin
// ✅ Good - immutable properties
data class User(val id: String, val name: String, val email: String)

// ❌ Avoid - mutable properties
data class User(var id: String, var name: String, var email: String)
```

### **2. Keep Data Classes Simple**
```kotlin
// ✅ Good - simple data class
data class Point(val x: Double, val y: Double)

// ❌ Avoid - complex logic in data class
data class ComplexPoint(val x: Double, val y: Double) {
    fun distance(other: ComplexPoint): Double {
        val dx = x - other.x
        val dy = y - other.y
        return Math.sqrt(dx * dx + dy * dy)
    }
    
    fun rotate(angle: Double): ComplexPoint {
        val cos = Math.cos(angle)
        val sin = Math.sin(angle)
        return copy(
            x = x * cos - y * sin,
            y = x * sin + y * cos
        )
    }
}
```

### **3. Use for Value Objects**
```kotlin
// ✅ Good - represents a value
data class Money(val amount: Double, val currency: String)

// ❌ Avoid - represents behavior
data class Calculator(val operation: String) {
    fun calculate(a: Double, b: Double): Double {
        return when (operation) {
            "add" -> a + b
            "subtract" -> a - b
            "multiply" -> a * b
            "divide" -> a / b
            else -> throw IllegalArgumentException("Unknown operation")
        }
    }
}
```

## 🔧 Practical Applications

### **1. Configuration Objects**
```kotlin
data class DatabaseConfig(
    val host: String,
    val port: Int,
    val database: String,
    val username: String,
    val password: String,
    val maxConnections: Int = 10,
    val timeout: Int = 30
) {
    val connectionString: String
        get() = "jdbc:postgresql://$host:$port/$database"
}

data class AppConfig(
    val name: String,
    val version: String,
    val debug: Boolean = false,
    val database: DatabaseConfig,
    val api: ApiConfig
)

data class ApiConfig(
    val baseUrl: String,
    val timeout: Int = 5000,
    val retryAttempts: Int = 3
)
```

### **2. DTOs (Data Transfer Objects)**
```kotlin
data class UserDto(
    val id: String,
    val username: String,
    val email: String,
    val firstName: String,
    val lastName: String,
    val isActive: Boolean,
    val createdAt: String
)

data class CreateUserRequest(
    val username: String,
    val email: String,
    val firstName: String,
    val lastName: String,
    val password: String
)

data class UpdateUserRequest(
    val firstName: String? = null,
    val lastName: String? = null,
    val email: String? = null
)
```

### **3. Event Objects**
```kotlin
data class UserEvent(
    val eventId: String,
    val eventType: EventType,
    val userId: String,
    val timestamp: Long,
    val data: Map<String, Any>
)

enum class EventType {
    USER_CREATED, USER_UPDATED, USER_DELETED, USER_LOGIN, USER_LOGOUT
}

data class AuditLog(
    val id: String,
    val action: String,
    val userId: String,
    val resourceType: String,
    val resourceId: String,
    val timestamp: Long,
    val details: String?
)
```

## 📚 Summary

**Data classes** in Kotlin provide:
- **Automatic method generation** (equals, hashCode, toString, copy)
- **Immutable data structures** by default
- **Destructuring support** for easy value extraction
- **Copy functionality** for creating modified instances
- **Clean, concise syntax** for data representation

## 🎯 Key Takeaways

1. **Use `data class`** for classes that primarily hold data
2. **Properties should be immutable** (`val` not `var`)
3. **Copy method** creates new instances with modifications
4. **Destructuring** extracts values easily
5. **Keep data classes simple** and focused on data storage

## 🚀 Next Steps

- Practice creating data classes for different scenarios
- Learn about data class inheritance limitations
- Explore destructuring declarations
- Understand when to use data classes vs regular classes

---

**📁 Source Code:** [32_data_class.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/32_data_class.kt)

**🔗 Related Topics:**
- [Classes and Constructors](../oop/01-classes-constructors.md)
- [Properties](../oop/06-properties.md)
- [Object Declaration](../oop/11-object-declaration.md)
