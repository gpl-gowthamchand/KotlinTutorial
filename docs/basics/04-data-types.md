# 🔢 Data Types Deep Dive in Kotlin

Welcome to the comprehensive guide to data types in Kotlin! In this lesson, you'll explore all the fundamental data types, their characteristics, and how to use them effectively in your programs.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand all basic data types in Kotlin
- ✅ Choose the right data type for your needs
- ✅ Work with numbers, text, and logical values
- ✅ Understand type conversion and casting
- ✅ Use data types efficiently in your programs

## 🔍 What You'll Learn

- **Number types** - Integers, floating-point numbers, and their ranges
- **Text types** - Characters and strings
- **Logical types** - Boolean values
- **Type conversion** - Converting between different types
- **Type safety** - How Kotlin ensures type safety

## 📝 Prerequisites

- Basic understanding of variables
- Completed [Variables and Data Types](02-variables-data-types.md) lesson

## 💻 The Code

Let's examine the data types example:

```kotlin
fun main(args: Array<String>) {
    var name: String
    name = "Kevin"

    var age: Int = 10
    var myAge = 10

    var isAlive: Boolean = true
    var marks: Float = 97.4F
    var percentage: Double = 90.78
    var gender: Char = 'M'

    print(marks)
}
```

**📁 File:** [07_data_types.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/07_data_types.kt)

## 🔍 Code Breakdown

### **String Type**

```kotlin
var name: String
name = "Kevin"
```

- **`String`**: Represents a sequence of characters
- **`"Kevin"`**: String literal (text in double quotes)
- **Mutable**: Can be changed since it's declared with `var`

### **Integer Types**

```kotlin
var age: Int = 10
var myAge = 10
```

- **`Int`**: 32-bit integer type
- **`10`**: Integer literal
- **Type inference**: `myAge` automatically becomes `Int`

### **Boolean Type**

```kotlin
var isAlive: Boolean = true
```

- **`Boolean`**: Represents true or false values
- **`true`**: Boolean literal
- **Use case**: Logical conditions and flags

### **Floating-Point Types**

```kotlin
var marks: Float = 97.4F
var percentage: Double = 90.78
```

- **`Float`**: 32-bit floating-point number
- **`Double`**: 64-bit floating-point number (default for decimals)
- **`97.4F`**: Float literal (note the `F` suffix)
- **`90.78`**: Double literal (default type for decimal numbers)

### **Character Type**

```kotlin
var gender: Char = 'M'
```

- **`Char`**: Represents a single Unicode character
- **`'M'`**: Character literal (single quotes)

## 🎯 Key Concepts Explained

### **1. Number Types in Detail**

#### **Integer Types**

| Type | Size | Range | Suffix | Example |
|------|------|-------|--------|---------|
| **Byte** | 8 bits | -128 to 127 | None | `val byte: Byte = 100` |
| **Short** | 16 bits | -32,768 to 32,767 | None | `val short: Short = 1000` |
| **Int** | 32 bits | -2³¹ to 2³¹-1 | None | `val int: Int = 1000000` |
| **Long** | 64 bits | -2⁶³ to 2⁶³-1 | `L` or `l` | `val long: Long = 1000000000L` |

**When to use each:**
- **`Byte`**: Very small numbers, memory optimization
- **`Short`**: Small numbers, legacy APIs
- **`Int`**: General-purpose integers (default choice)
- **`Long`**: Large numbers, timestamps, IDs

#### **Floating-Point Types**

| Type | Size | Precision | Suffix | Example |
|------|------|-----------|--------|---------|
| **Float** | 32 bits | 6-7 digits | `F` or `f` | `val float: Float = 3.14f` |
| **Double** | 64 bits | 15-17 digits | None | `val double: Double = 3.14` |

**When to use each:**
- **`Float`**: Memory optimization, sufficient precision
- **`Double`**: High precision, default for decimal numbers

### **2. Text Types**

#### **Character (`Char`)**

```kotlin
val letter: Char = 'A'
val digit: Char = '5'
val symbol: Char = '$'
val unicode: Char = '\u0041'  // Unicode for 'A'
```

**Characteristics:**
- Single Unicode character
- 16-bit Unicode value
- Single quotes required
- Can represent any Unicode character

#### **String**

```kotlin
val name: String = "John Doe"
val empty: String = ""
val multiline: String = """
    This is a
    multi-line string
"""
```

**Characteristics:**
- Sequence of characters
- Immutable (cannot be changed)
- Double quotes required
- Rich set of methods and properties

### **3. Boolean Type**

```kotlin
val isActive: Boolean = true
val isComplete: Boolean = false
val isValid: Boolean = (age >= 18)
```

**Use cases:**
- Conditional statements
- Flags and status indicators
- Logical operations
- Control flow decisions

## 🧪 Hands-On Exercises

### **Exercise 1: Type Declaration Practice**
Create variables of different types and observe type inference:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    // Explicit type declarations
    val age: Int = 25
    val height: Double = 1.75
    val isStudent: Boolean = true
    val grade: Char = 'A'
    val name: String = "Alice"
    
    // Type inference examples
    val temperature = 23.5        // Double (default for decimals)
    val year = 2024               // Int
    val message = "Hello"         // String
    val flag = false              // Boolean
    
    // Print types to verify
    println("Age type: ${age::class.simpleName}")
    println("Height type: ${height::class.simpleName}")
    println("Temperature type: ${temperature::class.simpleName}")
}
```

### **Exercise 2: Number Type Limits**
Explore the limits of different number types:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    // Byte limits
    val maxByte: Byte = Byte.MAX_VALUE
    val minByte: Byte = Byte.MIN_VALUE
    println("Byte range: $minByte to $maxByte")
    
    // Int limits
    val maxInt: Int = Int.MAX_VALUE
    val minInt: Int = Int.MIN_VALUE
    println("Int range: $minInt to $maxInt")
    
    // Long limits
    val maxLong: Long = Long.MAX_VALUE
    val minLong: Long = Long.MIN_VALUE
    println("Long range: $minLong to $maxLong")
    
    // Float vs Double precision
    val floatValue: Float = 3.14159265359f
    val doubleValue: Double = 3.14159265359
    println("Float: $floatValue")
    println("Double: $doubleValue")
}
```

### **Exercise 3: Type Conversion**
Practice converting between different types:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val intValue = 42
    val doubleValue = 3.14
    
    // Int to other types
    val longFromInt: Long = intValue.toLong()
    val floatFromInt: Float = intValue.toFloat()
    val doubleFromInt: Double = intValue.toDouble()
    
    // Double to other types
    val intFromDouble: Int = doubleValue.toInt()  // Truncates decimal part
    val floatFromDouble: Float = doubleValue.toFloat()
    val longFromDouble: Long = doubleValue.toLong()
    
    // String conversions
    val stringFromInt = intValue.toString()
    val intFromString = "123".toInt()
    
    println("Original int: $intValue")
    println("As long: $longFromInt")
    println("As float: $floatFromInt")
    println("As double: $doubleFromInt")
    println("As string: $stringFromInt")
}
```

### **Exercise 4: Practical Data Types**
Create a student information system using appropriate data types:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    // Student information with appropriate types
    val studentId: Long = 2024001L          // Long for large ID numbers
    val firstName: String = "John"
    val lastName: String = "Doe"
    val age: Int = 20                       // Int for age
    val height: Double = 1.75               // Double for precise height
    val weight: Float = 70.5f               // Float for weight
    val grade: Char = 'A'                   // Char for single grade
    val isEnrolled: Boolean = true          // Boolean for enrollment status
    val gpa: Double = 3.85                  // Double for precise GPA
    
    // Display student information
    println("Student ID: $studentId")
    println("Name: $firstName $lastName")
    println("Age: $age years")
    println("Height: ${height}m")
    println("Weight: ${weight}kg")
    println("Grade: $grade")
    println("Enrolled: $isEnrolled")
    println("GPA: $gpa")
    
    // Calculate age in months
    val ageInMonths: Int = age * 12
    println("Age in months: $ageInMonths")
}
```

## 🔍 Type Conversion and Casting

### **Implicit Conversion (Automatic)**

Kotlin automatically converts smaller types to larger types:

```kotlin
val intValue: Int = 42
val longValue: Long = intValue  // Automatic conversion Int → Long
val doubleValue: Double = intValue  // Automatic conversion Int → Double
```

### **Explicit Conversion (Manual)**

Use conversion functions for potentially lossy conversions:

```kotlin
val doubleValue: Double = 3.14
val intValue: Int = doubleValue.toInt()  // Truncates to 3
val longValue: Long = doubleValue.toLong()  // Truncates to 3
```

### **Safe Conversion Functions**

```kotlin
val stringNumber = "123"
val intNumber = stringNumber.toIntOrNull()  // Returns null if conversion fails
val longNumber = stringNumber.toLongOrNull()
val doubleNumber = stringNumber.toDoubleOrNull()
```

## 🚨 Common Mistakes to Avoid

1. **Type mismatch errors**:
   ```kotlin
   val age: Int = "25"  // ❌ Type mismatch
   val age: Int = 25    // ✅ Correct
   ```

2. **Forgetting suffixes for specific types**:
   ```kotlin
   val floatValue: Float = 3.14   // ❌ 3.14 is Double by default
   val floatValue: Float = 3.14f  // ✅ Correct
   ```

3. **Using wrong number types**:
   ```kotlin
   val largeNumber: Int = 3000000000  // ❌ Too large for Int
   val largeNumber: Long = 3000000000L // ✅ Correct
   ```

4. **Character vs String confusion**:
   ```kotlin
   val letter: Char = "A"    // ❌ Double quotes for String
   val letter: Char = 'A'    // ✅ Single quotes for Char
   ```

## 🎯 What's Next?

Excellent! You've mastered data types in Kotlin. Now you're ready to:

1. **Learn string operations** → [String Interpolation](05-string-interpolation.md)
2. **Understand control flow** → [If Expressions](../control-flow/01-if-expressions.md)
3. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
4. **Explore collections** → [Arrays](../collections/01-arrays.md)

## 📚 Additional Resources

- [Kotlin Basic Types](https://kotlinlang.org/docs/basic-types.html)
- [Number Types](https://kotlinlang.org/docs/numbers.html)
- [Strings](https://kotlinlang.org/docs/strings.html)
- [Type Conversion](https://kotlinlang.org/docs/numbers.html#explicit-conversions)

## 🏆 Summary

- ✅ You understand all basic data types in Kotlin
- ✅ You can choose the right data type for your needs
- ✅ You know how to work with numbers, text, and logical values
- ✅ You understand type conversion and casting
- ✅ You can use data types efficiently in your programs!

**Keep practicing and happy coding! 🎉**
