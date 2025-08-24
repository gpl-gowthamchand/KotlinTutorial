# 🧬 Inheritance in Kotlin

Welcome to the world of inheritance! Inheritance is a fundamental concept in Object-Oriented Programming that allows you to create a hierarchy of classes, where child classes inherit properties and methods from their parent classes. This promotes code reuse and establishes relationships between classes.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand the concept of inheritance
- ✅ Create parent and child classes
- ✅ Use the `open` keyword for inheritance
- ✅ Implement single inheritance properly
- ✅ Create class hierarchies

## 🔍 What You'll Learn

- **Inheritance basics** - Parent-child class relationships
- **Open classes** - Making classes inheritable
- **Single inheritance** - Kotlin's inheritance model
- **Class hierarchies** - Building inheritance chains
- **Code reuse** - Leveraging inherited functionality

## 📝 Prerequisites

- Basic understanding of classes and constructors
- Completed [Classes and Constructors](01-classes-constructors.md) lesson
- Knowledge of properties and methods

## 💻 The Code

Let's examine the inheritance example:

```kotlin
open class Animal {
    var color: String = ""

    fun eat() {
        println("Eat")
    }
}

class Dog : Animal() {
    var bread: String = ""

    fun bark() {
        println("Bark")
    }
}

class Cat : Animal() {
    var age: Int = -1

    fun meow() {
        println("Meow")
    }
}

fun main(args: Array<String>) {
    var dog = Dog()
    dog.bread = "labra"
    dog.color = "black"
    dog.bark()
    dog.eat()

    var cat = Cat()
    cat.age = 7
    cat.color = "brown"
    cat.meow()
    cat.eat()

    var animal = Animal()
    animal.color = "white"
    animal.eat()
}
```

**📁 File:** [27_inheritance.kt](src/27_inheritance.kt)

## 🔍 Code Breakdown

### **Parent Class (Base Class)**

```kotlin
open class Animal {
    var color: String = ""

    fun eat() {
        println("Eat")
    }
}
```

- **`open class Animal`**: `open` keyword makes class inheritable
- **`var color: String`**: Property that child classes will inherit
- **`fun eat()`**: Method that child classes will inherit

### **Child Class (Derived Class)**

```kotlin
class Dog : Animal() {
    var bread: String = ""

    fun bark() {
        println("Bark")
    }
}
```

- **`class Dog : Animal()`**: `Dog` inherits from `Animal`
- **`: Animal()`**: Inheritance syntax with constructor call
- **`var bread: String`**: New property specific to `Dog`
- **`fun bark()`**: New method specific to `Dog`

### **Using Inherited Members**

```kotlin
var dog = Dog()
dog.bread = "labra"    // Dog-specific property
dog.color = "black"    // Inherited property
dog.bark()             // Dog-specific method
dog.eat()              // Inherited method
```

## 🎯 Key Concepts Explained

### **1. Inheritance Basics**

#### **What is Inheritance?**

Inheritance is a mechanism that allows a class to inherit properties and methods from another class. The class that is inherited from is called the **parent class** (or base class, superclass), and the class that inherits is called the **child class** (or derived class, subclass).

#### **Benefits of Inheritance**

1. **Code Reuse**: Common functionality is defined once in the parent class
2. **Hierarchy**: Logical organization of related classes
3. **Polymorphism**: Child classes can be treated as parent class instances
4. **Maintainability**: Changes in parent class affect all child classes

### **2. Open Classes**

#### **The `open` Keyword**

By default, all classes in Kotlin are **final** (cannot be inherited). To make a class inheritable, you must use the `open` keyword.

```kotlin
// ❌ This class cannot be inherited (final by default)
class FinalClass {
    // Class members
}

// ✅ This class can be inherited
open class OpenClass {
    // Class members
}

// ✅ Child class can inherit from OpenClass
class ChildClass : OpenClass() {
    // Inherits from OpenClass
}
```

#### **Open vs Final Classes**

```kotlin
// Final class (default behavior)
class Vehicle {
    var brand: String = ""
    fun start() = println("Vehicle starting")
}

// Open class (can be inherited)
open class Car {
    var model: String = ""
    open fun start() = println("Car starting")
}

// Can inherit from Car
class ElectricCar : Car() {
    var batteryLevel: Int = 100
    override fun start() = println("Electric car starting silently")
}

// Cannot inherit from Vehicle
// class SportsCar : Vehicle() // Compilation error!
```

### **3. Single Inheritance**

#### **Kotlin's Inheritance Model**

Kotlin supports **single inheritance**, meaning a class can inherit from only one parent class. However, a class can implement multiple interfaces.

```kotlin
open class Animal {
    var name: String = ""
}

open class LivingThing {
    var isAlive: Boolean = true
}

// ❌ Multiple inheritance not allowed
// class Dog : Animal(), LivingThing() // Compilation error!

// ✅ Single inheritance
class Dog : Animal() {
    var breed: String = ""
}

// ✅ Multiple interface implementation
interface Movable {
    fun move()
}

interface Soundable {
    fun makeSound()
}

class Cat : Animal(), Movable, Soundable {
    override fun move() = println("Cat is moving")
    override fun makeSound() = println("Meow!")
}
```

### **4. Class Hierarchies**

#### **Building Inheritance Chains**

You can create deep inheritance hierarchies where classes inherit from other child classes.

```kotlin
open class LivingThing {
    var isAlive: Boolean = true
}

open class Animal : LivingThing() {
    var name: String = ""
    var age: Int = 0
}

open class Mammal : Animal() {
    var hasFur: Boolean = true
    var isWarmBlooded: Boolean = true
}

class Dog : Mammal() {
    var breed: String = ""
    var isDomestic: Boolean = true
}

class Cat : Mammal() {
    var isIndoor: Boolean = true
    var huntingSkill: Int = 8
}

// Usage
val dog = Dog()
dog.isAlive = true      // From LivingThing
dog.name = "Buddy"      // From Animal
dog.hasFur = true       // From Mammal
dog.breed = "Golden"    // From Dog
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Inheritance**
Create a simple inheritance hierarchy for shapes:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Shape class and Rectangle/Circle classes that inherit from it
    // Properties: color, area
    // Methods: calculateArea(), displayInfo()
}
```

**Solution:**
```kotlin
open class Shape {
    var color: String = "White"
    
    open fun calculateArea(): Double = 0.0
    
    fun displayInfo() {
        println("Shape color: $color, Area: ${calculateArea()}")
    }
}

class Rectangle : Shape() {
    var width: Double = 0.0
    var height: Double = 0.0
    
    override fun calculateArea(): Double = width * height
    
    fun setDimensions(w: Double, h: Double) {
        width = w
        height = h
    }
}

class Circle : Shape() {
    var radius: Double = 0.0
    
    override fun calculateArea(): Double = Math.PI * radius * radius
    
    fun setRadius(r: Double) {
        radius = r
    }
}

fun main(args: Array<String>) {
    val rectangle = Rectangle()
    rectangle.color = "Blue"
    rectangle.setDimensions(5.0, 3.0)
    rectangle.displayInfo()
    
    val circle = Circle()
    circle.color = "Red"
    circle.setRadius(4.0)
    circle.displayInfo()
}
```

### **Exercise 2: Animal Hierarchy**
Create a more complex animal inheritance hierarchy:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an Animal hierarchy with different types of animals
    // Include properties and methods specific to each type
}
```

**Solution:**
```kotlin
open class Animal {
    var name: String = ""
    var age: Int = 0
    var weight: Double = 0.0
    
    open fun makeSound() = println("Some animal sound")
    
    open fun move() = println("Moving")
    
    fun eat() = println("Eating")
    
    fun sleep() = println("Sleeping")
}

open class Mammal : Animal() {
    var hasFur: Boolean = true
    var isWarmBlooded: Boolean = true
    
    override fun move() = println("Walking on land")
}

open class Bird : Animal() {
    var canFly: Boolean = true
    var wingSpan: Double = 0.0
    
    override fun move() = println("Flying")
}

class Dog : Mammal() {
    var breed: String = ""
    var isDomestic: Boolean = true
    
    override fun makeSound() = println("Woof!")
    
    fun fetch() = println("Fetching ball")
}

class Cat : Mammal() {
    var isIndoor: Boolean = true
    var huntingSkill: Int = 8
    
    override fun makeSound() = println("Meow!")
    
    fun climb() = println("Climbing tree")
}

class Eagle : Bird() {
    var visionRange: Double = 5.0
    
    override fun makeSound() = println("Screech!")
    
    fun hunt() = println("Hunting prey")
}

fun main(args: Array<String>) {
    val dog = Dog()
    dog.name = "Buddy"
    dog.breed = "Golden Retriever"
    dog.makeSound()
    dog.move()
    dog.fetch()
    
    val cat = Cat()
    cat.name = "Whiskers"
    cat.isIndoor = true
    cat.makeSound()
    cat.climb()
    
    val eagle = Eagle()
    eagle.name = "Freedom"
    eagle.canFly = true
    eagle.makeSound()
    eagle.move()
    eagle.hunt()
}
```

### **Exercise 3: Employee Hierarchy**
Create an employee management system with inheritance:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an Employee hierarchy with different types of employees
    // Include salary calculation and role-specific methods
}
```

**Solution:**
```kotlin
open class Employee {
    var id: Int = 0
    var name: String = ""
    var email: String = ""
    var baseSalary: Double = 0.0
    
    open fun calculateSalary(): Double = baseSalary
    
    open fun getRole(): String = "Employee"
    
    fun displayInfo() {
        println("ID: $id, Name: $name, Role: ${getRole()}, Salary: $${calculateSalary()}")
    }
}

class Developer : Employee() {
    var programmingLanguage: String = ""
    var experienceYears: Int = 0
    
    override fun calculateSalary(): Double = baseSalary + (experienceYears * 1000)
    
    override fun getRole(): String = "Developer"
    
    fun code() = println("Coding in $programmingLanguage")
    
    fun debug() = println("Debugging code")
}

class Manager : Employee() {
    var teamSize: Int = 0
    var department: String = ""
    
    override fun calculateSalary(): Double = baseSalary + (teamSize * 500)
    
    override fun getRole(): String = "Manager"
    
    fun leadTeam() = println("Leading team of $teamSize people")
    
    fun conductMeeting() = println("Conducting team meeting")
}

class SalesPerson : Employee() {
    var salesTarget: Double = 0.0
    var commissionRate: Double = 0.05
    
    override fun calculateSalary(): Double = baseSalary + (salesTarget * commissionRate)
    
    override fun getRole(): String = "Sales Person"
    
    fun makeSale(amount: Double) {
        salesTarget += amount
        println("Sale made: $${amount}")
    }
    
    fun generateReport() = println("Generating sales report")
}

fun main(args: Array<String>) {
    val developer = Developer()
    developer.id = 1
    developer.name = "Alice"
    developer.baseSalary = 60000.0
    developer.programmingLanguage = "Kotlin"
    developer.experienceYears = 3
    developer.displayInfo()
    developer.code()
    
    val manager = Manager()
    manager.id = 2
    manager.name = "Bob"
    manager.baseSalary = 80000.0
    manager.teamSize = 5
    manager.department = "Engineering"
    manager.displayInfo()
    manager.leadTeam()
    
    val salesPerson = SalesPerson()
    salesPerson.id = 3
    salesPerson.name = "Charlie"
    salesPerson.baseSalary = 50000.0
    salesPerson.salesTarget = 100000.0
    salesPerson.displayInfo()
    salesPerson.makeSale(5000.0)
    salesPerson.displayInfo() // Updated salary after sale
}
```

### **Exercise 4: Vehicle Hierarchy**
Create a vehicle management system:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Vehicle hierarchy with different types of vehicles
    // Include fuel efficiency and maintenance methods
}
```

**Solution:**
```kotlin
open class Vehicle {
    var brand: String = ""
    var model: String = ""
    var year: Int = 0
    var fuelType: String = "Gasoline"
    
    open fun startEngine() = println("Engine starting")
    
    open fun stopEngine() = println("Engine stopping")
    
    open fun getFuelEfficiency(): Double = 0.0
    
    fun displayInfo() {
        println("$year $brand $model ($fuelType)")
        println("Fuel Efficiency: ${getFuelEfficiency()} MPG")
    }
}

open class Car : Vehicle() {
    var numberOfDoors: Int = 4
    var transmissionType: String = "Automatic"
    
    override fun getFuelEfficiency(): Double = 25.0
    
    fun openTrunk() = println("Opening trunk")
}

open class Motorcycle : Vehicle() {
    var engineSize: Int = 0
    var hasSidecar: Boolean = false
    
    override fun getFuelEfficiency(): Double = 45.0
    
    fun wheelie() = println("Performing wheelie")
}

class ElectricCar : Car() {
    var batteryCapacity: Int = 0
    var range: Int = 0
    
    init {
        fuelType = "Electric"
    }
    
    override fun getFuelEfficiency(): Double = 100.0 // MPGe
    
    override fun startEngine() = println("Electric motor starting silently")
    
    fun charge() = println("Charging battery")
}

class SportBike : Motorcycle() {
    var topSpeed: Int = 0
    
    override fun getFuelEfficiency(): Double = 35.0
    
    fun accelerate() = println("Accelerating to high speed")
}

fun main(args: Array<String>) {
    val electricCar = ElectricCar()
    electricCar.brand = "Tesla"
    electricCar.model = "Model 3"
    electricCar.year = 2023
    electricCar.batteryCapacity = 75
    electricCar.range = 350
    electricCar.displayInfo()
    electricCar.startEngine()
    electricCar.charge()
    
    val sportBike = SportBike()
    sportBike.brand = "Yamaha"
    sportBike.model = "R1"
    sportBike.year = 2023
    sportBike.engineSize = 1000
    sportBike.topSpeed = 186
    sportBike.displayInfo()
    sportBike.startEngine()
    sportBike.accelerate()
}
```

## 🔍 Advanced Inheritance Patterns

### **1. Constructor Inheritance**

```kotlin
open class Animal(val name: String) {
    var age: Int = 0
    
    constructor(name: String, age: Int): this(name) {
        this.age = age
    }
}

class Dog : Animal {
    var breed: String = ""
    
    constructor(name: String, age: Int, breed: String): super(name, age) {
        this.breed = breed
    }
}

// Usage
val dog = Dog("Buddy", 5, "Golden Retriever")
```

### **2. Abstract Classes with Inheritance**

```kotlin
abstract class Shape {
    abstract fun calculateArea(): Double
    abstract fun calculatePerimeter(): Double
    
    fun displayInfo() {
        println("Area: ${calculateArea()}, Perimeter: ${calculatePerimeter()}")
    }
}

class Rectangle(val width: Double, val height: Double) : Shape() {
    override fun calculateArea(): Double = width * height
    
    override fun calculatePerimeter(): Double = 2 * (width + height)
}

// Usage
val rectangle = Rectangle(5.0, 3.0)
rectangle.displayInfo()
```

### **3. Interface Implementation with Inheritance**

```kotlin
interface Movable {
    fun move()
}

interface Soundable {
    fun makeSound()
}

open class Animal(val name: String) {
    fun eat() = println("Eating")
}

class Dog(name: String) : Animal(name), Movable, Soundable {
    override fun move() = println("Walking")
    override fun makeSound() = println("Woof!")
}

// Usage
val dog = Dog("Buddy")
dog.eat()      // From Animal
dog.move()     // From Movable
dog.makeSound() // From Soundable
```

## 🔍 When to Use Inheritance

### **✅ Use Inheritance When:**

1. **Code reuse**:
   ```kotlin
   open class DatabaseConnection {
       fun connect() = println("Connecting to database")
       fun disconnect() = println("Disconnecting from database")
   }
   
   class MySQLConnection : DatabaseConnection() {
       fun executeQuery() = println("Executing MySQL query")
   }
   ```

2. **Hierarchical relationships**:
   ```kotlin
   open class Shape
   class Circle : Shape()
   class Rectangle : Shape()
   class Triangle : Shape()
   ```

3. **Polymorphism**:
   ```kotlin
   open class Animal
   class Dog : Animal()
   class Cat : Animal()
   
   fun processAnimal(animal: Animal) {
       // Can accept any Animal subclass
   }
   ```

### **❌ Avoid Inheritance When:**

1. **Composition is better**:
   ```kotlin
   // ❌ Don't inherit just for code reuse
   class Car : Engine() // Car is not an Engine
   
   // ✅ Use composition instead
   class Car {
       private val engine = Engine()
       fun start() = engine.start()
   }
   ```

2. **Multiple inheritance needed**:
   ```kotlin
   // ❌ Multiple inheritance not allowed
   // class Dog : Animal(), Pet(), Guard()
   
   // ✅ Use interfaces instead
   class Dog : Animal(), Pet, Guard
   ```

## 🚨 Common Mistakes to Avoid

### **1. Forgetting the `open` Keyword**

```kotlin
// ❌ Class cannot be inherited
class Animal {
    var name: String = ""
}

// ❌ Compilation error
class Dog : Animal() // Error: This type is final

// ✅ Make class inheritable
open class Animal {
    var name: String = ""
}

class Dog : Animal() // ✅ Works
```

### **2. Deep Inheritance Hierarchies**

```kotlin
// ❌ Too deep inheritance
open class A
open class B : A()
open class C : B()
open class D : C()
open class E : D()
class F : E() // Too many levels

// ✅ Keep inheritance shallow
open class Animal
class Mammal : Animal()
class Dog : Mammal() // Only 2 levels deep
```

### **3. Inheriting for Implementation**

```kotlin
// ❌ Inheriting just to reuse methods
class FileLogger : DatabaseConnection() // FileLogger is not a DatabaseConnection

// ✅ Use composition instead
class FileLogger {
    private val dbConnection = DatabaseConnection()
    fun log(message: String) {
        dbConnection.connect()
        // Log to file
        dbConnection.disconnect()
    }
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use inheritance for "is-a" relationships**:
   ```kotlin
   // ✅ Dog is an Animal
   open class Animal
   class Dog : Animal()
   ```

2. **Keep inheritance hierarchies shallow**:
   ```kotlin
   // ✅ Maximum 2-3 levels
   open class Vehicle
   class Car : Vehicle()
   class ElectricCar : Car()
   ```

3. **Use abstract classes for common behavior**:
   ```kotlin
   abstract class Shape {
       abstract fun calculateArea(): Double
       fun displayInfo() = println("Area: ${calculateArea()}")
   }
   ```

### **❌ Don'ts**

1. **Don't inherit for code reuse only**:
   ```kotlin
   // ❌ Bad inheritance
   class Logger : DatabaseConnection()
   
   // ✅ Use composition
   class Logger {
       private val db = DatabaseConnection()
   }
   ```

2. **Don't create deep hierarchies**:
   ```kotlin
   // ❌ Too many levels
   A -> B -> C -> D -> E -> F
   
   // ✅ Keep it shallow
   A -> B -> C
   ```

## 🎯 What's Next?

Excellent! You've mastered inheritance in Kotlin. Now you're ready to:

1. **Understand method overriding** → [Method Overriding](03-method-overriding.md)
2. **Explore abstract classes** → [Abstract Classes](04-abstract-classes.md)
3. **Master interfaces** → [Interfaces](05-interfaces.md)
4. **Learn about data classes** → [Data Classes](06-data-classes.md)

## 📚 Additional Resources

- [Kotlin Inheritance](https://kotlinlang.org/docs/inheritance.html)
- [Open Classes](https://kotlinlang.org/docs/inheritance.html#open-classes)
- [Class Hierarchies](https://kotlinlang.org/docs/inheritance.html#overriding-methods)

## 🏆 Summary

- ✅ You understand the concept of inheritance
- ✅ You can create parent and child classes
- ✅ You can use the `open` keyword for inheritance
- ✅ You can implement single inheritance properly
- ✅ You can create class hierarchies
- ✅ You're ready to build complex object-oriented systems!

**Keep practicing and happy coding! 🎉**
