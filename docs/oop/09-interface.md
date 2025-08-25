# 🔌 Interface in Kotlin

Interfaces in Kotlin are a powerful abstraction mechanism that defines a contract for classes to implement. They provide a way to achieve multiple inheritance and define common behavior that can be shared across different class hierarchies.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what interfaces are in Kotlin
- ✅ Create and implement interfaces
- ✅ Use interface properties and methods
- ✅ Know when to use interfaces vs abstract classes
- ✅ Apply interfaces in real-world scenarios

## 🔍 What You'll Learn

- **Interface syntax** - How to declare and use interfaces
- **Interface implementation** - How classes implement interfaces
- **Interface properties** - Properties in interfaces
- **Multiple inheritance** - Implementing multiple interfaces
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of classes in Kotlin
- ✅ Knowledge of inheritance
- ✅ Understanding of abstract classes
- ✅ Familiarity with Kotlin syntax

## 💻 The Code

Let's examine the interface examples:

**📁 File:** [31_interface.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/31_interface.kt)

## 🔍 Code Breakdown

### **Basic Interface Declaration**
```kotlin
interface Drawable {
    fun draw()
    val color: String
}
```

**Key Components:**
- `interface Drawable` - Interface declaration
- `fun draw()` - Abstract method (no implementation)
- `val color: String` - Abstract property

### **Interface Implementation**
```kotlin
class Circle : Drawable {
    override val color: String = "Red"
    override fun draw() {
        println("Drawing a $color circle")
    }
}
```

## 🎯 Key Concepts Explained

### **1. What are Interfaces?**

Interfaces in Kotlin:
- **Define contracts** that classes must implement
- **Provide abstraction** without implementation details
- **Enable multiple inheritance** (unlike classes)
- **Support default implementations** for methods
- **Can contain properties** and methods

### **2. Interface vs Abstract Class**

| Feature | Interface | Abstract Class |
|---------|-----------|----------------|
| **Inheritance** | Multiple | Single |
| **Constructor** | No | Yes |
| **State** | No | Yes |
| **Default methods** | Yes | Yes |
| **Properties** | Abstract only | Can have state |

### **3. Interface Implementation**

```kotlin
interface A {
    fun methodA()
}

interface B {
    fun methodB()
}

class MyClass : A, B {  // Multiple interface implementation
    override fun methodA() = println("Method A")
    override fun methodB() = println("Method B")
}
```

## 🧪 Examples and Exercises

### **Example 1: Basic Interface Implementation**
```kotlin
interface Animal {
    val name: String
    fun makeSound()
    fun move()
}

class Dog(override val name: String) : Animal {
    override fun makeSound() = println("$name says: Woof!")
    override fun move() = println("$name is running")
}

class Cat(override val name: String) : Animal {
    override fun makeSound() = println("$name says: Meow!")
    override fun move() = println("$name is walking")
}

class Bird(override val name: String) : Animal {
    override fun makeSound() = println("$name says: Tweet!")
    override fun move() = println("$name is flying")
}

// Usage
fun demonstrateInterfaces() {
    val animals: List<Animal> = listOf(
        Dog("Buddy"),
        Cat("Whiskers"),
        Bird("Polly")
    )
    
    animals.forEach { animal ->
        println("${animal.name}:")
        animal.makeSound()
        animal.move()
        println()
    }
}
```

### **Example 2: Interface with Default Methods**
```kotlin
interface Logger {
    fun log(message: String)
    fun logError(error: String) {
        log("ERROR: $error")  // Default implementation
    }
    fun logWarning(warning: String) {
        log("WARNING: $warning")  // Default implementation
    }
}

class ConsoleLogger : Logger {
    override fun log(message: String) {
        println("[${System.currentTimeMillis()}] $message")
    }
}

class FileLogger : Logger {
    override fun log(message: String) {
        // Write to file implementation
        println("Writing to file: $message")
    }
    
    override fun logError(error: String) {
        log("CRITICAL ERROR: $error")  // Override default implementation
    }
}

// Usage
fun demonstrateDefaultMethods() {
    val consoleLogger = ConsoleLogger()
    val fileLogger = FileLogger()
    
    consoleLogger.log("Application started")
    consoleLogger.logWarning("Low memory")
    consoleLogger.logError("Connection failed")
    
    fileLogger.log("Application started")
    fileLogger.logWarning("Low memory")
    fileLogger.logError("Connection failed")
}
```

### **Example 3: Multiple Interface Implementation**
```kotlin
interface Flyable {
    fun fly()
    val maxAltitude: Int
}

interface Swimmable {
    fun swim()
    val maxDepth: Int
}

interface Walkable {
    fun walk()
    val maxSpeed: Int
}

class Duck : Flyable, Swimmable, Walkable {
    override val maxAltitude: Int = 1000
    override val maxDepth: Int = 10
    override val maxSpeed: Int = 20
    
    override fun fly() = println("Duck is flying up to ${maxAltitude}m")
    override fun swim() = println("Duck is swimming down to ${maxDepth}m")
    override fun walk() = println("Duck is walking at ${maxSpeed}km/h")
}

class Fish : Swimmable {
    override val maxDepth: Int = 100
    
    override fun swim() = println("Fish is swimming down to ${maxDepth}m")
}

class Eagle : Flyable, Walkable {
    override val maxAltitude: Int = 5000
    override val maxSpeed: Int = 5
    
    override fun fly() = println("Eagle is flying up to ${maxAltitude}m")
    override fun walk() = println("Eagle is walking at ${maxSpeed}km/h")
}

// Usage
fun demonstrateMultipleInterfaces() {
    val duck = Duck()
    val fish = Fish()
    val eagle = Eagle()
    
    println("Duck capabilities:")
    duck.fly()
    duck.swim()
    duck.walk()
    
    println("\nFish capabilities:")
    fish.swim()
    
    println("\nEagle capabilities:")
    eagle.fly()
    eagle.walk()
}
```

### **Example 4: Interface Properties**
```kotlin
interface Vehicle {
    val brand: String
    val model: String
    val year: Int
    
    val fullName: String
        get() = "$year $brand $model"  // Default implementation
    
    fun start()
    fun stop()
    fun getInfo(): String
}

class Car(
    override val brand: String,
    override val model: String,
    override val year: Int
) : Vehicle {
    override fun start() = println("$fullName is starting")
    override fun stop() = println("$fullName is stopping")
    override fun getInfo() = "Car: $fullName"
}

class Motorcycle(
    override val brand: String,
    override val model: String,
    override val year: Int
) : Vehicle {
    override fun start() = println("$fullName is starting")
    override fun stop() = println("$fullName is stopping")
    override fun getInfo() = "Motorcycle: $fullName"
}

// Usage
fun demonstrateInterfaceProperties() {
    val car = Car("Toyota", "Camry", 2023)
    val motorcycle = Motorcycle("Honda", "CBR", 2023)
    
    println(car.getInfo())
    car.start()
    car.stop()
    
    println(motorcycle.getInfo())
    motorcycle.start()
    motorcycle.stop()
}
```

## ⚠️ Important Considerations

### **1. Interface Method Implementation**
```kotlin
interface MyInterface {
    fun method1()  // Abstract method
    fun method2() = println("Default implementation")  // Default method
}

class MyClass : MyInterface {
    override fun method1() = println("Custom implementation")  // Must implement
    // method2() uses default implementation
}
```

### **2. Interface Property Implementation**
```kotlin
interface MyInterface {
    val property1: String  // Abstract property
    val property2: String
        get() = "Default value"  // Default implementation
}

class MyClass : MyInterface {
    override val property1: String = "Custom value"  // Must implement
    // property2 uses default implementation
}
```

### **3. Multiple Interface Conflicts**
```kotlin
interface A {
    fun method() = "A"
}

interface B {
    fun method() = "B"
}

class MyClass : A, B {
    override fun method(): String {
        return super<A>.method() + " " + super<B>.method()  // Resolve conflict
    }
}
```

## 🎯 Best Practices

### **1. Use Interfaces for Capabilities**
```kotlin
// ✅ Good - interface for capabilities
interface Flyable {
    fun fly()
}

interface Swimmable {
    fun swim()
}

class Duck : Flyable, Swimmable {
    override fun fly() = println("Flying")
    override fun swim() = println("Swimming")
}

// ❌ Avoid - interface for everything
interface Animal {
    val name: String
    fun makeSound()
    fun move()
    fun eat()
    fun sleep()
    // Too many responsibilities
}
```

### **2. Keep Interfaces Focused**
```kotlin
// ✅ Good - focused interface
interface PaymentProcessor {
    fun processPayment(amount: Double): Boolean
    fun getPaymentInfo(): String
}

// ❌ Avoid - unfocused interface
interface PaymentProcessor {
    fun processPayment(amount: Double): Boolean
    fun getPaymentInfo(): String
    fun validateCard(): Boolean
    fun encryptData(): String
    fun sendReceipt(): Boolean
    // Too many responsibilities
}
```

### **3. Use Default Implementations Sparingly**
```kotlin
// ✅ Good - useful default implementation
interface Logger {
    fun log(message: String)
    fun logError(error: String) {
        log("ERROR: $error")  // Useful default
    }
}

// ❌ Avoid - complex default implementation
interface Logger {
    fun log(message: String)
    fun logError(error: String) {
        // Complex error handling logic...
        val timestamp = System.currentTimeMillis()
        val formattedError = "[$timestamp] ERROR: $error"
        val severity = calculateSeverity(error)
        log("$formattedError (Severity: $severity)")
    }
    
    private fun calculateSeverity(error: String): String {
        // Complex logic...
        return "HIGH"
    }
}
```

## 🔧 Practical Applications

### **1. Plugin Architecture**
```kotlin
interface Plugin {
    val name: String
    val version: String
    
    fun initialize()
    fun execute()
    fun cleanup()
}

class DatabasePlugin : Plugin {
    override val name: String = "Database Plugin"
    override val version: String = "1.0.0"
    
    override fun initialize() = println("Database plugin initialized")
    override fun execute() = println("Database plugin executed")
    override fun cleanup() = println("Database plugin cleaned up")
}

class FilePlugin : Plugin {
    override val name: String = "File Plugin"
    override val version: String = "1.0.0"
    
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
            println("Running ${plugin.name} v${plugin.version}")
            plugin.initialize()
            plugin.execute()
            plugin.cleanup()
            println()
        }
    }
}
```

### **2. Strategy Pattern**
```kotlin
interface SortingStrategy {
    fun sort(list: List<Int>): List<Int>
    val name: String
}

class BubbleSort : SortingStrategy {
    override val name: String = "Bubble Sort"
    override fun sort(list: List<Int>): List<Int> {
        println("Using $name")
        return list.sorted()
    }
}

class QuickSort : SortingStrategy {
    override val name: String = "Quick Sort"
    override fun sort(list: List<Int>): List<Int> {
        println("Using $name")
        return list.sorted()
    }
}

class Sorter(private val strategy: SortingStrategy) {
    fun sort(list: List<Int>): List<Int> = strategy.sort(list)
}
```

### **3. Observer Pattern**
```kotlin
interface Observer {
    fun update(data: String)
}

interface Subject {
    fun attach(observer: Observer)
    fun detach(observer: Observer)
    fun notify(data: String)
}

class NewsAgency : Subject {
    private val observers: MutableList<Observer> = mutableListOf()
    
    override fun attach(observer: Observer) {
        observers.add(observer)
    }
    
    override fun detach(observer: Observer) {
        observers.remove(observer)
    }
    
    override fun notify(data: String) {
        observers.forEach { it.update(data) }
    }
    
    fun publishNews(news: String) {
        println("News Agency: Publishing - $news")
        notify(news)
    }
}

class NewsChannel(val name: String) : Observer {
    override fun update(data: String) {
        println("$name received: $data")
    }
}
```

## 📚 Summary

**Interfaces** in Kotlin provide:
- **Contract definition** for classes to implement
- **Multiple inheritance** capability
- **Abstraction** without implementation details
- **Default method implementations**
- **Clean separation** of concerns

## 🎯 Key Takeaways

1. **Use interfaces** for defining contracts
2. **Implement multiple interfaces** for different capabilities
3. **Use default methods** sparingly and wisely
4. **Keep interfaces focused** on specific responsibilities
5. **Interfaces enable** flexible, extensible code

## 🚀 Next Steps

- Practice creating and implementing interfaces
- Learn about interface delegation
- Explore functional interfaces
- Understand interface vs abstract class usage

---

**📁 Source Code:** [31_interface.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/31_interface.kt)

**🔗 Related Topics:**
- [Abstract Classes](../oop/04-abstract-classes.md)
- [Polymorphism](../oop/08-polymorphism.md)
- [Inheritance](../oop/02-inheritance.md)
