# 🏗️ Classes and Constructors in Kotlin

Welcome to the world of Object-Oriented Programming in Kotlin! Classes are the building blocks of OOP, and constructors are how we create instances of these classes. Kotlin provides powerful and flexible ways to define classes with primary and secondary constructors, along with initialization blocks.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create classes with properties and methods
- ✅ Use primary constructors effectively
- ✅ Implement secondary constructors
- ✅ Understand initialization blocks (init)
- ✅ Create and use class instances

## 🔍 What You'll Learn

- **Class declaration** - Basic class syntax and structure
- **Primary constructors** - Main way to initialize classes
- **Secondary constructors** - Alternative initialization methods
- **Init blocks** - Code that runs during object creation
- **Properties and methods** - Class members and behavior

## 📝 Prerequisites

- Basic understanding of functions
- Completed [Extension Functions](04-extension-functions.md) lesson
- Knowledge of variables and data types

## 💻 The Code

Let's examine the classes and constructors example:

```kotlin
class Student(var name: String) {
    var id: Int = -1

    init {
        println("Student has got a name as $name and id is $id")
    }

    constructor(n: String, id: Int): this(n) {
        // The body of the secondary constructor is called after init block
        this.id = id
    }
}

fun main(args: Array<String>) {
    var student = Student("Steve", 10)
    println(student.id)
}
```

**📁 File:** [26_class_and_constructor.kt](src/26_class_and_constructor.kt)

## 🔍 Code Breakdown

### **Class Declaration**

```kotlin
class Student(var name: String) {
    // Class body
}
```

- **`class Student`**: Class declaration with name
- **`(var name: String)`**: Primary constructor parameter
- **`var name: String`**: Property declaration in constructor

### **Properties**

```kotlin
var id: Int = -1
```

- **`var id: Int`**: Mutable property declaration
- **`= -1`**: Default value assignment

### **Init Block**

```kotlin
init {
    println("Student has got a name as $name and id is $id")
}
```

- **`init`**: Initialization block keyword
- **Executes** during object creation
- **Access** to constructor parameters

### **Secondary Constructor**

```kotlin
constructor(n: String, id: Int): this(n) {
    this.id = id
}
```

- **`constructor`**: Secondary constructor keyword
- **`: this(n)`**: Calls primary constructor
- **`this.id = id`**: Assigns to instance property

## 🎯 Key Concepts Explained

### **1. Class Declaration**

#### **Basic Class Syntax**

```kotlin
class ClassName {
    // Properties
    // Methods
    // Constructors
}
```

**Components:**
- **`class`**: Keyword to declare a class
- **`ClassName`**: Name of the class (PascalCase convention)
- **`{ }`**: Class body containing members

#### **Class with Primary Constructor**

```kotlin
class Person(
    val name: String,
    var age: Int,
    private val email: String
) {
    // Class body
}
```

**Constructor Parameters:**
- **`val name: String`**: Immutable property (read-only)
- **`var age: Int`**: Mutable property (read-write)
- **`private val email: String`**: Private immutable property

### **2. Primary Constructor**

#### **Primary Constructor Syntax**

```kotlin
class Rectangle(
    val width: Double,
    val height: Double
) {
    // Class body
}
```

**Key Points:**
- **Primary constructor** is part of class header
- **Parameters** become class properties
- **No explicit constructor keyword** needed
- **Executes first** during object creation

#### **Property Declarations in Constructor**

```kotlin
class User(
    val id: Int,           // Immutable property
    var name: String,       // Mutable property
    private var email: String, // Private mutable property
    var isActive: Boolean = true // Property with default value
) {
    // Class body
}
```

### **3. Secondary Constructors**

#### **Secondary Constructor Syntax**

```kotlin
class Person(val name: String) {
    var age: Int = 0
    var email: String = ""
    
    // Secondary constructor
    constructor(name: String, age: Int): this(name) {
        this.age = age
    }
    
    // Another secondary constructor
    constructor(name: String, age: Int, email: String): this(name, age) {
        this.email = email
    }
}
```

**Key Points:**
- **`constructor`** keyword required
- **Must call primary constructor** with `this()`
- **Can have multiple** secondary constructors
- **Execute after** primary constructor and init blocks

#### **Constructor Delegation**

```kotlin
class Student(val name: String) {
    var id: Int = -1
    var grade: String = ""
    
    // Secondary constructor calls primary
    constructor(name: String, id: Int): this(name) {
        this.id = id
    }
    
    // Secondary constructor calls another secondary
    constructor(name: String, id: Int, grade: String): this(name, id) {
        this.grade = grade
    }
}
```

### **4. Init Blocks**

#### **Init Block Syntax**

```kotlin
class BankAccount(val accountNumber: String) {
    var balance: Double = 0.0
    var isActive: Boolean = false
    
    init {
        // Validation logic
        if (accountNumber.length < 8) {
            throw IllegalArgumentException("Account number too short")
        }
        
        // Initialize properties
        isActive = true
        println("Account $accountNumber created successfully")
    }
    
    // Another init block
    init {
        println("Account balance initialized to $balance")
    }
}
```

**Key Points:**
- **Multiple init blocks** allowed
- **Execute in order** they appear
- **Access to constructor parameters**
- **Run before** secondary constructor bodies

#### **Init Block Execution Order**

```kotlin
class Example(val param: String) {
    init {
        println("1. First init block")
    }
    
    var property = "Property".also { println("2. Property initialization") }
    
    init {
        println("3. Second init block")
    }
    
    constructor(param: String, extra: Int): this(param) {
        println("4. Secondary constructor body")
    }
}

// Execution order: 1, 2, 3, 4
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Class with Primary Constructor**
Create a simple class for a Book:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Book class and use it
    // Properties: title, author, year, isAvailable
    // Methods: checkOut(), returnBook()
}
```

**Solution:**
```kotlin
class Book(
    val title: String,
    val author: String,
    val year: Int,
    var isAvailable: Boolean = true
) {
    fun checkOut(): Boolean {
        return if (isAvailable) {
            isAvailable = false
            println("'$title' has been checked out")
            true
        } else {
            println("'$title' is already checked out")
            false
        }
    }
    
    fun returnBook(): Boolean {
        return if (!isAvailable) {
            isAvailable = true
            println("'$title' has been returned")
            true
        } else {
            println("'$title' is already available")
            false
        }
    }
}

fun main(args: Array<String>) {
    val book = Book("The Kotlin Guide", "John Doe", 2023)
    println("Book: ${book.title} by ${book.author} (${book.year})")
    
    book.checkOut()
    book.checkOut()  // Already checked out
    book.returnBook()
    book.returnBook() // Already returned
}
```

### **Exercise 2: Class with Secondary Constructor**
Create a Person class with multiple constructors:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Person class with primary and secondary constructors
    // Primary: name, age
    // Secondary: name, age, email
    // Secondary: name, age, email, phone
}
```

**Solution:**
```kotlin
class Person(val name: String, var age: Int) {
    var email: String = ""
    var phone: String = ""
    
    init {
        println("Person '$name' created with age $age")
    }
    
    // Secondary constructor with email
    constructor(name: String, age: Int, email: String): this(name, age) {
        this.email = email
        println("Email set to: $email")
    }
    
    // Secondary constructor with email and phone
    constructor(name: String, age: Int, email: String, phone: String): this(name, age, email) {
        this.phone = phone
        println("Phone set to: $phone")
    }
    
    fun displayInfo() {
        println("Name: $name, Age: $age")
        if (email.isNotEmpty()) println("Email: $email")
        if (phone.isNotEmpty()) println("Phone: $phone")
    }
}

fun main(args: Array<String>) {
    val person1 = Person("Alice", 25)
    val person2 = Person("Bob", 30, "bob@email.com")
    val person3 = Person("Charlie", 35, "charlie@email.com", "+1-555-0123")
    
    println("\nPerson 1:")
    person1.displayInfo()
    
    println("\nPerson 2:")
    person2.displayInfo()
    
    println("\nPerson 3:")
    person3.displayInfo()
}
```

### **Exercise 3: Class with Init Blocks**
Create a BankAccount class with validation:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a BankAccount class with init blocks for validation
    // Properties: accountNumber, balance, owner
    // Validation: account number length, positive balance
}
```

**Solution:**
```kotlin
class BankAccount(
    val accountNumber: String,
    var balance: Double,
    val owner: String
) {
    var isActive: Boolean = false
    
    init {
        // Validate account number
        if (accountNumber.length < 8) {
            throw IllegalArgumentException("Account number must be at least 8 characters")
        }
        
        // Validate balance
        if (balance < 0) {
            throw IllegalArgumentException("Initial balance cannot be negative")
        }
        
        // Validate owner name
        if (owner.trim().isEmpty()) {
            throw IllegalArgumentException("Owner name cannot be empty")
        }
        
        isActive = true
        println("Account validation passed")
    }
    
    init {
        println("Account $accountNumber created for $owner with balance $${balance}")
    }
    
    fun deposit(amount: Double): Boolean {
        if (amount > 0) {
            balance += amount
            println("Deposited $${amount}. New balance: $${balance}")
            return true
        } else {
            println("Invalid deposit amount")
            return false
        }
    }
    
    fun withdraw(amount: Double): Boolean {
        if (amount > 0 && amount <= balance) {
            balance -= amount
            println("Withdrew $${amount}. New balance: $${balance}")
            return true
        } else {
            println("Invalid withdrawal amount or insufficient funds")
            return false
        }
    }
}

fun main(args: Array<String>) {
    try {
        val account = BankAccount("12345678", 1000.0, "John Doe")
        
        account.deposit(500.0)
        account.withdraw(200.0)
        account.withdraw(2000.0)  // Insufficient funds
        
    } catch (e: IllegalArgumentException) {
        println("Error: ${e.message}")
    }
}
```

### **Exercise 4: Complex Class with Multiple Constructors**
Create a Student class with comprehensive constructors:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Student class with multiple constructors and init blocks
    // Properties: name, id, grade, subjects
    // Different constructors for different scenarios
}
```

**Solution:**
```kotlin
class Student(val name: String) {
    var id: Int = -1
    var grade: String = "Not Assigned"
    var subjects: MutableList<String> = mutableListOf()
    
    init {
        println("Student '$name' created")
    }
    
    // Secondary constructor with ID
    constructor(name: String, id: Int): this(name) {
        this.id = id
        println("Student ID set to: $id")
    }
    
    // Secondary constructor with ID and grade
    constructor(name: String, id: Int, grade: String): this(name, id) {
        this.grade = grade
        println("Student grade set to: $grade")
    }
    
    // Secondary constructor with ID, grade, and subjects
    constructor(name: String, id: Int, grade: String, subjects: List<String>): this(name, id, grade) {
        this.subjects.addAll(subjects)
        println("Student subjects set to: ${subjects.joinToString(", ")}")
    }
    
    fun addSubject(subject: String) {
        if (subject !in subjects) {
            subjects.add(subject)
            println("Subject '$subject' added")
        } else {
            println("Subject '$subject' already exists")
        }
    }
    
    fun removeSubject(subject: String) {
        if (subjects.remove(subject)) {
            println("Subject '$subject' removed")
        } else {
            println("Subject '$subject' not found")
        }
    }
    
    fun displayInfo() {
        println("\nStudent Information:")
        println("Name: $name")
        println("ID: $id")
        println("Grade: $grade")
        println("Subjects: ${if (subjects.isEmpty()) "None" else subjects.joinToString(", ")}")
    }
}

fun main(args: Array<String>) {
    val student1 = Student("Alice")
    val student2 = Student("Bob", 1001)
    val student3 = Student("Charlie", 1002, "A")
    val student4 = Student("Diana", 1003, "B", listOf("Math", "Science", "English"))
    
    student1.displayInfo()
    student2.displayInfo()
    student3.displayInfo()
    student4.displayInfo()
    
    // Add subjects to students
    student1.addSubject("History")
    student2.addSubject("Math")
    student2.addSubject("Math")  // Duplicate
    
    student1.displayInfo()
    student2.displayInfo()
}
```

## 🔍 Advanced Class Patterns

### **1. Class with Companion Object**

```kotlin
class DatabaseConnection private constructor(
    val host: String,
    val port: Int,
    val database: String
) {
    companion object {
        fun create(host: String = "localhost", port: Int = 5432, database: String = "default"): DatabaseConnection {
            return DatabaseConnection(host, port, database)
        }
        
        fun createLocal(): DatabaseConnection = create()
        fun createProduction(): DatabaseConnection = create("prod-server.com", 5432, "production")
    }
    
    fun connect(): String = "Connected to $host:$port/$database"
}

// Usage
val localDb = DatabaseConnection.createLocal()
val prodDb = DatabaseConnection.createProduction()
```

### **2. Class with Nested Classes**

```kotlin
class Car(val brand: String, val model: String) {
    class Engine(val type: String, val horsepower: Int) {
        fun start(): String = "Starting $type engine with $horsepower HP"
    }
    
    inner class Dashboard {
        fun showInfo(): String = "Car: $brand $model"
    }
    
    val engine = Engine("V8", 400)
    val dashboard = Dashboard()
}

// Usage
val car = Car("Toyota", "Camry")
println(car.engine.start())
println(car.dashboard.showInfo())
```

### **3. Class with Object Declaration**

```kotlin
class Logger {
    companion object {
        private var logLevel = "INFO"
        
        fun setLogLevel(level: String) {
            logLevel = level
        }
        
        fun log(message: String) {
            println("[$logLevel] $message")
        }
    }
}

// Usage
Logger.setLogLevel("DEBUG")
Logger.log("Application started")
Logger.log("User logged in")
```

## 🔍 When to Use Each Constructor Type

### **✅ Use Primary Constructor When:**

1. **Simple initialization**:
   ```kotlin
   class Point(val x: Double, val y: Double)
   ```

2. **Most common use case**:
   ```kotlin
   class User(val username: String, var isActive: Boolean = true)
   ```

3. **Immutable properties**:
   ```kotlin
   class Configuration(val apiKey: String, val baseUrl: String)
   ```

### **✅ Use Secondary Constructor When:**

1. **Multiple initialization patterns**:
   ```kotlin
   class Person(val name: String) {
       constructor(name: String, age: Int): this(name)
       constructor(name: String, age: Int, email: String): this(name, age)
   }
   ```

2. **Complex initialization logic**:
   ```kotlin
   class DatabaseConnection(val url: String) {
       constructor(host: String, port: Int, database: String): 
           this("jdbc:mysql://$host:$port/$database")
   }
   ```

3. **Factory methods**:
   ```kotlin
   class NetworkRequest(val url: String) {
       constructor(host: String, path: String): 
           this("https://$host$path")
   }
   ```

## 🚨 Common Mistakes to Avoid

### **1. Forgetting to Call Primary Constructor**

```kotlin
// ❌ Missing primary constructor call
class Student(val name: String) {
    constructor(name: String, age: Int) {
        // Missing this(name) call
    }
}

// ✅ Correct - calls primary constructor
class Student(val name: String) {
    constructor(name: String, age: Int): this(name) {
        // Constructor body
    }
}
```

### **2. Accessing Properties Before Initialization**

```kotlin
// ❌ Property accessed before initialization
class Example(val param: String) {
    init {
        println(property)  // property not initialized yet
    }
    
    val property = "value"
}

// ✅ Correct order
class Example(val param: String) {
    val property = "value"
    
    init {
        println(property)  // property is initialized
    }
}
```

### **3. Complex Logic in Primary Constructor**

```kotlin
// ❌ Too complex for primary constructor
class ComplexClass(
    val name: String,
    val age: Int,
    val email: String = if (age >= 18) "$name@adult.com" else "$name@minor.com"
)

// ✅ Better approach
class ComplexClass(val name: String, val age: Int) {
    val email: String = if (age >= 18) "$name@adult.com" else "$name@minor.com"
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use primary constructor for simple cases**:
   ```kotlin
   class User(val name: String, var age: Int)
   ```

2. **Keep constructors focused**:
   ```kotlin
   class Rectangle(val width: Double, val height: Double)
   ```

3. **Use init blocks for validation**:
   ```kotlin
   class BankAccount(val accountNumber: String) {
       init {
           require(accountNumber.length >= 8) { "Account number too short" }
       }
   }
   ```

### **❌ Don'ts**

1. **Don't create too many constructors**:
   ```kotlin
   // ❌ Too many constructors
   class Person(val name: String) {
       constructor(name: String, age: Int): this(name)
       constructor(name: String, age: Int, email: String): this(name, age)
       constructor(name: String, age: Int, email: String, phone: String): this(name, age, email)
       constructor(name: String, age: Int, email: String, phone: String, address: String): this(name, age, email, phone)
   }
   ```

2. **Don't put complex logic in constructors**:
   ```kotlin
   // ❌ Complex logic in constructor
   constructor(name: String, age: Int): this(name) {
       if (age < 0) throw IllegalArgumentException("Age cannot be negative")
       if (age > 150) throw IllegalArgumentException("Age too high")
       this.age = age
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered classes and constructors in Kotlin. Now you're ready to:

1. **Learn about inheritance** → [Inheritance](02-inheritance.md)
2. **Understand method overriding** → [Method Overriding](03-method-overriding.md)
3. **Explore abstract classes** → [Abstract Classes](04-abstract-classes.md)
4. **Master interfaces** → [Interfaces](05-interfaces.md)

## 📚 Additional Resources

- [Kotlin Classes](https://kotlinlang.org/docs/classes.html)
- [Constructors](https://kotlinlang.org/docs/classes.html#constructors)
- [Initialization](https://kotlinlang.org/docs/classes.html#creating-instances-of-classes)

## 🏆 Summary

- ✅ You can create classes with properties and methods
- ✅ You can use primary constructors effectively
- ✅ You can implement secondary constructors
- ✅ You understand initialization blocks (init)
- ✅ You can create and use class instances
- ✅ You're ready to build object-oriented applications!

**Keep practicing and happy coding! 🎉**

