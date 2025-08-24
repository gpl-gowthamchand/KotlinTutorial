# 🔄 For Loops in Kotlin

Welcome to the world of loops! For loops are essential for repeating code and iterating over collections. They're one of the most powerful tools for automating repetitive tasks and processing data efficiently.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write basic for loops with ranges
- ✅ Iterate over collections and arrays
- ✅ Use different loop directions (forward, backward, step)
- ✅ Understand loop control with break and continue
- ✅ Create efficient and readable loops

## 🔍 What You'll Learn

- **Basic for loops** - Simple iteration with ranges
- **Range-based loops** - Using `..`, `downTo`, and `step`
- **Collection iteration** - Looping through lists, arrays, and maps
- **Loop control** - Using break and continue statements
- **Best practices** - Writing efficient and readable loops

## 📝 Prerequisites

- Basic understanding of control flow
- Completed [When Expressions](02-when-expressions.md) lesson

## 💻 The Code

Let's examine the for loop example:

```kotlin
fun main(args: Array<String>) {
    for (i in 1..10) {
        if (i % 2 == 0) {
            println(i)
        }
    }

    println()

    for (i in 10 downTo 0) {
        if (i % 2 == 0) {
            println(i)
        }
    }
}
```

**📁 File:** [12_for_loop.kt](src/12_for_loop.kt)

## 🔍 Code Breakdown

### **First For Loop**

```kotlin
for (i in 1..10) {
    if (i % 2 == 0) {
        println(i)
    }
}
```

- **`for (i in 1..10)`**: Loop from 1 to 10 (inclusive)
- **`i`**: Loop variable that takes each value
- **`1..10`**: Range from 1 to 10
- **`if (i % 2 == 0)`**: Check if number is even
- **`println(i)`**: Print even numbers only

### **Second For Loop**

```kotlin
for (i in 10 downTo 0) {
    if (i % 2 == 0) {
        println(i)
    }
}
```

- **`for (i in 10 downTo 0)`**: Loop from 10 down to 0
- **`downTo`**: Reverse direction
- **Same logic**: Print even numbers in descending order

## 🎯 Key Concepts Explained

### **1. Basic For Loop Syntax**

```kotlin
for (variable in range) {
    // Code to execute for each iteration
}
```

**Components:**
- **`for`**: Loop keyword
- **`variable`**: Loop variable (can be any name)
- **`in`**: Membership operator
- **`range`**: What to iterate over
- **`{ }`**: Loop body

### **2. Range Types**

#### **Inclusive Range (`..`)**

```kotlin
for (i in 1..5) {
    println(i)  // Prints: 1, 2, 3, 4, 5
}
```

- **`1..5`**: Includes both 1 and 5
- **Forward direction**: 1 → 2 → 3 → 4 → 5

#### **Exclusive Range (`until`)**

```kotlin
for (i in 1 until 5) {
    println(i)  // Prints: 1, 2, 3, 4 (excludes 5)
}
```

- **`1 until 5`**: Excludes the upper bound
- **Useful for**: Array indices, avoiding off-by-one errors

#### **Reverse Range (`downTo`)**

```kotlin
for (i in 5 downTo 1) {
    println(i)  // Prints: 5, 4, 3, 2, 1
}
```

- **`5 downTo 1`**: Counts backward
- **Useful for**: Reverse iteration, countdowns

#### **Step Range**

```kotlin
for (i in 0..10 step 2) {
    println(i)  // Prints: 0, 2, 4, 6, 8, 10
}

for (i in 10 downTo 0 step 3) {
    println(i)  // Prints: 10, 7, 4, 1
}
```

- **`step 2`**: Skip every other number
- **`step 3`**: Skip by 3s

### **3. Collection Iteration**

#### **Array/List Iteration**

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)

// By index
for (i in numbers.indices) {
    println("Index $i: ${numbers[i]}")
}

// By value
for (number in numbers) {
    println("Number: $number")
}

// By index and value
for ((index, value) in numbers.withIndex()) {
    println("Index $index: $value")
}
```

#### **String Iteration**

```kotlin
val text = "Hello"

// By character
for (char in text) {
    println("Character: $char")
}

// By index
for (i in text.indices) {
    println("Index $i: ${text[i]}")
}
```

#### **Map Iteration**

```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)

// By key-value pairs
for ((key, value) in map) {
    println("$key -> $value")
}

// By keys only
for (key in map.keys) {
    println("Key: $key")
}

// By values only
for (value in map.values) {
    println("Value: $value")
}
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Range Loops**
Create a program that demonstrates different range types:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    println("Forward range (1..5):")
    for (i in 1..5) {
        print("$i ")
    }
    
    println("\n\nExclusive range (1 until 5):")
    for (i in 1 until 5) {
        print("$i ")
    }
    
    println("\n\nReverse range (5 downTo 1):")
    for (i in 5 downTo 1) {
        print("$i ")
    }
    
    println("\n\nStep range (0..10 step 2):")
    for (i in 0..10 step 2) {
        print("$i ")
    }
}
```

### **Exercise 2: Number Pattern Loops**
Create a program that prints different number patterns:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    println("Multiplication table for 5:")
    for (i in 1..10) {
        println("5 × $i = ${5 * i}")
    }
    
    println("\nEven numbers from 2 to 20:")
    for (i in 2..20 step 2) {
        print("$i ")
    }
    
    println("\n\nCountdown from 10:")
    for (i in 10 downTo 1) {
        print("$i ")
        if (i == 1) println("Blast off!") else print(", ")
    }
}
```

### **Exercise 3: Collection Iteration**
Create a program that demonstrates different ways to iterate over collections:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val fruits = listOf("Apple", "Banana", "Orange", "Grape", "Mango")
    
    println("Fruits by index:")
    for (i in fruits.indices) {
        println("${i + 1}. ${fruits[i]}")
    }
    
    println("\nFruits by value:")
    for (fruit in fruits) {
        println("• $fruit")
    }
    
    println("\nFruits with index:")
    for ((index, fruit) in fruits.withIndex()) {
        println("${index + 1}. $fruit")
    }
    
    println("\nFruits in reverse:")
    for (i in fruits.indices.reversed()) {
        println("${i + 1}. ${fruits[i]}")
    }
}
```

### **Exercise 4: Advanced Loop Patterns**
Create a program that demonstrates complex loop patterns:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    println("Pyramid pattern:")
    for (i in 1..5) {
        // Print spaces
        for (j in 1..(5 - i)) {
            print(" ")
        }
        // Print stars
        for (j in 1..(2 * i - 1)) {
            print("*")
        }
        println()
    }
    
    println("\nNumber triangle:")
    for (i in 1..5) {
        for (j in 1..i) {
            print("$j ")
        }
        println()
    }
    
    println("\nAlternating pattern:")
    for (i in 1..10) {
        val symbol = if (i % 2 == 0) "★" else "☆"
        print("$symbol ")
    }
}
```

## 🔍 Advanced For Loop Features

### **1. Nested Loops**

```kotlin
// Multiplication table
for (i in 1..5) {
    for (j in 1..5) {
        print("${i * j}\t")
    }
    println()
}
```

### **2. Loop with Conditions**

```kotlin
for (i in 1..20) {
    when {
        i % 3 == 0 && i % 5 == 0 -> println("FizzBuzz")
        i % 3 == 0 -> println("Fizz")
        i % 5 == 0 -> println("Buzz")
        else -> println(i)
    }
}
```

### **3. Custom Range Functions**

```kotlin
// Custom step function
fun Int.toward(to: Int): IntProgression {
    val step = if (this > to) -1 else 1
    return IntProgression.fromClosedRange(this, to, step)
}

// Usage
for (i in 5.toward(1)) {
    println(i)  // Prints: 5, 4, 3, 2, 1
}
```

## 🔍 Loop Control Statements

### **1. Break Statement**

```kotlin
for (i in 1..10) {
    if (i == 5) {
        break  // Exit loop when i equals 5
    }
    println(i)
}
// Output: 1, 2, 3, 4
```

### **2. Continue Statement**

```kotlin
for (i in 1..10) {
    if (i % 2 == 0) {
        continue  // Skip even numbers
    }
    println(i)
}
// Output: 1, 3, 5, 7, 9
```

### **3. Labeled Loops**

```kotlin
outer@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2 && j == 2) {
            break@outer  // Break outer loop
        }
        println("i=$i, j=$j")
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Off-by-one errors**:
   ```kotlin
   val array = arrayOf(1, 2, 3, 4, 5)
   for (i in 0..array.size) {  // ❌ Should be array.size - 1
       println(array[i])
   }
   
   for (i in 0 until array.size) {  // ✅ Correct
       println(array[i])
   }
   ```

2. **Infinite loops**:
   ```kotlin
   for (i in 1..10) {
       i++  // ❌ Cannot modify loop variable
   }
   ```

3. **Wrong range direction**:
   ```kotlin
   for (i in 10..1) {  // ❌ Empty range (10 is not <= 1)
       println(i)
   }
   
   for (i in 10 downTo 1) {  // ✅ Correct
       println(i)
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered for loops in Kotlin. Now you're ready to:

1. **Learn while loops** → [While Loops](04-while-loops.md)
2. **Understand break and continue** → [Break and Continue](05-break-continue.md)
3. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
4. **Explore collections** → [Arrays](../collections/01-arrays.md)

## 📚 Additional Resources

- [Kotlin For Loops](https://kotlinlang.org/docs/control-flow.html#for-loops)
- [Ranges](https://kotlinlang.org/docs/ranges.html)
- [Collections](https://kotlinlang.org/docs/collections-overview.html)

## 🏆 Summary

- ✅ You can write basic for loops with ranges
- ✅ You can iterate over collections and arrays
- ✅ You can use different loop directions (forward, backward, step)
- ✅ You understand loop control with break and continue
- ✅ You can create efficient and readable loops
- ✅ You're ready to automate repetitive tasks!

**Keep practicing and happy coding! 🎉**
