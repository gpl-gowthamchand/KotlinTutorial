# 🔤 Variables and Data Types in Kotlin

Welcome to the world of variables and data types! This is where you'll learn how to store and manipulate data in your Kotlin programs.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Declare variables using `var` and `val`
- ✅ Understand the difference between mutable and immutable variables
- ✅ Use type inference to let Kotlin determine types automatically
- ✅ Explicitly declare variable types when needed
- ✅ Work with basic data types: Int, Double, Boolean, String, Char

## 🔍 What You'll Learn

- **Variable declaration** - How to create variables in Kotlin
- **Mutability** - Understanding `var` vs `val`
- **Type inference** - Kotlin's automatic type detection
- **Explicit typing** - When and how to specify types manually
- **Basic data types** - Numbers, text, and logical values

## 📝 Prerequisites

- Basic understanding of programming concepts
- Completed [Hello World](01-hello-world.md) lesson

## 💻 The Code

Let's examine the variables and data types example:

```kotlin
fun main(args: Array<String>) {
    // Type inference examples - Kotlin automatically determines the type
    var myNumber = 10       // Type: Int
    var myDecimal = 1.0     // Type: Double (not Float!)
    var isActive = true     // Type: Boolean
    
    // Explicit type declaration
    var myString: String    // Mutable String with explicit type
    myString = "Hello World"
    myString = "Another World"  // Can change value since it's var
    
    // Immutable variable using val
    val myAnotherString = "My constant string value"    // Immutable String
    // myAnotherString = "some value"  // COMPILE ERROR: Cannot reassign val
    
    // Best practice: Use val by default, var only when you need mutability
    val pi = 3.14159        // Immutable constant
    val maxRetries = 3      // Immutable configuration
    
    // Printing values
    println("Number: $myNumber")
    println("Decimal: $myDecimal")
    println("Is Active: $isActive")
    println("String: $myString")
    println("Constant: $myAnotherString")
    println("Pi: $pi")
    println("Max Retries: $maxRetries")
}
```

**📁 File:** [04_variables_data_types.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/04_variables_data_types.kt)

## 🔍 Code Breakdown

### **Variable Declaration with Type Inference**

```kotlin
var myNumber = 10       // Type: Int
var myDecimal = 1.0     // Type: Double
var isActive = true     // Type: Boolean
```

- **`var`**: Declares a mutable variable (can be changed)
- **Type inference**: Kotlin automatically determines the type based on the value
- **`10`** → `Int` (32-bit integer)
- **`1.0`** → `Double` (64-bit floating point)
- **`true`** → `Boolean` (true/false value)

### **Explicit Type Declaration**

```kotlin
var myString: String    // Mutable String with explicit type
myString = "Hello World"
myString = "Another World"  // Can change value since it's var
```

- **`: String`**: Explicitly declares the variable type
- **`var`**: Allows reassignment
- **Multiple assignments**: Can change the value multiple times

### **Immutable Variables with `val`**

```kotlin
val myAnotherString = "My constant string value"    // Immutable String
// myAnotherString = "some value"  // COMPILE ERROR: Cannot reassign val
```

- **`val`**: Declares an immutable variable (cannot be changed)
- **Single assignment**: Value is set once and cannot be modified
- **Compile-time safety**: Kotlin prevents accidental reassignment

## 🎯 Key Concepts Explained

### **1. Variable Declaration Syntax**

```kotlin
// Mutable variable
var variableName: Type = value

// Immutable variable  
val constantName: Type = value

// With type inference
var inferredVariable = value
val inferredConstant = value
```

### **2. Mutability: `var` vs `val`**

| Feature | `var` | `val` |
|---------|-------|-------|
| **Mutability** | Mutable (can change) | Immutable (cannot change) |
| **Reassignment** | ✅ Allowed | ❌ Not allowed |
| **Use case** | When value needs to change | When value should remain constant |
| **Safety** | Less safe | More safe |

### **3. Type Inference**

Kotlin automatically determines the type based on the assigned value:

```kotlin
val number = 42          // Int
val decimal = 3.14       // Double
val text = "Hello"       // String
val flag = true          // Boolean
val character = 'A'      // Char
```

### **4. Explicit Type Declaration**

Sometimes you want to be explicit about types:

```kotlin
var age: Int = 25
var name: String = "John"
var height: Double = 1.75
var isStudent: Boolean = true
```

## 📊 Basic Data Types in Kotlin

### **Numbers**

| Type | Size | Range | Example |
|------|------|-------|---------|
| **Byte** | 8 bits | -128 to 127 | `val byte: Byte = 100` |
| **Short** | 16 bits | -32,768 to 32,767 | `val short: Short = 1000` |
| **Int** | 32 bits | -2³¹ to 2³¹-1 | `val int: Int = 1000000` |
| **Long** | 64 bits | -2⁶³ to 2⁶³-1 | `val long: Long = 1000000000L` |
| **Float** | 32 bits | ±3.4E-38 to ±3.4E+38 | `val float: Float = 3.14f` |
| **Double** | 64 bits | ±1.7E-308 to ±1.7E+308 | `val double: Double = 3.14` |

### **Text**

| Type | Description | Example |
|------|-------------|---------|
| **Char** | Single Unicode character | `val char: Char = 'A'` |
| **String** | Sequence of characters | `val string: String = "Hello"` |

### **Logical**

| Type | Description | Example |
|------|-------------|---------|
| **Boolean** | true or false | `val boolean: Boolean = true` |

## 🧪 Hands-On Exercises

### **Exercise 1: Create Different Variable Types**
Create variables for your personal information using different data types.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val name: String = "Your Name"
    val age: Int = 25
    val height: Double = 1.75
    val isStudent: Boolean = true
    val grade: Char = 'A'
    
    println("Name: $name")
    println("Age: $age")
    println("Height: $height")
    println("Is Student: $isStudent")
    println("Grade: $grade")
}
```

### **Exercise 2: Experiment with Mutability**
Create both `var` and `val` variables and try to reassign them.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    var mutableNumber = 10
    val immutableNumber = 20
    
    println("Mutable: $mutableNumber")
    mutableNumber = 15  // This works
    println("Mutable after change: $mutableNumber")
    
    println("Immutable: $immutableNumber")
    // immutableNumber = 25  // This would cause a compile error
}
```

### **Exercise 3: Type Inference Challenge**
Let Kotlin infer the types and then verify them.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val number = 42
    val decimal = 3.14
    val text = "Hello"
    val flag = true
    
    // Kotlin inferred these types automatically
    println("Number type: ${number::class.simpleName}")
    println("Decimal type: ${decimal::class.simpleName}")
    println("Text type: ${text::class.simpleName}")
    println("Flag type: ${flag::class.simpleName}")
}
```

### **Exercise 4: Calculate with Variables**
Create variables for mathematical calculations.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val radius: Double = 5.0
    val pi: Double = 3.14159
    
    val area = pi * radius * radius
    val circumference = 2 * pi * radius
    
    println("Radius: $radius")
    println("Area: $area")
    println("Circumference: $circumference")
}
```

## 🔍 Understanding Type Inference

### **When Type Inference Works Well**

```kotlin
// Clear and obvious types
val age = 25              // Int
val name = "John"         // String
val isActive = true       // Boolean
val price = 19.99         // Double
```

### **When to Use Explicit Types**

```kotlin
// Unclear or specific types
val number: Long = 1000000000L
val decimal: Float = 3.14f
val character: Char = 'A'
```

## 🚨 Common Mistakes to Avoid

1. **Confusing `var` and `val`**:
   ```kotlin
   val constant = 10
   constant = 20  // ❌ Compile error
   ```

2. **Type mismatch**:
   ```kotlin
   var number: Int = "Hello"  // ❌ Type mismatch
   ```

3. **Forgetting quotes for strings**:
   ```kotlin
   var name = Hello  // ❌ Missing quotes
   var name = "Hello"  // ✅ Correct
   ```

4. **Using wrong number types**:
   ```kotlin
   val decimal: Float = 3.14  // ❌ 3.14 is Double by default
   val decimal: Float = 3.14f  // ✅ Correct
   ```

## 🎯 What's Next?

Great job! You've learned about variables and data types. Now you're ready to:

1. **Explore more data types** → [Data Types Deep Dive](04-data-types.md)
2. **Learn string operations** → [String Interpolation](05-string-interpolation.md)
3. **Understand control flow** → [If Expressions](../control-flow/01-if-expressions.md)
4. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)

## 📚 Additional Resources

- [Kotlin Data Types Documentation](https://kotlinlang.org/docs/basic-types.html)
- [Kotlin Variables Documentation](https://kotlinlang.org/docs/properties.html)
- [Type Inference in Kotlin](https://kotlinlang.org/docs/type-inference.html)

## 🏆 Summary

- ✅ You can declare variables using `var` and `val`
- ✅ You understand the difference between mutable and immutable
- ✅ You can use type inference and explicit typing
- ✅ You know the basic data types in Kotlin
- ✅ You're ready to work with more complex data structures!

**Keep practicing and happy coding! 🎉**
