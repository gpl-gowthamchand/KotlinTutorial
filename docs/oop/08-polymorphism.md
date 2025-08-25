# 🔄 Polymorphism in Kotlin

Polymorphism is a fundamental concept in object-oriented programming that allows objects of different types to be treated as objects of a common base type. In Kotlin, polymorphism enables flexible, extensible code through method overriding and interface implementation.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what polymorphism is
- ✅ Implement method overriding
- ✅ Use interface polymorphism
- ✅ Know when to use polymorphism
- ✅ Apply polymorphism in real-world scenarios

## 🔍 What You'll Learn

- **Polymorphism concepts** - Understanding the different types of polymorphism
- **Method overriding** - How to override methods in subclasses
- **Interface polymorphism** - Using interfaces for polymorphic behavior
- **Use cases** - When and where to use polymorphism
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of inheritance
- ✅ Understanding of interfaces
- ✅ Familiarity with method overriding

## 💻 The Code

Let's examine the polymorphism examples:

**📁 File:** [27_inheritance.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/27_inheritance.kt)

## 🔍 Code Breakdown

### **Basic Polymorphism with Inheritance**
```kotlin
open class Animal(val name: String) {
    open fun makeSound(): String = "Some sound"
}

class Dog(name: String) : Animal(name) {
    override fun makeSound(): String = "Woof!"
}

class Cat(name: String) : Animal(name) {
    override fun makeSound(): String = "Meow!"
}
```

**Key Components:**
- `open class Animal` - Base class that can be inherited
- `open fun makeSound()` - Method that can be overridden
- `override fun makeSound()` - Overridden method in subclasses
- Different implementations for each animal type

### **Polymorphic Usage**
```kotlin
val animals: List<Animal> = listOf(
    Dog("Buddy"),
    Cat("Whiskers"),
    Animal("Generic Animal")
)

// Polymorphic behavior
animals.forEach { animal ->
    println("${animal.name} says: ${animal.makeSound()}")
}
```

## 🎯 Key Concepts Explained

### **1. What is Polymorphism?**

Polymorphism means "many forms" and allows:
- **Different objects** to respond to the same method call
- **Code flexibility** through common interfaces
- **Extensibility** without modifying existing code
- **Type safety** while maintaining flexibility

### **2. Types of Polymorphism**

| Type | Description | Example |
|------|-------------|---------|
| **Compile-time** | Method overloading | Multiple methods with same name, different parameters |
| **Runtime** | Method overriding | Subclasses provide different implementations |
| **Interface** | Interface implementation | Different classes implement same interface |

### **3. Polymorphism vs Inheritance**

- **Inheritance** establishes the "is-a" relationship
- **Polymorphism** enables the "behaves-like" relationship
- **Polymorphism** works with inheritance and interfaces
- **Polymorphism** provides runtime flexibility

## 🧪 Examples and Exercises

### **Example 1: Animal Hierarchy**
```kotlin
open class Animal(val name: String, val species: String) {
    open fun makeSound(): String = "Some sound"
    open fun move(): String = "Moving"
    open fun eat(): String = "Eating"
    
    fun describe(): String = "$name is a $species"
}

class Dog(name: String) : Animal(name, "Dog") {
    override fun makeSound(): String = "Woof!"
    override fun move(): String = "Running on four legs"
    override fun eat(): String = "Eating dog food"
}

class Cat(name: String) : Animal(name, "Cat") {
    override fun makeSound(): String = "Meow!"
    override fun move(): String = "Walking gracefully"
    override fun eat(): String = "Eating cat food"
}

class Bird(name: String) : Animal(name, "Bird") {
    override fun makeSound(): String = "Tweet!"
    override fun move(): String = "Flying"
    override fun eat(): String = "Eating seeds"
}

// Polymorphic usage
fun demonstratePolymorphism() {
    val animals: List<Animal> = listOf(
        Dog("Buddy"),
        Cat("Whiskers"),
        Bird("Polly")
    )
    
    animals.forEach { animal ->
        println("${animal.describe()}")
        println("  Sound: ${animal.makeSound()}")
        println("  Movement: ${animal.move()}")
        println("  Eating: ${animal.eat()}")
        println()
    }
}

// Output:
// Buddy is a Dog
//   Sound: Woof!
//   Movement: Running on four legs
//   Eating: Eating dog food
//
// Whiskers is a Cat
//   Sound: Meow!
//   Movement: Walking gracefully
//   Eating: Eating cat food
//
// Polly is a Bird
//   Sound: Tweet!
//   Movement: Flying
//   Eating: Eating seeds
```

### **Example 2: Shape Hierarchy**
```kotlin
abstract class Shape(val name: String) {
    abstract fun calculateArea(): Double
    abstract fun calculatePerimeter(): Double
    
    fun describe(): String = "$name - Area: ${calculateArea()}, Perimeter: ${calculatePerimeter()}"
}

class Circle(val radius: Double) : Shape("Circle") {
    override fun calculateArea(): Double = Math.PI * radius * radius
    override fun calculatePerimeter(): Double = 2 * Math.PI * radius
}

class Rectangle(val width: Double, val height: Double) : Shape("Rectangle") {
    override fun calculateArea(): Double = width * height
    override fun calculatePerimeter(): Double = 2 * (width + height)
}

class Triangle(val sideA: Double, val sideB: Double, val sideC: Double) : Shape("Triangle") {
    override fun calculateArea(): Double {
        val s = (sideA + sideB + sideC) / 2
        return Math.sqrt(s * (s - sideA) * (s - sideB) * (s - sideC))
    }
    
    override fun calculatePerimeter(): Double = sideA + sideB + sideC
}

// Polymorphic usage
fun demonstrateShapePolymorphism() {
    val shapes: List<Shape> = listOf(
        Circle(5.0),
        Rectangle(4.0, 6.0),
        Triangle(3.0, 4.0, 5.0)
    )
    
    shapes.forEach { shape ->
        println(shape.describe())
    }
    
    // Calculate total area
    val totalArea = shapes.sumOf { it.calculateArea() }
    println("Total area of all shapes: $totalArea")
}
```

### **Example 3: Interface Polymorphism**
```kotlin
interface PaymentMethod {
    fun processPayment(amount: Double): Boolean
    fun getPaymentInfo(): String
}

class CreditCard(val cardNumber: String, val expiryDate: String) : PaymentMethod {
    override fun processPayment(amount: Double): Boolean {
        println("Processing credit card payment: $$amount")
        return true
    }
    
    override fun getPaymentInfo(): String = "Credit Card ending in ${cardNumber.takeLast(4)}"
}

class PayPal(val email: String) : PaymentMethod {
    override fun processPayment(amount: Double): Boolean {
        println("Processing PayPal payment: $$amount")
        return true
    }
    
    override fun getPaymentInfo(): String = "PayPal: $email"
}

class BankTransfer(val accountNumber: String) : PaymentMethod {
    override fun processPayment(amount: Double): Boolean {
        println("Processing bank transfer: $$amount")
        return true
    }
    
    override fun getPaymentInfo(): String = "Bank Transfer to account $accountNumber"
}

// Polymorphic usage
fun demonstratePaymentPolymorphism() {
    val paymentMethods: List<PaymentMethod> = listOf(
        CreditCard("1234567890123456", "12/25"),
        PayPal("user@example.com"),
        BankTransfer("987654321")
    )
    
    val amount = 100.0
    
    paymentMethods.forEach { method ->
        println("Using: ${method.getPaymentInfo()}")
        val success = method.processPayment(amount)
        println("Payment ${if (success) "succeeded" else "failed"}")
        println()
    }
}
```

### **Example 4: Employee Management System**
```kotlin
abstract class Employee(val name: String, val id: String) {
    abstract fun calculateSalary(): Double
    abstract fun getRole(): String
    
    fun displayInfo() {
        println("Employee: $name (ID: $id)")
        println("Role: ${getRole()}")
        println("Salary: $${calculateSalary()}")
        println()
    }
}

class Manager(name: String, id: String, val department: String) : Employee(name, id) {
    override fun calculateSalary(): Double = 80000.0
    override fun getRole(): String = "Manager of $department"
}

class Developer(name: String, id: String, val programmingLanguage: String) : Employee(name, id) {
    override fun calculateSalary(): Double = 70000.0
    override fun getRole(): String = "$programmingLanguage Developer"
}

class Designer(name: String, id: String, val designTool: String) : Employee(name, id) {
    override fun calculateSalary(): Double = 65000.0
    override fun getRole(): String = "$designTool Designer"
}

// Polymorphic usage
fun demonstrateEmployeePolymorphism() {
    val employees: List<Employee> = listOf(
        Manager("John Smith", "M001", "Engineering"),
        Developer("Alice Johnson", "D001", "Kotlin"),
        Designer("Bob Wilson", "DS001", "Figma")
    )
    
    // Display all employee information
    employees.forEach { it.displayInfo() }
    
    // Calculate total payroll
    val totalPayroll = employees.sumOf { it.calculateSalary() }
    println("Total monthly payroll: $$totalPayroll")
    
    // Find employees by role type
    val developers = employees.filterIsInstance<Developer>()
    println("Number of developers: ${developers.size}")
}
```

## ⚠️ Important Considerations

### **1. Method Overriding Rules**
```kotlin
open class Base {
    open fun method1() = "Base method1"
    open fun method2() = "Base method2"
    fun method3() = "Base method3"  // Not open, cannot override
}

class Derived : Base() {
    override fun method1() = "Derived method1"  // ✅ Can override
    override fun method2() = "Derived method2"  // ✅ Can override
    // override fun method3() = "Derived method3"  // ❌ Cannot override
}
```

### **2. Property Overriding**
```kotlin
open class Base {
    open val property1: String = "Base property1"
    open var property2: String = "Base property2"
}

class Derived : Base() {
    override val property1: String = "Derived property1"  // ✅ Can override
    override var property2: String = "Derived property2"  // ✅ Can override
}
```

### **3. Constructor Parameters**
```kotlin
open class Base(val name: String) {
    open fun greet() = "Hello, I'm $name"
}

class Derived(name: String, val age: Int) : Base(name) {
    override fun greet() = "Hello, I'm $name and I'm $age years old"
}
```

## 🎯 Best Practices

### **1. Use Abstract Classes for Common Behavior**
```kotlin
// ✅ Good - abstract class with common behavior
abstract class Vehicle(val name: String) {
    fun start() = println("$name is starting")
    fun stop() = println("$name is stopping")
    abstract fun move()
}

class Car(name: String) : Vehicle(name) {
    override fun move() = println("$name is driving on roads")
}

class Boat(name: String) : Vehicle(name) {
    override fun move() = println("$name is sailing on water")
}
```

### **2. Use Interfaces for Capabilities**
```kotlin
// ✅ Good - interface for capabilities
interface Flyable {
    fun fly()
}

interface Swimmable {
    fun swim()
}

class Duck : Animal("Duck"), Flyable, Swimmable {
    override fun fly() = println("Duck is flying")
    override fun swim() = println("Duck is swimming")
}
```

### **3. Keep Overridden Methods Simple**
```kotlin
// ✅ Good - simple, focused overrides
class Dog(name: String) : Animal(name) {
    override fun makeSound(): String = "Woof!"
}

// ❌ Avoid - complex logic in overrides
class Dog(name: String) : Animal(name) {
    override fun makeSound(): String {
        // Complex sound generation logic...
        val time = System.currentTimeMillis()
        val volume = (time % 100) / 100.0
        return if (volume > 0.5) "WOOF!" else "woof"
    }
}
```

## 🔧 Practical Applications

### **1. Plugin Systems**
```kotlin
interface Plugin {
    fun initialize()
    fun execute()
    fun cleanup()
}

class DatabasePlugin : Plugin {
    override fun initialize() = println("Database plugin initialized")
    override fun execute() = println("Database plugin executed")
    override fun cleanup() = println("Database plugin cleaned up")
}

class FilePlugin : Plugin {
    override fun initialize() = println("File plugin initialized")
    override fun execute() = println("File plugin executed")
    override fun cleanup() = println("File plugin cleaned up")
}

class PluginManager {
    private val plugins: MutableList<Plugin> = mutableListOf()
    
    fun addPlugin(plugin: Plugin) {
        plugins.add(plugin)
    }
    
    fun runAllPlugins() {
        plugins.forEach { plugin ->
            plugin.initialize()
            plugin.execute()
            plugin.cleanup()
        }
    }
}
```

### **2. Strategy Pattern**
```kotlin
interface SortingStrategy {
    fun sort(list: List<Int>): List<Int>
}

class BubbleSort : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // Bubble sort implementation
        return list.sorted()
    }
}

class QuickSort : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // Quick sort implementation
        return list.sorted()
    }
}

class Sorter(private val strategy: SortingStrategy) {
    fun sort(list: List<Int>): List<Int> = strategy.sort(list)
}
```

### **3. Factory Pattern**
```kotlin
interface AnimalFactory {
    fun createAnimal(type: String, name: String): Animal
}

class ConcreteAnimalFactory : AnimalFactory {
    override fun createAnimal(type: String, name: String): Animal {
        return when (type.lowercase()) {
            "dog" -> Dog(name)
            "cat" -> Cat(name)
            "bird" -> Bird(name)
            else -> throw IllegalArgumentException("Unknown animal type: $type")
        }
    }
}
```

## 📚 Summary

**Polymorphism** in Kotlin provides:
- **Code flexibility** through common interfaces
- **Extensibility** without modifying existing code
- **Runtime behavior** selection
- **Type safety** with flexibility
- **Clean architecture** through abstraction

## 🎯 Key Takeaways

1. **Use `open` keyword** for classes and methods that can be overridden
2. **Use `override` keyword** when overriding methods
3. **Interfaces provide** polymorphic behavior
4. **Abstract classes** combine common behavior with polymorphism
5. **Polymorphism enables** flexible, extensible code

## 🚀 Next Steps

- Practice creating polymorphic hierarchies
- Learn about sealed classes
- Explore generic polymorphism
- Understand covariance and contravariance

---

**📁 Source Code:** [27_inheritance.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/27_inheritance.kt)

**🔗 Related Topics:**
- [Inheritance](../oop/02-inheritance.md)
- [Method Overriding](../oop/03-method-overriding.md)
- [Abstract Classes](../oop/04-abstract-classes.md)
