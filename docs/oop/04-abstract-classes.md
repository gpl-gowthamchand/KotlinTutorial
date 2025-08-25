# 🎭 Abstract Classes in Kotlin

Welcome to the world of abstract classes! Abstract classes are a powerful feature in Object-Oriented Programming that allows you to create base classes that cannot be instantiated directly but provide a common interface and implementation for their subclasses. They're perfect for creating templates that child classes must implement.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create abstract classes with abstract and concrete members
- ✅ Understand the difference between abstract and open classes
- ✅ Implement abstract methods in concrete subclasses
- ✅ Use abstract classes as base classes
- ✅ Create flexible class hierarchies

## 🔍 What You'll Learn

- **Abstract class basics** - How to define and use abstract classes
- **Abstract vs concrete members** - Understanding what must be implemented
- **Abstract class inheritance** - Creating concrete subclasses
- **Abstract class design patterns** - When and how to use abstract classes
- **Real-world applications** - Practical use cases

## 📝 Prerequisites

- Basic understanding of inheritance and method overriding
- Completed [Method Overriding](03-method-overriding.md) lesson
- Knowledge of classes, properties, and methods

## 💻 The Code

Let's examine the abstract class example:

```kotlin
abstract class MyPerson {
    abstract var name: String

    abstract fun eat()

    open fun getHeight() {}

    fun goToSchool() {}
}

class Indian: MyPerson() {
    override var name: String = "dummy_indian_name"

    override fun eat() {
        // Our own code
    }
}

fun main(args: Array<String>) {
    // var person = MyPerson()   // Not allowed. You cannot create instance of abstract class
    var person = Indian()       // Allowed. Abstract Super class reference variable
                                // pointing to child class object.
    person.name = "Steve"
    person.eat()
    person.goToSchool()
}
```

**📁 File:** [30_abstract_class.kt](src/30_abstract_class.kt)

## 🔍 Code Breakdown

### **Abstract Class Declaration**

```kotlin
abstract class MyPerson {
    abstract var name: String

    abstract fun eat()

    open fun getHeight() {}

    fun goToSchool() {}
}
```

- **`abstract class MyPerson`**: Abstract class declaration
- **`abstract var name: String`**: Abstract property that must be implemented
- **`abstract fun eat()`**: Abstract method that must be implemented
- **`open fun getHeight()`**: Open method that can be overridden
- **`fun goToSchool()`**: Concrete method that cannot be overridden

### **Concrete Subclass Implementation**

```kotlin
class Indian: MyPerson() {
    override var name: String = "dummy_indian_name"

    override fun eat() {
        // Our own code
    }
}
```

- **`class Indian: MyPerson()`**: Concrete class inheriting from abstract class
- **`override var name: String`**: Implementation of abstract property
- **`override fun eat()`**: Implementation of abstract method

## 🎯 Key Concepts Explained

### **1. Abstract Class Basics**

#### **What is an Abstract Class?**

An abstract class is a class that cannot be instantiated directly. It serves as a base class for other classes and can contain both abstract and concrete members. Abstract classes are perfect for creating common functionality that subclasses can inherit and extend.

#### **Abstract Class Characteristics**

```kotlin
abstract class Shape {
    abstract fun calculateArea(): Double      // Must be implemented
    abstract fun calculatePerimeter(): Double // Must be implemented
    
    fun displayInfo() {                      // Concrete method
        println("Area: ${calculateArea()}")
        println("Perimeter: ${calculatePerimeter()}")
    }
}
```

**Key Points:**
- **Cannot be instantiated** directly
- **Can contain abstract members** (properties and methods)
- **Can contain concrete members** (implemented properties and methods)
- **Must be inherited** by concrete subclasses

### **2. Abstract vs Concrete Members**

#### **Abstract Members (Must be Implemented)**

```kotlin
abstract class Animal {
    abstract var name: String           // Abstract property
    abstract fun makeSound()           // Abstract method
    abstract fun move(): String        // Abstract method with return type
}
```

**Abstract Member Rules:**
- **Must be implemented** in concrete subclasses
- **Cannot have implementation** in abstract class
- **Can have different access modifiers** (public, protected, private)
- **Properties can be abstract** (var or val)

#### **Concrete Members (Already Implemented)**

```kotlin
abstract class Vehicle {
    var brand: String = ""             // Concrete property
    
    fun start() = println("Starting")  // Concrete method
    
    open fun accelerate() = println("Accelerating")  // Open concrete method
}
```

**Concrete Member Rules:**
- **Already implemented** in abstract class
- **Can be inherited** by subclasses
- **Can be overridden** if marked as `open`
- **Provide default behavior** for subclasses

### **3. Abstract Class Inheritance**

#### **Creating Concrete Subclasses**

```kotlin
abstract class Database {
    abstract fun connect(): Boolean
    abstract fun disconnect(): Boolean
    abstract fun executeQuery(query: String): String
    
    fun isConnected(): Boolean = true  // Concrete method
}

class MySQLDatabase : Database() {
    override fun connect(): Boolean {
        println("Connecting to MySQL database")
        return true
    }
    
    override fun disconnect(): Boolean {
        println("Disconnecting from MySQL database")
        return true
    }
    
    override fun executeQuery(query: String): String {
        println("Executing MySQL query: $query")
        return "MySQL result"
    }
}

class PostgreSQLDatabase : Database() {
    override fun connect(): Boolean {
        println("Connecting to PostgreSQL database")
        return true
    }
    
    override fun disconnect(): Boolean {
        println("Disconnecting from PostgreSQL database")
        return true
    }
    
    override fun executeQuery(query: String): String {
        println("Executing PostgreSQL query: $query")
        return "PostgreSQL result"
    }
}
```

#### **Using Abstract Classes as Types**

```kotlin
fun processDatabase(database: Database) {
    if (database.connect()) {
        val result = database.executeQuery("SELECT * FROM users")
        println("Query result: $result")
        database.disconnect()
    }
}

// Usage
val mysql = MySQLDatabase()
val postgres = PostgreSQLDatabase()

processDatabase(mysql)      // Works with MySQL
processDatabase(postgres)   // Works with PostgreSQL
```

### **4. Abstract Class Design Patterns**

#### **Template Method Pattern**

```kotlin
abstract class DataProcessor {
    abstract fun readData(): String
    abstract fun processData(data: String): String
    abstract fun writeData(data: String): Boolean
    
    fun execute() {
        val data = readData()
        val processedData = processData(data)
        val success = writeData(processedData)
        
        if (success) {
            println("Data processing completed successfully")
        } else {
            println("Data processing failed")
        }
    }
}

class FileProcessor : DataProcessor() {
    override fun readData(): String = "Reading from file"
    
    override fun processData(data: String): String = "Processing: $data"
    
    override fun writeData(data: String): Boolean = true
}

class NetworkProcessor : DataProcessor() {
    override fun readData(): String = "Reading from network"
    
    override fun processData(data: String): String = "Processing: $data"
    
    override fun writeData(data: String): Boolean = true
}
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Abstract Class**
Create a simple abstract class for shapes:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an abstract Shape class and concrete implementations
    // Abstract methods: calculateArea(), calculatePerimeter()
    // Concrete method: displayInfo()
}
```

**Solution:**
```kotlin
abstract class Shape {
    abstract var color: String
    
    abstract fun calculateArea(): Double
    
    abstract fun calculatePerimeter(): Double
    
    fun displayInfo() {
        println("Shape: ${this::class.simpleName}")
        println("Color: $color")
        println("Area: ${calculateArea()}")
        println("Perimeter: ${calculatePerimeter()}")
    }
}

class Rectangle : Shape() {
    override var color: String = "White"
    var width: Double = 0.0
    var height: Double = 0.0
    
    override fun calculateArea(): Double = width * height
    
    override fun calculatePerimeter(): Double = 2 * (width + height)
}

class Circle : Shape() {
    override var color: String = "White"
    var radius: Double = 0.0
    
    override fun calculateArea(): Double = Math.PI * radius * radius
    
    override fun calculatePerimeter(): Double = 2 * Math.PI * radius
}

fun main(args: Array<String>) {
    val rectangle = Rectangle()
    rectangle.color = "Blue"
    rectangle.width = 5.0
    rectangle.height = 3.0
    rectangle.displayInfo()
    
    println()
    
    val circle = Circle()
    circle.color = "Red"
    circle.radius = 4.0
    circle.displayInfo()
}
```

### **Exercise 2: Abstract Class with Properties**
Create an abstract class for different types of accounts:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an abstract BankAccount class with different account types
    // Abstract properties: accountType, interestRate
    // Abstract methods: calculateInterest(), displayInfo()
}
```

**Solution:**
```kotlin
abstract class BankAccount {
    abstract val accountType: String
    abstract val interestRate: Double
    
    var accountNumber: String = ""
    var balance: Double = 0.0
    
    abstract fun calculateInterest(): Double
    
    abstract fun displayInfo()
    
    fun deposit(amount: Double): Boolean {
        if (amount > 0) {
            balance += amount
            println("Deposited $${amount}. New balance: $${balance}")
            return true
        }
        return false
    }
    
    fun withdraw(amount: Double): Boolean {
        if (amount > 0 && amount <= balance) {
            balance -= amount
            println("Withdrew $${amount}. New balance: $${balance}")
            return true
        }
        return false
    }
}

class SavingsAccount : BankAccount() {
    override val accountType: String = "Savings"
    override val interestRate: Double = 0.025
    
    override fun calculateInterest(): Double = balance * interestRate
    
    override fun displayInfo() {
        println("Account Type: $accountType")
        println("Account Number: $accountNumber")
        println("Balance: $${balance}")
        println("Interest Rate: ${interestRate * 100}%")
        println("Interest Earned: $${calculateInterest()}")
    }
}

class CheckingAccount : BankAccount() {
    override val accountType: String = "Checking"
    override val interestRate: Double = 0.005
    
    override fun calculateInterest(): Double = balance * interestRate
    
    override fun displayInfo() {
        println("Account Type: $accountType")
        println("Account Number: $accountNumber")
        println("Balance: $${balance}")
        println("Interest Rate: ${interestRate * 100}%")
        println("No monthly fees")
    }
}

fun main(args: Array<String>) {
    val savings = SavingsAccount()
    savings.accountNumber = "SAV001"
    savings.deposit(5000.0)
    savings.displayInfo()
    
    println()
    
    val checking = CheckingAccount()
    checking.accountNumber = "CHK001"
    checking.deposit(2000.0)
    checking.withdraw(500.0)
    checking.displayInfo()
}
```

### **Exercise 3: Abstract Class with Template Method**
Create an abstract class for different data processors:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an abstract DataProcessor class with template method pattern
    // Abstract methods: readData(), processData(), writeData()
    // Template method: execute()
}
```

**Solution:**
```kotlin
abstract class DataProcessor {
    abstract fun readData(): String
    abstract fun processData(data: String): String
    abstract fun writeData(data: String): Boolean
    
    fun execute() {
        println("Starting data processing...")
        
        val data = readData()
        println("Data read: $data")
        
        val processedData = processData(data)
        println("Data processed: $processedData")
        
        val success = writeData(processedData)
        
        if (success) {
            println("Data processing completed successfully")
        } else {
            println("Data processing failed")
        }
    }
}

class FileProcessor : DataProcessor() {
    override fun readData(): String = "Reading data from file system"
    
    override fun processData(data: String): String = "File: $data"
    
    override fun writeData(data: String): Boolean {
        println("Writing to file: $data")
        return true
    }
}

class DatabaseProcessor : DataProcessor() {
    override fun readData(): String = "Reading data from database"
    
    override fun processData(data: String): String = "Database: $data"
    
    override fun writeData(data: String): Boolean {
        println("Writing to database: $data")
        return true
    }
}

class NetworkProcessor : DataProcessor() {
    override fun readData(): String = "Reading data from network"
    
    override fun processData(data: String): String = "Network: $data"
    
    override fun writeData(data: String): Boolean {
        println("Writing to network: $data")
        return true
    }
}

fun main(args: Array<String>) {
    val fileProcessor = FileProcessor()
    fileProcessor.execute()
    
    println()
    
    val dbProcessor = DatabaseProcessor()
    dbProcessor.execute()
    
    println()
    
    val networkProcessor = NetworkProcessor()
    networkProcessor.execute()
}
```

### **Exercise 4: Complex Abstract Class Hierarchy**
Create an abstract class for different types of vehicles:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an abstract Vehicle class with different vehicle types
    // Abstract properties: fuelType, maxSpeed
    // Abstract methods: startEngine(), stopEngine(), getFuelEfficiency()
}
```

**Solution:**
```kotlin
abstract class Vehicle {
    abstract val fuelType: String
    abstract val maxSpeed: Int
    
    var brand: String = ""
    var model: String = ""
    var year: Int = 0
    
    abstract fun startEngine(): String
    
    abstract fun stopEngine(): String
    
    abstract fun getFuelEfficiency(): Double
    
    fun displayInfo() {
        println("Vehicle: $year $brand $model")
        println("Fuel Type: $fuelType")
        println("Max Speed: $maxSpeed mph")
        println("Fuel Efficiency: ${getFuelEfficiency()} MPG")
    }
    
    fun accelerate() = println("Accelerating to $maxSpeed mph")
}

class Car : Vehicle() {
    override val fuelType: String = "Gasoline"
    override val maxSpeed: Int = 120
    
    var numberOfDoors: Int = 4
    
    override fun startEngine(): String = "Car engine starting with key"
    
    override fun stopEngine(): String = "Car engine stopping"
    
    override fun getFuelEfficiency(): Double = 25.0
    
    override fun displayInfo() {
        super.displayInfo()
        println("Number of Doors: $numberOfDoors")
    }
}

class ElectricCar : Vehicle() {
    override val fuelType: String = "Electric"
    override val maxSpeed: Int = 150
    
    var batteryCapacity: Int = 75
    
    override fun startEngine(): String = "Electric motor starting silently"
    
    override fun stopEngine(): String = "Electric motor stopping"
    
    override fun getFuelEfficiency(): Double = 100.0 // MPGe
    
    override fun displayInfo() {
        super.displayInfo()
        println("Battery Capacity: ${batteryCapacity} kWh")
    }
}

class Motorcycle : Vehicle() {
    override val fuelType: String = "Gasoline"
    override val maxSpeed: Int = 180
    
    var engineSize: Int = 1000
    
    override fun startEngine(): String = "Motorcycle engine starting"
    
    override fun stopEngine(): String = "Motorcycle engine stopping"
    
    override fun getFuelEfficiency(): Double = 45.0
    
    override fun displayInfo() {
        super.displayInfo()
        println("Engine Size: ${engineSize}cc")
    }
}

fun main(args: Array<String>) {
    val car = Car()
    car.brand = "Toyota"
    car.model = "Camry"
    car.year = 2023
    car.displayInfo()
    println("Start: ${car.startEngine()}")
    println("Stop: ${car.stopEngine()}")
    
    println()
    
    val electricCar = ElectricCar()
    electricCar.brand = "Tesla"
    electricCar.model = "Model 3"
    electricCar.year = 2023
    electricCar.displayInfo()
    println("Start: ${electricCar.startEngine()}")
    println("Stop: ${electricCar.stopEngine()}")
    
    println()
    
    val motorcycle = Motorcycle()
    motorcycle.brand = "Yamaha"
    motorcycle.model = "R1"
    motorcycle.year = 2023
    motorcycle.displayInfo()
    println("Start: ${motorcycle.startEngine()}")
    println("Stop: ${motorcycle.stopEngine()}")
}
```

## 🔍 Advanced Abstract Class Patterns

### **1. Abstract Class with Companion Object**

```kotlin
abstract class DatabaseConnection {
    abstract fun connect(): Boolean
    abstract fun disconnect(): Boolean
    
    companion object {
        fun create(type: String): DatabaseConnection {
            return when (type.lowercase()) {
                "mysql" -> MySQLConnection()
                "postgresql" -> PostgreSQLConnection()
                else -> throw IllegalArgumentException("Unknown database type: $type")
            }
        }
    }
}

class MySQLConnection : DatabaseConnection() {
    override fun connect(): Boolean = true
    override fun disconnect(): Boolean = true
}

class PostgreSQLConnection : DatabaseConnection() {
    override fun connect(): Boolean = true
    override fun disconnect(): Boolean = true
}

// Usage
val mysql = DatabaseConnection.create("mysql")
val postgres = DatabaseConnection.create("postgresql")
```

### **2. Abstract Class with Sealed Classes**

```kotlin
abstract class Result<out T> {
    abstract fun isSuccess(): Boolean
    abstract fun getOrNull(): T?
    
    sealed class Success<T>(val data: T) : Result<T>() {
        override fun isSuccess(): Boolean = true
        override fun getOrNull(): T = data
    }
    
    sealed class Error(val message: String) : Result<Nothing>() {
        override fun isSuccess(): Boolean = false
        override fun getOrNull(): Nothing? = null
    }
}

// Usage
val success: Result<String> = Result.Success("Data loaded successfully")
val error: Result<String> = Result.Error("Failed to load data")

println(success.isSuccess())  // true
println(error.isSuccess())    // false
```

### **3. Abstract Class with Generic Types**

```kotlin
abstract class Repository<T> {
    abstract fun save(item: T): Boolean
    abstract fun findById(id: String): T?
    abstract fun delete(id: String): Boolean
    
    fun exists(id: String): Boolean = findById(id) != null
    
    fun saveIfNotExists(item: T, id: String): Boolean {
        return if (!exists(id)) {
            save(item)
        } else {
            false
        }
    }
}

data class User(val id: String, val name: String, val email: String)

class UserRepository : Repository<User>() {
    private val users = mutableMapOf<String, User>()
    
    override fun save(item: User): Boolean {
        users[item.id] = item
        return true
    }
    
    override fun findById(id: String): User? = users[id]
    
    override fun delete(id: String): Boolean {
        return users.remove(id) != null
    }
}

// Usage
val userRepo = UserRepository()
val user = User("1", "John Doe", "john@example.com")
userRepo.save(user)
println(userRepo.exists("1"))  // true
```

## 🔍 When to Use Abstract Classes

### **✅ Use Abstract Classes When:**

1. **Common implementation needed**:
   ```kotlin
   abstract class Animal {
       fun eat() = println("Eating")  // Common behavior
       abstract fun makeSound()       // Must be implemented
   }
   ```

2. **Template method pattern**:
   ```kotlin
   abstract class DataProcessor {
       fun execute() {                // Template method
           val data = readData()      // Abstract
           val processed = processData(data)  // Abstract
           writeData(processed)       // Abstract
       }
       
       abstract fun readData(): String
       abstract fun processData(data: String): String
       abstract fun writeData(data: String): Boolean
   }
   ```

3. **State sharing**:
   ```kotlin
   abstract class Connection {
       protected var isConnected = false  // Shared state
       
       abstract fun connect(): Boolean
       abstract fun disconnect(): Boolean
       
       fun getStatus() = if (isConnected) "Connected" else "Disconnected"
   }
   ```

### **❌ Avoid Abstract Classes When:**

1. **Only interface needed**:
   ```kotlin
   // ❌ Don't use abstract class for pure interface
   abstract class Movable {
       abstract fun move()
       abstract fun stop()
   }
   
   // ✅ Use interface instead
   interface Movable {
       fun move()
       fun stop()
   }
   ```

2. **Multiple inheritance needed**:
   ```kotlin
   // ❌ Abstract classes don't support multiple inheritance
   // abstract class A
   // abstract class B
   // class C : A(), B()  // Error!
   
   // ✅ Use interfaces for multiple inheritance
   interface A
   interface B
   class C : A, B  // Works!
   ```

## 🚨 Common Mistakes to Avoid

### **1. Trying to Instantiate Abstract Classes**

```kotlin
abstract class Animal {
    abstract fun makeSound()
}

// ❌ Cannot create instance of abstract class
val animal = Animal()  // Compilation error!

// ✅ Create instance of concrete subclass
class Dog : Animal() {
    override fun makeSound() = println("Woof!")
}

val dog = Dog()  // Works!
```

### **2. Forgetting to Implement Abstract Members**

```kotlin
abstract class Shape {
    abstract fun calculateArea(): Double
}

// ❌ Missing implementation
class Rectangle : Shape() {
    // Error: must implement calculateArea
}

// ✅ Correct implementation
class Rectangle : Shape() {
    override fun calculateArea(): Double = 0.0
}
```

### **3. Mixing Abstract and Final Members**

```kotlin
abstract class Base {
    abstract fun method1()  // Must be implemented
    
    fun method2() = println("Final method")  // Cannot be overridden
}

class Derived : Base() {
    override fun method1() = println("Implemented")
    
    // ❌ Cannot override final method
    // override fun method2() = println("Custom")  // Error!
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use abstract classes for common behavior**:
   ```kotlin
   abstract class Database {
       fun connect() = println("Connecting")  // Common behavior
       abstract fun executeQuery(query: String): String  // Must implement
   }
   ```

2. **Keep abstract methods focused**:
   ```kotlin
   abstract class Shape {
       abstract fun calculateArea(): Double  // Single responsibility
       abstract fun calculatePerimeter(): Double  // Single responsibility
   }
   ```

3. **Provide meaningful default implementations**:
   ```kotlin
   abstract class Animal {
       open fun sleep() = println("Sleeping")  // Default behavior
       abstract fun makeSound()  // Must implement
   }
   ```

### **❌ Don'ts**

1. **Don't create abstract classes with no abstract members**:
   ```kotlin
   // ❌ No abstract members - use regular class instead
   abstract class Utility {
       fun helper1() = println("Helper 1")
       fun helper2() = println("Helper 2")
   }
   
   // ✅ Regular class
   class Utility {
       fun helper1() = println("Helper 1")
       fun helper2() = println("Helper 2")
   }
   ```

2. **Don't make everything abstract**:
   ```kotlin
   // ❌ Too many abstract members
   abstract class Person {
       abstract var name: String
       abstract var age: Int
       abstract var email: String
       abstract fun walk()
       abstract fun talk()
       abstract fun eat()
   }
   
   // ✅ Mix of abstract and concrete
   abstract class Person {
       abstract var name: String
       var age: Int = 0  // Concrete with default
       fun walk() = println("Walking")  // Common behavior
       abstract fun talk()  // Must implement
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered abstract classes in Kotlin. Now you're ready to:

1. **Master interfaces** → [Interfaces](05-interfaces.md)
2. **Learn about data classes** → [Data Classes](06-data-classes.md)
3. **Understand sealed classes** → [Sealed Classes](07-sealed-classes.md)
4. **Explore object declarations** → [Object Declarations](08-object-declarations.md)

## 📚 Additional Resources

- [Kotlin Abstract Classes](https://kotlinlang.org/docs/classes.html#abstract-classes)
- [Abstract Members](https://kotlinlang.org/docs/classes.html#abstract-members)
- [Abstract Class Design](https://kotlinlang.org/docs/classes.html#abstract-classes)

## 🏆 Summary

- ✅ You can create abstract classes with abstract and concrete members
- ✅ You understand the difference between abstract and open classes
- ✅ You can implement abstract methods in concrete subclasses
- ✅ You can use abstract classes as base classes
- ✅ You can create flexible class hierarchies
- ✅ You're ready to design robust object-oriented systems!

**Keep practicing and happy coding! 🎉**

