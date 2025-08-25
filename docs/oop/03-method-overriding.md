# 🔄 Method Overriding in Kotlin

Welcome to the world of method overriding! Method overriding allows child classes to provide their own implementation of methods inherited from parent classes. This is a powerful feature that enables polymorphism and allows you to customize behavior while maintaining a consistent interface.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Override methods from parent classes
- ✅ Use the `override` keyword properly
- ✅ Call parent class methods with `super`
- ✅ Override properties and their accessors
- ✅ Understand the rules of method overriding

## 🔍 What You'll Learn

- **Method overriding basics** - How to override inherited methods
- **The `override` keyword** - Required for method overriding
- **Property overriding** - Overriding properties and accessors
- **Super calls** - Accessing parent class implementations
- **Override rules** - What can and cannot be overridden

## 📝 Prerequisites

- Basic understanding of inheritance
- Completed [Inheritance](02-inheritance.md) lesson
- Knowledge of classes, properties, and methods

## 💻 The Code

Let's examine the method overriding example:

```kotlin
open class MyAnimal {
    open var color: String = "White"

    open fun eat() {
        println("Animal Eating")
    }
}

class MyDog : MyAnimal() {
    var bread: String = ""

    override var color: String = "Black"

    fun bark() {
        println("Bark")
    }

    override fun eat() {
        super<MyAnimal>.eat()
        println("Dog is eating")
    }
}

fun main(args: Array<String>) {
    var dog = MyDog()
    println(dog.color)
    dog.eat()
}
```

**📁 File:** [28_overriding_methods_properties.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/28_overriding_methods_properties.kt)

## 🔍 Code Breakdown

### **Parent Class with Open Members**

```kotlin
open class MyAnimal {
    open var color: String = "White"

    open fun eat() {
        println("Animal Eating")
    }
}
```

- **`open class MyAnimal`**: Class that can be inherited from
- **`open var color: String`**: Property that can be overridden
- **`open fun eat()`**: Method that can be overridden

### **Child Class with Overrides**

```kotlin
class MyDog : MyAnimal() {
    var bread: String = ""

    override var color: String = "Black"

    override fun eat() {
        super<MyAnimal>.eat()
        println("Dog is eating")
    }
}
```

- **`override var color: String`**: Overrides parent's color property
- **`override fun eat()`**: Overrides parent's eat method
- **`super<MyAnimal>.eat()`**: Calls parent's eat method

## 🎯 Key Concepts Explained

### **1. Method Overriding Basics**

#### **What is Method Overriding?**

Method overriding allows a child class to provide a specific implementation of a method that is already defined in its parent class. The overridden method must have the same signature (name, parameters, and return type) as the parent method.

#### **The `override` Keyword**

In Kotlin, you must explicitly use the `override` keyword when overriding methods. This makes the code more readable and prevents accidental overrides.

```kotlin
open class Parent {
    open fun display() = println("Parent display")
}

class Child : Parent() {
    override fun display() = println("Child display")
}

// Usage
val parent = Parent()
val child = Child()
parent.display()  // "Parent display"
child.display()   // "Child display"
```

### **2. Open vs Final Members**

#### **Open Members (Can be Overridden)**

```kotlin
open class Shape {
    open var color: String = "White"
    open fun calculateArea(): Double = 0.0
    open fun display() = println("Shape with color $color")
}
```

**Key Points:**
- **`open`** keyword allows overriding
- **Properties** can be overridden
- **Methods** can be overridden
- **Default behavior** is final (cannot be overridden)

#### **Final Members (Cannot be Overridden)**

```kotlin
open class Vehicle {
    var brand: String = ""  // Final by default
    
    fun start() = println("Starting vehicle")  // Final by default
    
    open fun accelerate() = println("Accelerating")  // Can be overridden
}

class Car : Vehicle() {
    // ❌ Cannot override final members
    // override var brand: String = "Custom"  // Error
    // override fun start() = println("Custom start")  // Error
    
    // ✅ Can override open members
    override fun accelerate() = println("Car accelerating")
}
```

### **3. Property Overriding**

#### **Overriding Properties**

```kotlin
open class Animal {
    open var name: String = "Unknown"
    open var age: Int = 0
    open val species: String = "Animal"
}

class Dog : Animal() {
    override var name: String = "Dog"
    override var age: Int = 1
    override val species: String = "Canine"
}

// Usage
val dog = Dog()
println(dog.name)     // "Dog"
println(dog.age)      // 1
println(dog.species)  // "Canine"
```

#### **Overriding Property Accessors**

```kotlin
open class Person {
    open var name: String = ""
    open val age: Int = 0
}

class Student : Person() {
    private var _age: Int = 0
    
    override var name: String = ""
        get() = "Student: $field"
        set(value) {
            field = value.uppercase()
        }
    
    override val age: Int
        get() = _age + 1  // Always return age + 1
}

// Usage
val student = Student()
student.name = "john"
println(student.name)  // "Student: JOHN"
student._age = 20
println(student.age)   // 21
```

### **4. Method Overriding with Super Calls**

#### **Calling Parent Methods**

```kotlin
open class Animal {
    open fun makeSound() = println("Some animal sound")
    open fun move() = println("Moving")
}

class Dog : Animal() {
    override fun makeSound() {
        super.makeSound()  // Call parent's makeSound
        println("Woof!")   // Add dog-specific sound
    }
    
    override fun move() {
        println("Dog is walking")  // Completely replace parent's move
    }
}

// Usage
val dog = Dog()
dog.makeSound()  // "Some animal sound" then "Woof!"
dog.move()       // "Dog is walking"
```

#### **Multiple Inheritance with Super Calls**

```kotlin
interface A {
    fun foo() = println("A.foo")
}

interface B {
    fun foo() = println("B.foo")
}

class C : A, B {
    override fun foo() {
        super<A>.foo()  // Call A's foo
        super<B>.foo()  // Call B's foo
        println("C.foo")
    }
}

// Usage
val c = C()
c.foo()  // "A.foo", "B.foo", "C.foo"
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Method Overriding**
Create a simple inheritance hierarchy with method overriding:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Vehicle class and Car/Motorcycle classes that override methods
    // Methods to override: start(), stop(), getInfo()
}
```

**Solution:**
```kotlin
open class Vehicle {
    var brand: String = ""
    var model: String = ""
    
    open fun start() = println("Vehicle starting")
    
    open fun stop() = println("Vehicle stopping")
    
    open fun getInfo(): String = "$brand $model"
}

class Car : Vehicle() {
    var numberOfDoors: Int = 4
    
    override fun start() = println("Car engine starting")
    
    override fun stop() = println("Car engine stopping")
    
    override fun getInfo(): String = "${super.getInfo()} (Car with $numberOfDoors doors)"
}

class Motorcycle : Vehicle() {
    var engineSize: Int = 0
    
    override fun start() = println("Motorcycle engine starting")
    
    override fun stop() = println("Motorcycle engine stopping")
    
    override fun getInfo(): String = "${super.getInfo()} (Motorcycle with ${engineSize}cc engine)"
}

fun main(args: Array<String>) {
    val car = Car()
    car.brand = "Toyota"
    car.model = "Camry"
    car.start()
    car.stop()
    println(car.getInfo())
    
    val motorcycle = Motorcycle()
    motorcycle.brand = "Yamaha"
    motorcycle.model = "R1"
    motorcycle.engineSize = 1000
    motorcycle.start()
    motorcycle.stop()
    println(motorcycle.getInfo())
}
```

### **Exercise 2: Property Overriding**
Create classes with property overriding:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a BankAccount class and different account types with property overriding
    // Override: interestRate, accountType, displayInfo()
}
```

**Solution:**
```kotlin
open class BankAccount {
    open var accountNumber: String = ""
    open var balance: Double = 0.0
    open val interestRate: Double = 0.01
    open val accountType: String = "Basic"
    
    open fun displayInfo() {
        println("Account: $accountNumber")
        println("Type: $accountType")
        println("Balance: $${balance}")
        println("Interest Rate: ${interestRate * 100}%")
    }
    
    open fun calculateInterest(): Double = balance * interestRate
}

class SavingsAccount : BankAccount() {
    override val interestRate: Double = 0.025
    override val accountType: String = "Savings"
    
    override fun displayInfo() {
        super.displayInfo()
        println("Interest Earned: $${calculateInterest()}")
    }
}

class CheckingAccount : BankAccount() {
    override val interestRate: Double = 0.005
    override val accountType: String = "Checking"
    
    override fun displayInfo() {
        super.displayInfo()
        println("No monthly fees")
    }
}

class PremiumAccount : BankAccount() {
    override val interestRate: Double = 0.035
    override val accountType: String = "Premium"
    
    override fun displayInfo() {
        super.displayInfo()
        println("Premium benefits included")
        println("24/7 customer support")
    }
}

fun main(args: Array<String>) {
    val savings = SavingsAccount()
    savings.accountNumber = "SAV001"
    savings.balance = 5000.0
    savings.displayInfo()
    
    println()
    
    val checking = CheckingAccount()
    checking.accountNumber = "CHK001"
    checking.balance = 2000.0
    checking.displayInfo()
    
    println()
    
    val premium = PremiumAccount()
    premium.accountNumber = "PRE001"
    premium.balance = 10000.0
    premium.displayInfo()
}
```

### **Exercise 3: Complex Method Overriding**
Create a shape hierarchy with method overriding:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Shape class with abstract methods and concrete implementations
    // Override: calculateArea(), calculatePerimeter(), displayInfo()
}
```

**Solution:**
```kotlin
abstract class Shape {
    open var color: String = "White"
    
    abstract fun calculateArea(): Double
    
    abstract fun calculatePerimeter(): Double
    
    open fun displayInfo() {
        println("Shape: ${this::class.simpleName}")
        println("Color: $color")
        println("Area: ${calculateArea()}")
        println("Perimeter: ${calculatePerimeter()}")
    }
}

class Rectangle : Shape() {
    var width: Double = 0.0
    var height: Double = 0.0
    
    override fun calculateArea(): Double = width * height
    
    override fun calculatePerimeter(): Double = 2 * (width + height)
    
    override fun displayInfo() {
        super.displayInfo()
        println("Width: $width, Height: $height")
    }
}

class Circle : Shape() {
    var radius: Double = 0.0
    
    override fun calculateArea(): Double = Math.PI * radius * radius
    
    override fun calculatePerimeter(): Double = 2 * Math.PI * radius
    
    override fun displayInfo() {
        super.displayInfo()
        println("Radius: $radius")
    }
}

class Triangle : Shape() {
    var sideA: Double = 0.0
    var sideB: Double = 0.0
    var sideC: Double = 0.0
    
    override fun calculateArea(): Double {
        val s = (sideA + sideB + sideC) / 2
        return Math.sqrt(s * (s - sideA) * (s - sideB) * (s - sideC))
    }
    
    override fun calculatePerimeter(): Double = sideA + sideB + sideC
    
    override fun displayInfo() {
        super.displayInfo()
        println("Sides: $sideA, $sideB, $sideC")
    }
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
    
    println()
    
    val triangle = Triangle()
    triangle.color = "Green"
    triangle.sideA = 3.0
    triangle.sideB = 4.0
    triangle.sideC = 5.0
    triangle.displayInfo()
}
```

### **Exercise 4: Employee Hierarchy with Overriding**
Create an employee system with method and property overriding:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create an Employee hierarchy with different roles and salary calculations
    // Override: calculateSalary(), getRole(), displayInfo()
}
```

**Solution:**
```kotlin
open class Employee {
    open var id: Int = 0
    open var name: String = ""
    open var baseSalary: Double = 0.0
    
    open fun calculateSalary(): Double = baseSalary
    
    open fun getRole(): String = "Employee"
    
    open fun displayInfo() {
        println("ID: $id")
        println("Name: $name")
        println("Role: ${getRole()}")
        println("Salary: $${calculateSalary()}")
    }
}

class Developer : Employee() {
    var programmingLanguage: String = ""
    var experienceYears: Int = 0
    
    override fun calculateSalary(): Double = baseSalary + (experienceYears * 1000)
    
    override fun getRole(): String = "Developer"
    
    override fun displayInfo() {
        super.displayInfo()
        println("Language: $programmingLanguage")
        println("Experience: $experienceYears years")
    }
}

class Manager : Employee() {
    var teamSize: Int = 0
    var department: String = ""
    
    override fun calculateSalary(): Double = baseSalary + (teamSize * 500)
    
    override fun getRole(): String = "Manager"
    
    override fun displayInfo() {
        super.displayInfo()
        println("Team Size: $teamSize")
        println("Department: $department")
    }
}

class SalesPerson : Employee() {
    var salesTarget: Double = 0.0
    var commissionRate: Double = 0.05
    
    override fun calculateSalary(): Double = baseSalary + (salesTarget * commissionRate)
    
    override fun getRole(): String = "Sales Person"
    
    override fun displayInfo() {
        super.displayInfo()
        println("Sales Target: $${salesTarget}")
        println("Commission Rate: ${commissionRate * 100}%")
    }
}

fun main(args: Array<String>) {
    val developer = Developer()
    developer.id = 1
    developer.name = "Alice"
    developer.baseSalary = 60000.0
    developer.programmingLanguage = "Kotlin"
    developer.experienceYears = 3
    developer.displayInfo()
    
    println()
    
    val manager = Manager()
    manager.id = 2
    manager.name = "Bob"
    manager.baseSalary = 80000.0
    manager.teamSize = 5
    manager.department = "Engineering"
    manager.displayInfo()
    
    println()
    
    val salesPerson = SalesPerson()
    salesPerson.id = 3
    salesPerson.name = "Charlie"
    salesPerson.baseSalary = 50000.0
    salesPerson.salesTarget = 100000.0
    salesPerson.displayInfo()
}
```

## 🔍 Advanced Overriding Patterns

### **1. Covariant Return Types**

```kotlin
open class Animal {
    open fun createOffspring(): Animal = Animal()
}

class Dog : Animal() {
    override fun createOffspring(): Dog = Dog()  // Covariant return type
}

// Usage
val dog = Dog()
val offspring = dog.createOffspring()  // Type is Dog, not Animal
```

### **2. Overriding with Different Visibility**

```kotlin
open class Parent {
    protected open fun internalMethod() = println("Parent internal")
}

class Child : Parent() {
    public override fun internalMethod() = println("Child internal")  // Can increase visibility
}

// Usage
val child = Child()
child.internalMethod()  // Now accessible from outside
```

### **3. Overriding with Default Parameters**

```kotlin
open class Parent {
    open fun greet(name: String = "World") = println("Hello, $name!")
}

class Child : Parent() {
    override fun greet(name: String) = println("Hi, $name!")  // Default parameter not inherited
}

// Usage
val child = Child()
child.greet()        // Error: parameter required
child.greet("Alice") // "Hi, Alice!"
```

## 🔍 When to Use Method Overriding

### **✅ Use Method Overriding When:**

1. **Customizing behavior**:
   ```kotlin
   open class Animal {
       open fun makeSound() = println("Some sound")
   }
   
   class Dog : Animal() {
       override fun makeSound() = println("Woof!")  // Custom sound
   }
   ```

2. **Extending functionality**:
   ```kotlin
   open class DatabaseConnection {
       open fun connect() = println("Connecting")
   }
   
   class MySQLConnection : DatabaseConnection() {
       override fun connect() {
           super.connect()  // Call parent
           println("MySQL specific connection")  // Add more
       }
   }
   ```

3. **Polymorphic behavior**:
   ```kotlin
   open class Shape {
       open fun calculateArea(): Double = 0.0
   }
   
   class Circle : Shape() {
       override fun calculateArea(): Double = Math.PI * radius * radius
   }
   
   class Rectangle : Shape() {
       override fun calculateArea(): Double = width * height
   }
   ```

### **❌ Avoid Method Overriding When:**

1. **Breaking the contract**:
   ```kotlin
   // ❌ Don't change expected behavior
   open class FileReader {
       open fun read(): String = "file content"
   }
   
   class NetworkReader : FileReader() {
       override fun read(): String = "network content"  // Unexpected behavior
   }
   ```

2. **Overriding for side effects only**:
   ```kotlin
   // ❌ Don't override just for logging
   open class Calculator {
       open fun add(a: Int, b: Int): Int = a + b
   }
   
   class LoggingCalculator : Calculator() {
       override fun add(a: Int, b: Int): Int {
           println("Adding $a + $b")  // Just logging
           return super.add(a, b)
       }
   }
   ```

## 🚨 Common Mistakes to Avoid

### **1. Forgetting the `override` Keyword**

```kotlin
open class Parent {
    open fun method() = println("Parent")
}

class Child : Parent() {
    // ❌ Missing override keyword
    fun method() = println("Child")  // This creates a new method, doesn't override
}

// Usage
val child = Child()
child.method()  // "Child" (but this is not overriding)
```

### **2. Changing Method Signature**

```kotlin
open class Parent {
    open fun method(param: String) = println("Parent: $param")
}

class Child : Parent() {
    // ❌ Different signature
    override fun method(param: Int) = println("Child: $param")  // Error!
}
```

### **3. Overriding Final Members**

```kotlin
open class Parent {
    fun method() = println("Parent")  // Final by default
}

class Child : Parent() {
    // ❌ Cannot override final method
    override fun method() = println("Child")  // Error!
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Always use `override` keyword**:
   ```kotlin
   class Child : Parent() {
       override fun method() = println("Child implementation")
   }
   ```

2. **Call parent methods when appropriate**:
   ```kotlin
   override fun method() {
       super.method()  // Call parent first
       // Add child-specific behavior
   }
   ```

3. **Maintain the contract**:
   ```kotlin
   open class Database {
       open fun connect(): Boolean = true
   }
   
   class MySQLDatabase : Database() {
       override fun connect(): Boolean {
           // Always return Boolean as expected
           return try {
               // Connection logic
               true
           } catch (e: Exception) {
               false
           }
       }
   }
   ```

### **❌ Don'ts**

1. **Don't override without good reason**:
   ```kotlin
   // ❌ Unnecessary override
   class Child : Parent() {
       override fun method() = super.method()  // Just calls parent
   }
   ```

2. **Don't change method behavior unexpectedly**:
   ```kotlin
   // ❌ Unexpected behavior change
   open class Calculator {
       open fun add(a: Int, b: Int): Int = a + b
   }
   
   class ChildCalculator : Calculator() {
       override fun add(a: Int, b: Int): Int = a * b  // Changed from add to multiply!
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered method overriding in Kotlin. Now you're ready to:

1. **Explore abstract classes** → [Abstract Classes](04-abstract-classes.md)
2. **Master interfaces** → [Interfaces](05-interfaces.md)
3. **Learn about data classes** → [Data Classes](06-data-classes.md)
4. **Understand sealed classes** → [Sealed Classes](07-sealed-classes.md)

## 📚 Additional Resources

- [Kotlin Overriding](https://kotlinlang.org/docs/inheritance.html#overriding-methods)
- [Property Overriding](https://kotlinlang.org/docs/inheritance.html#overriding-properties)
- [Override Rules](https://kotlinlang.org/docs/inheritance.html#overriding-rules)

## 🏆 Summary

- ✅ You can override methods from parent classes
- ✅ You can use the `override` keyword properly
- ✅ You can call parent class methods with `super`
- ✅ You can override properties and their accessors
- ✅ You understand the rules of method overriding
- ✅ You're ready to create polymorphic class hierarchies!

**Keep practicing and happy coding! 🎉**

