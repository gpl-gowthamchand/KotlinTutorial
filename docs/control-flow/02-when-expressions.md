# 🎲 When Expressions in Kotlin

Welcome to the powerful world of when expressions! When expressions are Kotlin's replacement for switch statements and provide a much more flexible and expressive way to handle multiple conditions. They're perfect for replacing long if-else chains with clean, readable code.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write basic when expressions
- ✅ Use when expressions to return values
- ✅ Handle multiple conditions elegantly
- ✅ Use when expressions with different data types
- ✅ Understand when expressions vs if-else chains

## 🔍 What You'll Learn

- **Basic when expressions** - Simple multiple condition handling
- **When expressions as values** - Using when to return results
- **Multiple conditions** - Handling various cases elegantly
- **Type matching** - Using when with different data types
- **Best practices** - When and how to use when expressions

## 📝 Prerequisites

- Basic understanding of if expressions
- Completed [If Expressions](01-if-expressions.md) lesson

## 💻 The Code

Let's examine the when expression example:

```kotlin
fun main(args: Array<String>) {
    val x = 100

    val str: String = when (x) {
        1 -> "x is 1"
        2 -> "x is 2"
        else -> {
            "x value is unknown"
            "x is an alien"
        }
    }

    println(str)
}
```

**📁 File:** [11_when_expression.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/11_when_expression.kt)

## 🔍 Code Breakdown

### **Variable Declaration**

```kotlin
val x = 100
```

- **Single variable** to test against multiple values
- **`val`** makes it immutable

### **When Expression**

```kotlin
val str: String = when (x) {
    1 -> "x is 1"
    2 -> "x is 2"
    else -> {
        "x value is unknown"
        "x is an alien"
    }
}
```

- **`when (x)`**: Tests the value of `x` against different cases
- **`1 -> "x is 1"`**: If `x` equals 1, return "x is 1"
- **`2 -> "x is 2"`**: If `x` equals 2, return "x is 2"
- **`else -> { }`**: Default case when no other conditions match
- **`str`**: Variable that stores the result

## 🎯 Key Concepts Explained

### **1. When Expression Syntax**

```kotlin
val result = when (expression) {
    value1 -> result1
    value2 -> result2
    value3 -> result3
    else -> defaultResult
}
```

**Components:**
- **`when (expression)`**: The value to test
- **`value -> result`**: Each case with its corresponding result
- **`else ->`**: Default case (optional but recommended)

### **2. When vs If-Else Chains**

#### **If-Else Chain (Verbose)**

```kotlin
val grade = if (score >= 90) {
    'A'
} else if (score >= 80) {
    'B'
} else if (score >= 70) {
    'C'
} else if (score >= 60) {
    'D'
} else {
    'F'
}
```

#### **When Expression (Clean)**

```kotlin
val grade = when {
    score >= 90 -> 'A'
    score >= 80 -> 'B'
    score >= 70 -> 'C'
    score >= 60 -> 'D'
    else -> 'F'
}
```

**Advantages of when:**
- ✅ More readable
- ✅ Less repetitive
- ✅ Better performance
- ✅ Easier to maintain

### **3. Different Types of When Expressions**

#### **Value-Based When**

```kotlin
val day = 3
val dayName = when (day) {
    1 -> "Monday"
    2 -> "Tuesday"
    3 -> "Wednesday"
    4 -> "Thursday"
    5 -> "Friday"
    6 -> "Saturday"
    7 -> "Sunday"
    else -> "Invalid day"
}
```

#### **Expression-Based When**

```kotlin
val score = 85
val grade = when {
    score >= 90 -> 'A'
    score >= 80 -> 'B'
    score >= 70 -> 'C'
    score >= 60 -> 'D'
    else -> 'F'
}
```

#### **Range-Based When**

```kotlin
val age = 25
val category = when (age) {
    in 0..12 -> "Child"
    in 13..19 -> "Teenager"
    in 20..64 -> "Adult"
    else -> "Senior"
}
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic When Expression**
Create a program that converts numbers to day names:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val dayNumber = 3
    
    val dayName = when (dayNumber) {
        1 -> "Monday"
        2 -> "Tuesday"
        3 -> "Wednesday"
        4 -> "Thursday"
        5 -> "Friday"
        6 -> "Saturday"
        7 -> "Sunday"
        else -> "Invalid day number"
    }
    
    println("Day $dayNumber is $dayName")
}
```

### **Exercise 2: When Expression with Ranges**
Create a program that categorizes ages using ranges:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val age = 17
    
    val category = when (age) {
        in 0..2 -> "Infant"
        in 3..5 -> "Toddler"
        in 6..12 -> "Child"
        in 13..19 -> "Teenager"
        in 20..39 -> "Young Adult"
        in 40..59 -> "Middle Aged"
        in 60..79 -> "Senior"
        else -> "Elderly"
    }
    
    println("Age $age belongs to category: $category")
}
```

### **Exercise 3: Complex When Expression**
Create a program that determines shipping cost based on weight and destination:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val weight = 2.5  // in kg
    val destination = "International"
    
    val shippingCost = when {
        weight <= 1.0 -> {
            when (destination) {
                "Local" -> 5.0
                "National" -> 8.0
                "International" -> 15.0
                else -> 0.0
            }
        }
        weight <= 5.0 -> {
            when (destination) {
                "Local" -> 10.0
                "National" -> 15.0
                "International" -> 25.0
                else -> 0.0
            }
        }
        weight <= 10.0 -> {
            when (destination) {
                "Local" -> 15.0
                "National" -> 25.0
                "International" -> 40.0
                else -> 0.0
            }
        }
        else -> {
            when (destination) {
                "Local" -> 20.0
                "National" -> 35.0
                "International" -> 60.0
                else -> 0.0
            }
        }
    }
    
    println("Weight: ${weight}kg")
    println("Destination: $destination")
    println("Shipping Cost: $${shippingCost}")
}
```

### **Exercise 4: When Expression with Multiple Values**
Create a program that handles multiple conditions elegantly:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val temperature = 25
    val humidity = 70
    val isRaining = false
    
    val activity = when {
        temperature > 30 && humidity > 80 -> "Stay indoors with AC"
        temperature > 25 && !isRaining -> "Go for a walk"
        temperature in 15..25 && !isRaining -> "Perfect for outdoor activities"
        temperature < 15 -> "Bundle up and stay warm"
        isRaining -> "Indoor activities recommended"
        else -> "Moderate outdoor activities"
    }
    
    println("Temperature: ${temperature}°C")
    println("Humidity: ${humidity}%")
    println("Raining: $isRaining")
    println("Recommended activity: $activity")
}
```

## 🔍 Advanced When Expression Features

### **1. Multiple Values in One Case**

```kotlin
val day = 3
val dayType = when (day) {
    1, 2, 3, 4, 5 -> "Weekday"
    6, 7 -> "Weekend"
    else -> "Invalid day"
}
```

### **2. Using When with Custom Objects**

```kotlin
sealed class Shape
data class Circle(val radius: Double) : Shape()
data class Rectangle(val width: Double, val height: Double) : Shape()
data class Triangle(val base: Double, val height: Double) : Shape()

fun calculateArea(shape: Shape): Double = when (shape) {
    is Circle -> Math.PI * shape.radius * shape.radius
    is Rectangle -> shape.width * shape.height
    is Triangle -> 0.5 * shape.base * shape.height
}
```

### **3. When Expression as Statement**

```kotlin
val score = 85
when {
    score >= 90 -> println("Excellent!")
    score >= 80 -> println("Good job!")
    score >= 70 -> println("Not bad!")
    else -> println("Keep trying!")
}
```

## 🔍 When Expression Best Practices

### **✅ Do's**

1. **Always include an else branch** (unless exhaustive):
   ```kotlin
   val result = when (value) {
       1 -> "One"
       2 -> "Two"
       else -> "Unknown"  // ✅ Safe fallback
   }
   ```

2. **Use ranges for numeric comparisons**:
   ```kotlin
   val category = when (age) {
       in 0..12 -> "Child"      // ✅ Clean and readable
       in 13..19 -> "Teenager"
       else -> "Adult"
   }
   ```

3. **Group related cases together**:
   ```kotlin
   val season = when (month) {
       12, 1, 2 -> "Winter"     // ✅ Logical grouping
       3, 4, 5 -> "Spring"
       6, 7, 8 -> "Summer"
       9, 10, 11 -> "Fall"
       else -> "Invalid month"
   }
   ```

### **❌ Don'ts**

1. **Don't forget the else branch**:
   ```kotlin
   val result = when (value) {
       1 -> "One"
       2 -> "Two"
       // ❌ Missing else branch
   }
   ```

2. **Don't use when for simple if-else**:
   ```kotlin
   // ❌ Overkill for simple condition
   val result = when (a > b) {
       true -> a
       false -> b
   }
   
   // ✅ Better approach
   val result = if (a > b) a else b
   ```

## 🚨 Common Mistakes to Avoid

1. **Missing else branch**:
   ```kotlin
   val result = when (x) {
       1 -> "One"
       2 -> "Two"
       // ❌ Compile error: missing else branch
   }
   ```

2. **Using wrong syntax**:
   ```kotlin
   when (x) {
       1: "One"    // ❌ Wrong syntax
       1 -> "One"  // ✅ Correct syntax
   }
   ```

3. **Forgetting to handle all cases**:
   ```kotlin
   val result = when (x) {
       1 -> "One"
       2 -> "Two"
       // ❌ What if x is 3?
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered when expressions in Kotlin. Now you're ready to:

1. **Learn loops** → [For Loops](03-for-loops.md)
2. **Understand while loops** → [While Loops](04-while-loops.md)
3. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
4. **Explore collections** → [Arrays](../collections/01-arrays.md)

## 📚 Additional Resources

- [Kotlin When Expression](https://kotlinlang.org/docs/control-flow.html#when-expression)
- [Control Flow](https://kotlinlang.org/docs/control-flow.html)
- [Sealed Classes](https://kotlinlang.org/docs/sealed-classes.html)

## 🏆 Summary

- ✅ You can write basic when expressions
- ✅ You can use when expressions to return values
- ✅ You can handle multiple conditions elegantly
- ✅ You can use when expressions with different data types
- ✅ You understand when expressions vs if-else chains
- ✅ You're ready to write clean, readable conditional code!

**Keep practicing and happy coding! 🎉**
