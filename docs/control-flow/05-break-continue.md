# ⏹️ Break and Continue in Kotlin

Welcome to the world of loop control! Break and continue statements give you fine-grained control over how your loops execute. They allow you to skip iterations, exit loops early, and create more efficient and readable code.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Use break statements to exit loops early
- ✅ Use continue statements to skip iterations
- ✅ Understand labeled break and continue
- ✅ Choose the right control statement for your needs
- ✅ Write more efficient and readable loops

## 🔍 What You'll Learn

- **Break statements** - Exiting loops prematurely
- **Continue statements** - Skipping specific iterations
- **Labeled statements** - Controlling nested loops
- **Best practices** - When and how to use each statement
- **Real-world applications** - Practical use cases

## 📝 Prerequisites

- Basic understanding of loops (for, while)
- Completed [While Loops](04-while-loops.md) lesson

## 💻 The Code

Let's examine the break and continue examples:

```kotlin
fun main(args: Array<String>) {
    for (i in 1..10) {
        if (i == 5) {
            break  // Exit loop when i equals 5
        }
        println(i)
    }
    
    println("Loop finished!")
}
```

**📁 File:** [15_break_keyword.kt](src/15_break_keyword.kt)

## 🔍 Code Breakdown

### **Break Statement Example**

```kotlin
for (i in 1..10) {
    if (i == 5) {
        break  // Exit loop when i equals 5
    }
    println(i)
}
```

- **`for (i in 1..10)`**: Loop from 1 to 10
- **`if (i == 5)`**: Condition to check
- **`break`**: Exit the loop immediately
- **Output**: Only prints 1, 2, 3, 4 (loop exits at 5)

## 🎯 Key Concepts Explained

### **1. Break Statement**

#### **Basic Break Syntax**

```kotlin
for (i in 1..10) {
    if (condition) {
        break  // Exit the loop immediately
    }
    // This code won't execute after break
}
```

**What Break Does:**
- **Immediately exits** the innermost loop
- **Skips remaining iterations**
- **Continues execution** after the loop
- **Useful for**: Early termination, error conditions, found items

#### **Break in Different Loop Types**

```kotlin
// For loop
for (i in 1..10) {
    if (i == 5) break
    println(i)
}

// While loop
var i = 1
while (i <= 10) {
    if (i == 5) break
    println(i)
    i++
}

// Do-while loop
var j = 1
do {
    if (j == 5) break
    println(j)
    j++
} while (j <= 10)
```

### **2. Continue Statement**

#### **Basic Continue Syntax**

```kotlin
for (i in 1..10) {
    if (condition) {
        continue  // Skip to next iteration
    }
    // This code executes for non-skipped iterations
}
```

**What Continue Does:**
- **Skips current iteration**
- **Continues with next iteration**
- **Loop body continues** after continue
- **Useful for**: Skipping invalid data, filtering, conditional processing

#### **Continue Examples**

```kotlin
// Skip even numbers
for (i in 1..10) {
    if (i % 2 == 0) {
        continue  // Skip even numbers
    }
    println("Odd: $i")
}

// Skip specific values
for (i in 1..10) {
    if (i == 3 || i == 7) {
        continue  // Skip 3 and 7
    }
    println(i)
}
```

### **3. Labeled Break and Continue**

#### **Labeled Break**

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

**Output:**
```
i=1, j=1
i=1, j=2
i=1, j=3
i=2, j=1
```

#### **Labeled Continue**

```kotlin
outer@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2 && j == 2) {
            continue@outer  // Continue outer loop
        }
        println("i=$i, j=$j")
    }
}
```

**Output:**
```
i=1, j=1
i=1, j=2
i=1, j=3
i=2, j=1
i=3, j=1
i=3, j=2
i=3, j=3
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Break Statement**
Create a program that finds the first number divisible by both 3 and 5:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    for (i in 1..100) {
        if (i % 3 == 0 && i % 5 == 0) {
            println("First number divisible by both 3 and 5: $i")
            break  // Exit loop after finding first match
        }
    }
}
```

### **Exercise 2: Continue Statement**
Create a program that prints all numbers from 1 to 20, except multiples of 3:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    for (i in 1..20) {
        if (i % 3 == 0) {
            continue  // Skip multiples of 3
        }
        print("$i ")
    }
    println()
}
```

### **Exercise 3: Labeled Break**
Create a program that demonstrates labeled break with nested loops:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val targetSum = 15
    
    outer@ for (i in 1..5) {
        for (j in 1..5) {
            for (k in 1..5) {
                val sum = i + j + k
                if (sum == targetSum) {
                    println("Found combination: $i + $j + $k = $targetSum")
                    break@outer  // Exit all loops
                }
            }
        }
    }
}
```

### **Exercise 4: Complex Loop Control**
Create a program that processes a list of numbers with multiple control statements:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    var sum = 0
    var count = 0
    
    for (number in numbers) {
        // Skip negative numbers (though our list doesn't have any)
        if (number < 0) {
            continue
        }
        
        // Stop if we've processed 5 numbers
        if (count >= 5) {
            break
        }
        
        // Skip even numbers
        if (number % 2 == 0) {
            continue
        }
        
        sum += number
        count++
        println("Added $number, sum is now $sum")
    }
    
    println("Final sum: $sum")
    println("Numbers processed: $count")
}
```

## 🔍 Advanced Control Flow Patterns

### **1. Break with When Expression**

```kotlin
for (i in 1..10) {
    val action = when {
        i < 5 -> "Continue"
        i == 5 -> "Break"
        else -> "Process"
    }
    
    when (action) {
        "Continue" -> continue
        "Break" -> break
        "Process" -> println("Processing $i")
    }
}
```

### **2. Continue with Complex Conditions**

```kotlin
for (i in 1..20) {
    // Skip numbers that are multiples of 2, 3, or 5
    if (i % 2 == 0 || i % 3 == 0 || i % 5 == 0) {
        continue
    }
    
    // Only process prime numbers (simplified)
    if (i > 1) {
        println("Prime number: $i")
    }
}
```

### **3. Break in Data Processing**

```kotlin
val data = listOf(1, 2, 3, -1, 4, 5)  // -1 is sentinel value
var sum = 0

for (item in data) {
    if (item == -1) {
        break  // Stop processing at sentinel value
    }
    sum += item
}

println("Sum before sentinel: $sum")
```

## 🔍 When to Use Each Statement

### **✅ Use Break When:**

1. **Searching for items**:
   ```kotlin
   for (item in list) {
       if (item == target) {
           println("Found: $item")
           break  // Exit after finding
       }
   }
   ```

2. **Error conditions**:
   ```kotlin
   for (i in 1..10) {
       if (i == 0) {
           println("Error: Division by zero")
           break  // Exit on error
       }
       println(100 / i)
   }
   ```

3. **Performance optimization**:
   ```kotlin
   for (i in 1..1000) {
       if (i * i > 100) {
           break  // Exit when condition met
       }
       println("$i squared is ${i * i}")
   }
   ```

### **✅ Use Continue When:**

1. **Filtering data**:
   ```kotlin
   for (number in numbers) {
       if (number < 0) {
           continue  // Skip negative numbers
       }
       processPositiveNumber(number)
   }
   ```

2. **Skipping invalid input**:
   ```kotlin
   for (input in inputs) {
       if (!isValid(input)) {
           continue  // Skip invalid input
       }
       processValidInput(input)
   }
   ```

3. **Conditional processing**:
   ```kotlin
   for (i in 1..10) {
       if (i % 2 == 0) {
           continue  // Skip even numbers
       }
       processOddNumber(i)
   }
   ```

## 🚨 Common Mistakes to Avoid

### **1. Infinite Loops with Continue**

```kotlin
// ❌ Infinite loop - i never increments
var i = 1
while (i <= 10) {
    if (i % 2 == 0) {
        continue  // Skips the rest of the loop body
    }
    println(i)
    i++  // This line is never reached for even numbers!
}

// ✅ Correct - increment before continue
var i = 1
while (i <= 10) {
    if (i % 2 == 0) {
        i++  // Increment first
        continue
    }
    println(i)
    i++
}
```

### **2. Unreachable Code After Break**

```kotlin
// ❌ Unreachable code
for (i in 1..10) {
    if (i == 5) {
        break
        println("This will never execute")  // Unreachable
    }
    println(i)
}

// ✅ Correct - no unreachable code
for (i in 1..10) {
    if (i == 5) {
        break
    }
    println(i)
}
```

### **3. Wrong Label Usage**

```kotlin
// ❌ Label doesn't exist
for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2) {
            break@nonexistent  // Compile error
        }
    }
}

// ✅ Correct label usage
outer@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2) {
            break@outer  // Valid label
        }
    }
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use descriptive labels**:
   ```kotlin
   searchLoop@ for (i in 1..100) {
       if (found) break@searchLoop
   }
   ```

2. **Keep break/continue conditions simple**:
   ```kotlin
   // ✅ Simple and clear
   if (item == target) break
   
   // ❌ Complex condition
   if (item == target && !isProcessed && isValid) break
   ```

3. **Document complex control flow**:
   ```kotlin
   // Skip invalid entries and stop at sentinel
   for (entry in entries) {
       if (!isValid(entry)) continue  // Skip invalid
       if (entry == SENTINEL) break    // Stop at sentinel
       process(entry)
   }
   ```

### **❌ Don'ts**

1. **Don't overuse break/continue**:
   ```kotlin
   // ❌ Too many control statements
   for (i in 1..10) {
       if (i == 1) continue
       if (i == 2) continue
       if (i == 3) break
       if (i == 4) continue
       println(i)
   }
   ```

2. **Don't create deeply nested control flow**:
   ```kotlin
   // ❌ Hard to follow
   outer@ for (i in 1..3) {
       for (j in 1..3) {
           for (k in 1..3) {
               if (condition) break@outer
           }
       }
   }
   ```

## 🎯 What's Next?

Excellent! You've mastered break and continue statements in Kotlin. Now you're ready to:

1. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
2. **Explore collections** → [Arrays](../collections/01-arrays.md)
3. **Understand OOP** → [Classes and Constructors](../oop/01-classes-constructors.md)
4. **Learn functional programming** → [Lambdas](../functional-programming/01-lambdas.md)

## 📚 Additional Resources

- [Kotlin Returns and Jumps](https://kotlinlang.org/docs/returns.html)
- [Control Flow](https://kotlinlang.org/docs/control-flow.html)
- [Loop Control](https://kotlinlang.org/docs/returns.html#break-and-continue-labels)

## 🏆 Summary

- ✅ You can use break statements to exit loops early
- ✅ You can use continue statements to skip iterations
- ✅ You understand labeled break and continue
- ✅ You can choose the right control statement for your needs
- ✅ You can write more efficient and readable loops
- ✅ You're ready to create sophisticated loop control logic!

**Keep practicing and happy coding! 🎉**
