# 🎭 Advanced OOP: Enums, Sealed Classes, and Companion Objects

This lesson covers advanced object-oriented programming concepts in Kotlin: enums, sealed classes, and companion objects. These features provide powerful ways to model domain concepts and organize code effectively.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Use enums to represent fixed sets of values with properties and methods
- ✅ Implement sealed classes for restricted class hierarchies
- ✅ Utilize companion objects for static members and factory methods
- ✅ Choose the right approach for different modeling scenarios
- ✅ Apply these patterns in real-world applications

## 🔍 What You'll Learn

- **Enums** - Fixed value sets with properties and behavior
- **Sealed Classes** - Restricted inheritance hierarchies
- **Companion Objects** - Static members and factory patterns
- **Pattern Matching** - Using when expressions with these types
- **Real-world Applications** - Practical use cases and best practices

## 📝 Prerequisites

- Understanding of [Classes and Constructors](../oop/01-classes-constructors.md)
- Knowledge of [Inheritance](../oop/02-inheritance.md)
- Familiarity with [Interfaces](../oop/03-interfaces.md)
- Basic knowledge of [Control Flow](../control-flow/02-when-expressions.md)

## 💻 The Code

Let's examine the advanced OOP examples:

**📁 File:** [34_1_enum_class](../src/34_1_enum_class)
**📁 File:** [34_2_sealed_class.kt](../src/34_2_sealed_class.kt)
**📁 File:** [34_companion_object.kt](../src/34_companion_object.kt)

## 🔍 Code Breakdown

### **1. Enums (Enumerations)**

#### **Basic Enum Declaration**
```kotlin
enum class Direction {
    NORTH, SOUTH, EAST, WEST
}

fun main() {
    val direction = Direction.NORTH
    println("Direction: $direction")
    
    // Iterate through all enum values
    Direction.values().forEach { dir ->
        println("Available direction: $dir")
    }
}
```

#### **Enum with Properties and Methods**
```kotlin
enum class Color(val rgb: Int, val hex: String) {
    RED(0xFF0000, "#FF0000") {
        override fun description() = "Warm and energetic"
    },
    GREEN(0x00FF00, "#00FF00") {
        override fun description() = "Natural and peaceful"
    },
    BLUE(0x0000FF, "#0000FF") {
        override fun description() = "Calm and trustworthy"
    };
    
    abstract fun description()
    
    fun isWarm(): Boolean = this == RED
    fun isCool(): Boolean = this == BLUE
}

fun main() {
    val color = Color.RED
    println("Color: ${color.name}")
    println("RGB: ${color.rgb}")
    println("Hex: ${color.hex}")
    println("Description: ${color.description()}")
    println("Is warm: ${color.isWarm()}")
}
```

#### **Enum with Parameters**
```kotlin
enum class Planet(
    val mass: Double,
    val radius: Double,
    val distanceFromSun: Double
) {
    MERCURY(3.303e23, 2.4397e6, 5.79e10),
    VENUS(4.869e24, 6.0518e6, 1.08e11),
    EARTH(5.976e24, 6.37814e6, 1.496e11),
    MARS(6.421e23, 3.3972e6, 2.279e11);
    
    fun surfaceGravity(): Double {
        val g = 6.67300e-11
        return g * mass / (radius * radius)
    }
    
    fun surfaceWeight(otherMass: Double): Double {
        return otherMass * surfaceGravity()
    }
}

fun main() {
    val earth = Planet.EARTH
    println("Earth surface gravity: ${earth.surfaceGravity()} m/s²")
    
    val myWeight = earth.surfaceWeight(70.0)
    println("My weight on Earth: $myWeight N")
}
```

### **2. Sealed Classes**

#### **Basic Sealed Class**
```kotlin
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val message: String) : Result<Nothing>()
    object Loading : Result<Nothing>()
}

fun processResult(result: Result<String>) {
    when (result) {
        is Result.Success -> {
            println("Success: ${result.data}")
        }
        is Result.Error -> {
            println("Error: ${result.message}")
        }
        is Result.Loading -> {
            println("Loading...")
        }
    }
}

fun main() {
    val results = listOf(
        Result.Success("Data loaded"),
        Result.Error("Network failed"),
        Result.Loading
    )
    
    results.forEach { processResult(it) }
}
```

#### **Sealed Class with Complex Hierarchy**
```kotlin
sealed class Expression {
    data class Number(val value: Double) : Expression()
    data class Sum(val left: Expression, val right: Expression) : Expression()
    data class Product(val left: Expression, val right: Expression) : Expression()
    data class Variable(val name: String) : Expression()
    
    fun evaluate(variables: Map<String, Double> = emptyMap()): Double {
        return when (this) {
            is Number -> value
            is Sum -> left.evaluate(variables) + right.evaluate(variables)
            is Product -> left.evaluate(variables) * right.evaluate(variables)
            is Variable -> variables[name] ?: throw IllegalArgumentException("Variable $name not found")
        }
    }
}

fun main() {
    // Expression: 2 * (x + 3)
    val expression = Expression.Product(
        Expression.Number(2.0),
        Expression.Sum(
            Expression.Variable("x"),
            Expression.Number(3.0)
        )
    )
    
    val variables = mapOf("x" to 5.0)
    val result = expression.evaluate(variables)
    println("2 * (5 + 3) = $result")
}
```

#### **Sealed Class for State Management**
```kotlin
sealed class NetworkState {
    object Idle : NetworkState()
    object Loading : NetworkState()
    data class Success<T>(val data: T) : NetworkState()
    data class Error(val message: String, val code: Int) : NetworkState()
}

class NetworkManager {
    private var currentState: NetworkState = NetworkState.Idle
    
    fun updateState(newState: NetworkState) {
        currentState = newState
        when (newState) {
            is NetworkState.Idle -> println("Network idle")
            is NetworkState.Loading -> println("Network loading...")
            is NetworkState.Success -> println("Network success: ${newState.data}")
            is NetworkState.Error -> println("Network error: ${newState.message} (${newState.code})")
        }
    }
    
    fun getCurrentState(): NetworkState = currentState
}

fun main() {
    val manager = NetworkManager()
    
    manager.updateState(NetworkState.Loading)
    manager.updateState(NetworkState.Success("Data received"))
    manager.updateState(NetworkState.Error("Connection failed", 404))
}
```

### **3. Companion Objects**

#### **Basic Companion Object**
```kotlin
class DatabaseConnection private constructor(val url: String) {
    companion object {
        private var instance: DatabaseConnection? = null
        
        fun getInstance(url: String = "default.db"): DatabaseConnection {
            if (instance == null) {
                instance = DatabaseConnection(url)
            }
            return instance!!
        }
        
        const val DEFAULT_TIMEOUT = 30000
        const val MAX_CONNECTIONS = 10
    }
    
    fun connect() {
        println("Connecting to database: $url")
    }
}

fun main() {
    val db1 = DatabaseConnection.getInstance("production.db")
    val db2 = DatabaseConnection.getInstance("test.db")
    
    println("Same instance: ${db1 === db2}")
    db1.connect()
    
    println("Default timeout: ${DatabaseConnection.DEFAULT_TIMEOUT}ms")
}
```

#### **Companion Object with Factory Methods**
```kotlin
class User private constructor(
    val id: String,
    val name: String,
    val email: String
) {
    companion object {
        fun createGuest(): User {
            return User("guest_${System.currentTimeMillis()}", "Guest", "guest@example.com")
        }
        
        fun createAdmin(name: String, email: String): User {
            return User("admin_${System.currentTimeMillis()}", name, email)
        }
        
        fun createRegular(name: String, email: String): User {
            return User("user_${System.currentTimeMillis()}", name, email)
        }
        
        fun validateEmail(email: String): Boolean {
            return email.contains("@") && email.contains(".")
        }
    }
    
    override fun toString(): String {
        return "User(id='$id', name='$name', email='$email')"
    }
}

fun main() {
    val guest = User.createGuest()
    val admin = User.createAdmin("Admin User", "admin@company.com")
    val regular = User.createRegular("John Doe", "john@email.com")
    
    println("Guest: $guest")
    println("Admin: $admin")
    println("Regular: $regular")
    
    println("Valid email: ${User.validateEmail("test@example.com")}")
    println("Invalid email: ${User.validateEmail("invalid-email")}")
}
```

#### **Companion Object with Extension Functions**
```kotlin
class StringUtils {
    companion object {
        fun isPalindrome(text: String): Boolean {
            val clean = text.lowercase().replace(Regex("[^a-z0-9]"), "")
            return clean == clean.reversed()
        }
        
        fun countWords(text: String): Int {
            return text.trim().split(Regex("\\s+")).size
        }
    }
}

// Extension functions on companion object
fun StringUtils.Companion.capitalizeWords(text: String): String {
    return text.split(" ").joinToString(" ") { word ->
        word.lowercase().replaceFirstChar { it.uppercase() }
    }
}

fun main() {
    val text = "A man a plan a canal Panama"
    
    println("Text: $text")
    println("Is palindrome: ${StringUtils.isPalindrome(text)}")
    println("Word count: ${StringUtils.countWords(text)}")
    println("Capitalized: ${StringUtils.capitalizeWords(text)}")
}
```

### **4. Advanced Patterns**

#### **Enum with Sealed Class Combination**
```kotlin
enum class PaymentMethod {
    CREDIT_CARD, DEBIT_CARD, BANK_TRANSFER, CASH
}

sealed class PaymentResult {
    data class Success(val transactionId: String, val amount: Double) : PaymentResult()
    data class Failure(val reason: String, val code: Int) : PaymentResult()
    object Pending : PaymentResult()
}

class PaymentProcessor {
    fun processPayment(method: PaymentMethod, amount: Double): PaymentResult {
        return when (method) {
            PaymentMethod.CREDIT_CARD -> {
                if (amount > 1000) {
                    PaymentResult.Failure("Amount exceeds limit", 400)
                } else {
                    PaymentResult.Success("TXN_${System.currentTimeMillis()}", amount)
                }
            }
            PaymentMethod.DEBIT_CARD -> {
                PaymentResult.Success("TXN_${System.currentTimeMillis()}", amount)
            }
            PaymentMethod.BANK_TRANSFER -> {
                PaymentResult.Pending
            }
            PaymentMethod.CASH -> {
                PaymentResult.Success("CASH_${System.currentTimeMillis()}", amount)
            }
        }
    }
}

fun main() {
    val processor = PaymentProcessor()
    
    val methods = PaymentMethod.values()
    val amounts = listOf(500.0, 1500.0, 200.0)
    
    methods.forEach { method ->
        amounts.forEach { amount ->
            val result = processor.processPayment(method, amount)
            println("$method - $${amount}: $result")
        }
    }
}
```

#### **Companion Object with Sealed Class**
```kotlin
sealed class ValidationResult {
    object Valid : ValidationResult()
    data class Invalid(val errors: List<String>) : ValidationResult()
}

class UserValidator {
    companion object {
        fun validateName(name: String): ValidationResult {
            val errors = mutableListOf<String>()
            
            if (name.isBlank()) {
                errors.add("Name cannot be blank")
            }
            if (name.length < 2) {
                errors.add("Name must be at least 2 characters")
            }
            if (name.length > 50) {
                errors.add("Name cannot exceed 50 characters")
            }
            
            return if (errors.isEmpty()) ValidationResult.Valid else ValidationResult.Invalid(errors)
        }
        
        fun validateEmail(email: String): ValidationResult {
            val errors = mutableListOf<String>()
            
            if (email.isBlank()) {
                errors.add("Email cannot be blank")
            }
            if (!email.contains("@")) {
                errors.add("Email must contain @ symbol")
            }
            if (!email.contains(".")) {
                errors.add("Email must contain domain")
            }
            
            return if (errors.isEmpty()) ValidationResult.Valid else ValidationResult.Invalid(errors)
        }
        
        fun validateAge(age: Int): ValidationResult {
            return when {
                age < 0 -> ValidationResult.Invalid(listOf("Age cannot be negative"))
                age < 13 -> ValidationResult.Invalid(listOf("Must be at least 13 years old"))
                age > 120 -> ValidationResult.Invalid(listOf("Age seems unrealistic"))
                else -> ValidationResult.Valid
            }
        }
    }
}

fun main() {
    val testCases = listOf(
        "name" to "John",
        "name" to "",
        "name" to "A",
        "email" to "john@example.com",
        "email" to "invalid-email",
        "age" to 25,
        "age" to -5,
        "age" to 150
    )
    
    testCases.forEach { (field, value) ->
        val result = when (field) {
            "name" -> UserValidator.validateName(value as String)
            "email" -> UserValidator.validateEmail(value as String)
            "age" -> UserValidator.validateAge(value as Int)
            else -> ValidationResult.Invalid(listOf("Unknown field"))
        }
        
        println("$field: $value -> $result")
    }
}
```

## 🎯 Key Concepts Explained

### **1. When to Use Each Approach**

| Feature | Use Case | Example |
|---------|----------|---------|
| **Enum** | Fixed set of values with properties/methods | Days of week, colors, status codes |
| **Sealed Class** | Restricted inheritance hierarchy | Result types, state machines, expressions |
| **Companion Object** | Static members, factory methods, utilities | Singletons, validation, constants |

### **2. Pattern Matching with When Expressions**
```kotlin
// Exhaustive when expressions with sealed classes
fun handleResult(result: Result<String>) = when (result) {
    is Result.Success -> "Success: ${result.data}"
    is Result.Error -> "Error: ${result.message}"
    is Result.Loading -> "Loading..."
}

// When with enums
fun getDirectionInfo(direction: Direction) = when (direction) {
    Direction.NORTH -> "Going up"
    Direction.SOUTH -> "Going down"
    Direction.EAST -> "Going right"
    Direction.WEST -> "Going left"
}
```

### **3. Inheritance and Polymorphism**
- **Enums**: Can implement interfaces, have abstract methods
- **Sealed Classes**: Support inheritance, but only within the same file
- **Companion Objects**: Can inherit from other classes, implement interfaces

## 🧪 Running the Examples

### **Step 1: Open the Files**
1. Navigate to `src/34_1_enum_class`
2. Navigate to `src/34_2_sealed_class.kt`
3. Navigate to `src/34_companion_object.kt`
4. Open them in IntelliJ IDEA

### **Step 2: Run the Programs**
1. Right-click on each file
2. Select "Run '[filename]Kt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Enum with Business Logic**
Create an enum for different user roles with associated permissions.

**Solution:**
```kotlin
enum class UserRole(val permissions: List<String>, val maxFileSize: Long) {
    GUEST(emptyList(), 1024 * 1024) {
        override fun canAccessAdminPanel() = false
    },
    USER(listOf("read", "write"), 10 * 1024 * 1024) {
        override fun canAccessAdminPanel() = false
    },
    MODERATOR(listOf("read", "write", "moderate"), 50 * 1024 * 1024) {
        override fun canAccessAdminPanel() = false
    },
    ADMIN(listOf("read", "write", "moderate", "delete", "manage_users"), Long.MAX_VALUE) {
        override fun canAccessAdminPanel() = true
    };
    
    abstract fun canAccessAdminPanel(): Boolean
    
    fun hasPermission(permission: String): Boolean {
        return permissions.contains(permission)
    }
}

fun main() {
    val roles = UserRole.values()
    
    roles.forEach { role ->
        println("Role: ${role.name}")
        println("  Permissions: ${role.permissions}")
        println("  Max file size: ${role.maxFileSize} bytes")
        println("  Can access admin: ${role.canAccessAdminPanel()}")
        println("  Has write permission: ${role.hasPermission("write")}")
        println()
    }
}
```

### **Exercise 2: Sealed Class for API Responses**
Create a sealed class hierarchy for handling different types of API responses.

**Solution:**
```kotlin
sealed class ApiResponse<out T> {
    data class Success<T>(val data: T, val statusCode: Int) : ApiResponse<T>()
    data class Error(val message: String, val statusCode: Int, val timestamp: Long) : ApiResponse<Nothing>()
    data class ValidationError(val field: String, val message: String) : ApiResponse<Nothing>()
    object Unauthorized : ApiResponse<Nothing>()
    object NotFound : ApiResponse<Nothing>()
    object ServerError : ApiResponse<Nothing>()
}

class ApiHandler {
    fun handleResponse(response: ApiResponse<String>) {
        when (response) {
            is ApiResponse.Success -> {
                println("✅ Success (${response.statusCode}): ${response.data}")
            }
            is ApiResponse.Error -> {
                println("❌ Error (${response.statusCode}): ${response.message}")
            }
            is ApiResponse.ValidationError -> {
                println("⚠️ Validation Error in ${response.field}: ${response.message}")
            }
            is ApiResponse.Unauthorized -> {
                println("🚫 Unauthorized access")
            }
            is ApiResponse.NotFound -> {
                println("🔍 Resource not found")
            }
            is ApiResponse.ServerError -> {
                println("💥 Internal server error")
            }
        }
    }
}

fun main() {
    val handler = ApiHandler()
    
    val responses = listOf(
        ApiResponse.Success("User data", 200),
        ApiResponse.Error("Database connection failed", 500, System.currentTimeMillis()),
        ApiResponse.ValidationError("email", "Invalid email format"),
        ApiResponse.Unauthorized,
        ApiResponse.NotFound,
        ApiResponse.ServerError
    )
    
    responses.forEach { response ->
        handler.handleResponse(response)
    }
}
```

### **Exercise 3: Companion Object with Builder Pattern**
Implement a companion object with builder pattern for creating complex objects.

**Solution:**
```kotlin
data class Person(
    val name: String,
    val age: Int,
    val email: String,
    val phone: String?,
    val address: String?
) {
    companion object {
        class Builder {
            private var name: String = ""
            private var age: Int = 0
            private var email: String = ""
            private var phone: String? = null
            private var address: String? = null
            
            fun name(name: String) = apply { this.name = name }
            fun age(age: Int) = apply { this.age = age }
            fun email(email: String) = apply { this.email = email }
            fun phone(phone: String?) = apply { this.phone = phone }
            fun address(address: String?) = apply { this.address = address }
            
            fun build(): Person {
                require(name.isNotBlank()) { "Name is required" }
                require(age > 0) { "Age must be positive" }
                require(email.isNotBlank()) { "Email is required" }
                
                return Person(name, age, email, phone, address)
            }
        }
        
        fun builder() = Builder()
        
        fun createDefault() = Person("Unknown", 18, "unknown@example.com", null, null)
        
        fun validateEmail(email: String): Boolean {
            return email.contains("@") && email.contains(".")
        }
    }
}

fun main() {
    // Using builder pattern
    val person1 = Person.builder()
        .name("John Doe")
        .age(30)
        .email("john@example.com")
        .phone("123-456-7890")
        .address("123 Main St")
        .build()
    
    println("Person 1: $person1")
    
    // Using factory method
    val person2 = Person.createDefault()
    println("Person 2: $person2")
    
    // Validation
    println("Valid email: ${Person.validateEmail("test@example.com")}")
    println("Invalid email: ${Person.validateEmail("invalid")}")
}
```

### **Exercise 4: Combined Pattern**
Create a system that combines enums, sealed classes, and companion objects.

**Solution:**
```kotlin
enum class OrderStatus(val description: String, val canBeModified: Boolean) {
    PENDING("Order is waiting for confirmation", true),
    CONFIRMED("Order has been confirmed", true),
    PROCESSING("Order is being processed", false),
    SHIPPED("Order has been shipped", false),
    DELIVERED("Order has been delivered", false),
    CANCELLED("Order has been cancelled", false);
    
    fun nextPossibleStatuses(): List<OrderStatus> {
        return when (this) {
            PENDING -> listOf(CONFIRMED, CANCELLED)
            CONFIRMED -> listOf(PROCESSING, CANCELLED)
            PROCESSING -> listOf(SHIPPED)
            SHIPPED -> listOf(DELIVERED)
            DELIVERED -> emptyList()
            CANCELLED -> emptyList()
        }
    }
}

sealed class OrderEvent {
    data class Created(val orderId: String, val timestamp: Long) : OrderEvent()
    data class StatusChanged(val orderId: String, val oldStatus: OrderStatus, val newStatus: OrderStatus) : OrderEvent()
    data class Cancelled(val orderId: String, val reason: String) : OrderEvent()
}

class OrderManager {
    companion object {
        private val orders = mutableMapOf<String, OrderStatus>()
        private val events = mutableListOf<OrderEvent>()
        
        fun createOrder(orderId: String): Boolean {
            if (orders.containsKey(orderId)) {
                return false
            }
            
            orders[orderId] = OrderStatus.PENDING
            events.add(OrderEvent.Created(orderId, System.currentTimeMillis()))
            return true
        }
        
        fun changeStatus(orderId: String, newStatus: OrderStatus): Boolean {
            val currentStatus = orders[orderId] ?: return false
            
            if (!currentStatus.nextPossibleStatuses().contains(newStatus)) {
                return false
            }
            
            orders[orderId] = newStatus
            events.add(OrderEvent.StatusChanged(orderId, currentStatus, newStatus))
            return true
        }
        
        fun cancelOrder(orderId: String, reason: String): Boolean {
            val currentStatus = orders[orderId] ?: return false
            
            if (!currentStatus.canBeModified) {
                return false
            }
            
            orders[orderId] = OrderStatus.CANCELLED
            events.add(OrderEvent.Cancelled(orderId, reason))
            return true
        }
        
        fun getOrderStatus(orderId: String): OrderStatus? = orders[orderId]
        
        fun getOrderEvents(orderId: String): List<OrderEvent> {
            return events.filter { event ->
                when (event) {
                    is OrderEvent.Created -> event.orderId == orderId
                    is OrderEvent.StatusChanged -> event.orderId == orderId
                    is OrderEvent.Cancelled -> event.orderId == orderId
                }
            }
        }
    }
}

fun main() {
    val orderId = "ORD-001"
    
    // Create order
    if (OrderManager.createOrder(orderId)) {
        println("Order created: $orderId")
    }
    
    // Change status
    OrderManager.changeStatus(orderId, OrderStatus.CONFIRMED)
    OrderManager.changeStatus(orderId, OrderStatus.PROCESSING)
    
    // Try to cancel (should fail)
    if (!OrderManager.cancelOrder(orderId, "Customer request")) {
        println("Cannot cancel order in ${OrderManager.getOrderStatus(orderId)} status")
    }
    
    // Complete order
    OrderManager.changeStatus(orderId, OrderStatus.SHIPPED)
    OrderManager.changeStatus(orderId, OrderStatus.DELIVERED)
    
    // Display final status and events
    println("Final status: ${OrderManager.getOrderStatus(orderId)}")
    println("Order events:")
    OrderManager.getOrderEvents(orderId).forEach { event ->
        println("  $event")
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Forgetting exhaustive when expressions**: Always handle all sealed class cases ✅
2. **Using enums for complex hierarchies**: Use sealed classes for inheritance ✅
3. **Overusing companion objects**: Don't put everything in companion objects ✅
4. **Ignoring enum properties**: Leverage enum properties and methods ✅

## 🎯 What's Next?

Now that you understand advanced OOP concepts, continue with:

1. **Data Classes** → [Data Classes](../oop/08-data-classes.md)
2. **Object Declarations** → [Object Declarations](../oop/09-object-declarations.md)
3. **Coroutines** → [Coroutines Introduction](../coroutines/01-introduction.md)
4. **Functional Programming** → [Lambdas and Higher-Order Functions](../functional-programming/01-lambdas.md)

## 📚 Additional Resources

- [Official Kotlin Enums Documentation](https://kotlinlang.org/docs/enum-classes.html)
- [Sealed Classes Guide](https://kotlinlang.org/docs/sealed-classes.html)
- [Companion Objects](https://kotlinlang.org/docs/object-declarations.html#companion-objects)

## 🏆 Summary

- ✅ You can use enums to represent fixed sets of values with properties and methods
- ✅ You understand sealed classes for restricted class hierarchies
- ✅ You can utilize companion objects for static members and factory methods
- ✅ You know how to choose the right approach for different modeling scenarios
- ✅ You're ready to apply these patterns in real-world applications!

**Enums, sealed classes, and companion objects are powerful tools for modeling domain concepts. Master them for elegant and maintainable code! 🎉**
