# 🔁 While Loops in Kotlin

Welcome to the world of while loops! While loops are perfect for situations where you don't know in advance how many times you need to repeat a block of code. They continue executing as long as a condition remains true, making them ideal for user input validation, data processing, and game loops.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write basic while loops
- ✅ Use do-while loops effectively
- ✅ Understand when to use while vs for loops
- ✅ Control loop execution with break and continue
- ✅ Avoid infinite loops and common pitfalls

## 🔍 What You'll Learn

- **Basic while loops** - Simple conditional repetition
- **Do-while loops** - Execute first, then check condition
- **Loop control** - Using break and continue statements
- **Infinite loop prevention** - Best practices and safety
- **Real-world applications** - Practical use cases

## 📝 Prerequisites

- Basic understanding of for loops
- Completed [For Loops](03-for-loops.md) lesson

## 💻 The Code

Let's examine the while loop example:

```kotlin
fun main(args: Array<String>) {
    var i = 1
    
    while (i <= 5) {
        println("Count: $i")
        i++
    }
    
    println("Loop finished!")
}
```

**📁 File:** [13_while_loop.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/13_while_loop.kt)

## 🔍 Code Breakdown

### **Variable Initialization**

```kotlin
var i = 1
```

- **`var i = 1`**: Initialize loop counter
- **`var`** makes it mutable (can be changed)

### **While Loop**

```kotlin
while (i <= 5) {
    println("Count: $i")
    i++
}
```

- **`while (i <= 5)`**: Condition to check before each iteration
- **`{ }`**: Loop body containing statements
- **`println("Count: $i")`**: Print current count
- **`i++`**: Increment counter (crucial to avoid infinite loop)

## 🎯 Key Concepts Explained

### **1. While Loop Syntax**

```kotlin
while (condition) {
    // Code to execute while condition is true
}
```

**Components:**
- **`while`**: Loop keyword
- **`(condition)`**: Boolean expression that controls the loop
- **`{ }`**: Loop body containing statements

**Execution Flow:**
1. **Check condition** - Is it true?
2. **If true** - Execute loop body
3. **Repeat** - Go back to step 1
4. **If false** - Exit loop

### **2. Do-While Loop Syntax**

```kotlin
do {
    // Code to execute at least once
} while (condition)
```

**Key Difference:**
- **While loop**: Check condition first, then execute
- **Do-while loop**: Execute first, then check condition
- **Guarantee**: Do-while always executes at least once

### **3. When to Use Each Loop Type**

#### **Use While Loop When:**
- You don't know the number of iterations in advance
- Condition depends on user input
- Processing data until a condition is met
- Game loops or event-driven programming

#### **Use For Loop When:**
- You know the exact number of iterations
- Iterating over collections or ranges
- Simple counting scenarios

#### **Use Do-While Loop When:**
- You need to execute code at least once
- Menu-driven programs
- Input validation scenarios

## 🧪 Hands-On Exercises

### **Exercise 1: Basic While Loop**
Create a program that counts down from 10 to 1:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    var count = 10
    
    while (count >= 1) {
        println("Countdown: $count")
        count--
    }
    
    println("Blast off!")
}
```

### **Exercise 2: User Input Validation**
Create a program that asks for a positive number using while loop:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    var input: Int
    var attempts = 0
    
    do {
        print("Enter a positive number: ")
        input = readLine()?.toIntOrNull() ?: 0
        attempts++
        
        if (input <= 0) {
            println("Invalid input. Please try again.")
        }
    } while (input <= 0)
    
    println("Valid input received: $input")
    println("Number of attempts: $attempts")
}
```

### **Exercise 3: Data Processing Loop**
Create a program that processes numbers until a sentinel value is encountered:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    var sum = 0
    var count = 0
    var number: Int
    
    println("Enter numbers (enter -1 to stop):")
    
    while (true) {
        print("Enter number: ")
        number = readLine()?.toIntOrNull() ?: 0
        
        if (number == -1) {
            break  // Exit loop when sentinel value is entered
        }
        
        sum += number
        count++
    }
    
    if (count > 0) {
        val average = sum.toDouble() / count
        println("Sum: $sum")
        println("Count: $count")
        println("Average: $average")
    } else {
        println("No numbers entered.")
    }
}
```

### **Exercise 4: Menu-Driven Program**
Create a simple calculator using do-while loop:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    var choice: Int
    var continueProgram = true
    
    do {
        println("\n=== Simple Calculator ===")
        println("1. Addition")
        println("2. Subtraction")
        println("3. Multiplication")
        println("4. Division")
        println("5. Exit")
        print("Enter your choice (1-5): ")
        
        choice = readLine()?.toIntOrNull() ?: 0
        
        when (choice) {
            1 -> {
                print("Enter first number: ")
                val a = readLine()?.toDoubleOrNull() ?: 0.0
                print("Enter second number: ")
                val b = readLine()?.toDoubleOrNull() ?: 0.0
                println("Result: ${a + b}")
            }
            2 -> {
                print("Enter first number: ")
                val a = readLine()?.toDoubleOrNull() ?: 0.0
                print("Enter second number: ")
                val b = readLine()?.toDoubleOrNull() ?: 0.0
                println("Result: ${a - b}")
            }
            3 -> {
                print("Enter first number: ")
                val a = readLine()?.toDoubleOrNull() ?: 0.0
                print("Enter second number: ")
                val b = readLine()?.toDoubleOrNull() ?: 0.0
                println("Result: ${a * b}")
            }
            4 -> {
                print("Enter first number: ")
                val a = readLine()?.toDoubleOrNull() ?: 0.0
                print("Enter second number: ")
                val b = readLine()?.toDoubleOrNull() ?: 0.0
                if (b != 0.0) {
                    println("Result: ${a / b}")
                } else {
                    println("Error: Division by zero!")
                }
            }
            5 -> {
                println("Goodbye!")
                continueProgram = false
            }
            else -> println("Invalid choice. Please try again.")
        }
    } while (continueProgram)
}
```

## 🔍 Advanced While Loop Concepts

### **1. Nested While Loops**

```kotlin
var i = 1
while (i <= 3) {
    var j = 1
    while (j <= i) {
        print("*")
        j++
    }
    println()
    i++
}
// Output:
// *
// **
// ***
```

### **2. While Loop with Collections**

```kotlin
val numbers = mutableListOf(1, 2, 3, 4, 5)
var index = 0

while (index < numbers.size) {
    if (numbers[index] % 2 == 0) {
        numbers[index] *= 2  // Double even numbers
    }
    index++
}

println(numbers)  // [1, 4, 3, 8, 5]
```

### **3. While Loop with Custom Conditions**

```kotlin
var password = ""
var attempts = 0
val correctPassword = "secret123"

while (password != correctPassword && attempts < 3) {
    print("Enter password (attempt ${attempts + 1}/3): ")
    password = readLine() ?: ""
    attempts++
    
    if (password != correctPassword) {
        println("Incorrect password. Try again.")
    }
}

if (password == correctPassword) {
    println("Access granted!")
} else {
    println("Access denied. Too many attempts.")
}
```

## 🔍 Loop Control in While Loops

### **1. Break Statement**

```kotlin
var i = 1
while (true) {
    if (i > 10) {
        break  // Exit loop when i exceeds 10
    }
    println(i)
    i++
}
```

### **2. Continue Statement**

```kotlin
var i = 1
while (i <= 10) {
    if (i % 2 == 0) {
        i++
        continue  // Skip even numbers
    }
    println("Odd number: $i")
    i++
}
```

### **3. Labeled Loops**

```kotlin
outer@ while (true) {
    var i = 1
    while (i <= 5) {
        if (i == 3) {
            break@outer  // Break outer loop
        }
        println("i = $i")
        i++
    }
}
```

## 🚨 Common Mistakes to Avoid

### **1. Infinite Loops**

```kotlin
// ❌ Infinite loop - missing increment
var i = 1
while (i <= 5) {
    println(i)
    // i++ is missing!
}

// ✅ Correct - with increment
var i = 1
while (i <= 5) {
    println(i)
    i++
}
```

### **2. Off-by-One Errors**

```kotlin
// ❌ Wrong condition - will miss last element
var i = 0
while (i < array.size - 1) {
    println(array[i])
    i++
}

// ✅ Correct condition
var i = 0
while (i < array.size) {
    println(array[i])
    i++
}
```

### **3. Using Wrong Loop Type**

```kotlin
// ❌ While loop for simple counting
var i = 1
while (i <= 10) {
    println(i)
    i++
}

// ✅ For loop is better for counting
for (i in 1..10) {
    println(i)
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Always ensure loop termination**:
   ```kotlin
   var i = 1
   while (i <= 10) {  // ✅ Clear termination condition
       println(i)
       i++
   }
   ```

2. **Use meaningful variable names**:
   ```kotlin
   var count = 0
   while (count < maxAttempts) {  // ✅ Clear and descriptive
       // Loop body
       count++
   }
   ```

3. **Initialize variables before the loop**:
   ```kotlin
   var sum = 0  // ✅ Initialize before loop
   var i = 1
   while (i <= 10) {
       sum += i
       i++
   }
   ```

### **❌ Don'ts**

1. **Don't forget to update loop variables**:
   ```kotlin
   var i = 1
   while (i <= 5) {
       println(i)
       // ❌ Missing i++ - infinite loop!
   }
   ```

2. **Don't use while loops for simple counting**:
   ```kotlin
   // ❌ Overkill for simple iteration
   var i = 0
   while (i < 10) {
       println(i)
       i++
   }
   
   // ✅ Use for loop instead
   for (i in 0 until 10) {
       println(i)
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered while loops in Kotlin. Now you're ready to:

1. **Learn break and continue** → [Break and Continue](05-break-continue.md)
2. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
3. **Explore collections** → [Arrays](../collections/01-arrays.md)
4. **Understand OOP** → [Classes and Constructors](../oop/01-classes-constructors.md)

## 📚 Additional Resources

- [Kotlin While Loops](https://kotlinlang.org/docs/control-flow.html#while-loops)
- [Control Flow](https://kotlinlang.org/docs/control-flow.html)
- [Loop Control](https://kotlinlang.org/docs/returns.html)

## 🏆 Summary

- ✅ You can write basic while loops
- ✅ You can use do-while loops effectively
- ✅ You understand when to use while vs for loops
- ✅ You can control loop execution with break and continue
- ✅ You know how to avoid infinite loops and common pitfalls
- ✅ You're ready to handle dynamic repetition scenarios!

**Keep practicing and happy coding! 🎉**

