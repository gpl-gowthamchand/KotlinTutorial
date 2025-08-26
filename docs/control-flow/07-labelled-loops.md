# 🏷️ Labelled Loops in Kotlin

Labelled loops are a powerful feature in Kotlin that allows you to control nested loops with precision. They're especially useful when you need to break out of or continue from specific loops in complex nested structures.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what labelled loops are and when to use them
- ✅ Use labels with break and continue statements
- ✅ Control nested loops effectively
- ✅ Write cleaner, more readable nested loop code
- ✅ Avoid common pitfalls with labelled loops

## 🔍 What You'll Learn

- **Loop labels** - How to label loops for identification
- **Labelled break** - Breaking out of specific loops
- **Labelled continue** - Continuing specific loops
- **Nested loop control** - Managing complex loop structures
- **Best practices** - When and how to use labels effectively

## 📝 Prerequisites

- Understanding of [For Loops](03-for-loops.md)
- Knowledge of [While Loops](04-while-loops.md)
- Familiarity with [Break and Continue](05-break-continue.md)

## 💻 The Code

Let's examine labelled loops in action:

**📁 File:** [15_break_keyword.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/15_break_keyword.kt)

## 🔍 Code Breakdown

### **1. Basic Labelled Loops**

#### **What are Labels?**
A label is an identifier followed by `@` that you can use to mark loops, expressions, or functions. When used with `break` or `continue`, it allows you to control which specific loop to break out of or continue.

#### **Label Syntax**
```kotlin
fun main() {
    // Label the outer loop
    outer@ for (i in 1..3) {
        for (j in 1..3) {
            if (i == 2 && j == 2) {
                // Break out of the outer loop
                break@outer
            }
            println("i=$i, j=$j")
        }
    }
    println("Outer loop finished")
}
```

**Output:**
```
i=1, j=1
i=1, j=2
i=1, j=3
i=2, j=1
Outer loop finished
```

### **2. Labelled Break Examples**

#### **Breaking Out of Nested Loops**
```kotlin
fun findElementExample() {
    val matrix = arrayOf(
        intArrayOf(1, 2, 3),
        intArrayOf(4, 5, 6),
        intArrayOf(7, 8, 9)
    )
    
    val target = 5
    var found = false
    
    // Label the outer loop
    search@ for (row in matrix.indices) {
        for (col in matrix[row].indices) {
            if (matrix[row][col] == target) {
                println("Found $target at position [$row][$col]")
                found = true
                // Break out of both loops
                break@search
            }
        }
    }
    
    if (!found) {
        println("$target not found in matrix")
    }
}
```

#### **Complex Nested Structure**
```kotlin
fun complexNestedExample() {
    val data = listOf(
        listOf(1, 2, 3),
        listOf(4, 5, 6),
        listOf(7, 8, 9)
    )
    
    process@ for (list in data) {
        for (item in list) {
            if (item < 0) {
                println("Found negative number: $item")
                // Skip processing this entire list
                continue@process
            }
            
            if (item == 0) {
                println("Found zero, stopping all processing")
                // Stop processing all lists
                break@process
            }
            
            println("Processing: $item")
        }
        println("Finished processing list")
    }
}
```

### **3. Labelled Continue Examples**

#### **Continuing Specific Loops**
```kotlin
fun continueExample() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    outer@ for (i in 0 until numbers.size) {
        if (i % 2 == 0) {
            // Skip even indices
            continue@outer
        }
        
        for (j in 0 until i) {
            if (j == 3) {
                // Skip to next iteration of outer loop
                continue@outer
            }
            println("Processing i=$i, j=$j")
        }
        
        println("Completed processing for i=$i")
    }
}
```

#### **Matrix Processing with Continue**
```kotlin
fun matrixProcessingExample() {
    val matrix = arrayOf(
        intArrayOf(1, 2, 3, 4),
        intArrayOf(5, 6, 7, 8),
        intArrayOf(9, 10, 11, 12)
    )
    
    row@ for (row in matrix.indices) {
        var rowSum = 0
        
        for (col in matrix[row].indices) {
            val value = matrix[row][col]
            
            if (value < 0) {
                println("Skipping negative value in row $row")
                // Skip this entire row
                continue@row
            }
            
            if (value == 0) {
                println("Found zero in row $row, column $col")
                // Skip this element but continue with the row
                continue
            }
            
            rowSum += value
        }
        
        println("Row $row sum: $rowSum")
    }
}
```

### **4. Advanced Labelled Loop Patterns**

#### **Multiple Labels**
```kotlin
fun multipleLabelsExample() {
    val data = listOf(
        listOf(1, 2, 3),
        listOf(4, 5, 6),
        listOf(7, 8, 9)
    )
    
    outer@ for (i in data.indices) {
        middle@ for (j in data[i].indices) {
            inner@ for (k in 0..2) {
                val value = data[i][j] + k
                
                when {
                    value < 0 -> {
                        println("Negative value, skip inner loop")
                        continue@inner
                    }
                    value > 10 -> {
                        println("Value too high, skip middle loop")
                        continue@middle
                    }
                    value == 5 -> {
                        println("Found target value, exit all loops")
                        break@outer
                    }
                    else -> {
                        println("Processing value: $value")
                    }
                }
            }
        }
    }
}
```

#### **Conditional Labelling**
```kotlin
fun conditionalLabellingExample() {
    val shouldUseLabels = true
    
    if (shouldUseLabels) {
        labelled@ for (i in 1..5) {
            for (j in 1..5) {
                if (i * j > 20) {
                    println("Product too large, breaking outer loop")
                    break@labelled
                }
                println("i=$i, j=$j, product=${i * j}")
            }
        }
    } else {
        // Regular nested loops without labels
        for (i in 1..5) {
            for (j in 1..5) {
                if (i * j > 20) {
                    println("Product too large, breaking inner loop only")
                    break
                }
                println("i=$i, j=$j, product=${i * j}")
            }
        }
    }
}
```

### **5. Real-World Examples**

#### **Game Board Processing**
```kotlin
fun gameBoardExample() {
    val board = Array(8) { Array(8) { 0 } }
    
    // Place some pieces
    board[0][0] = 1  // White piece
    board[7][7] = 2  // Black piece
    
    // Find all pieces of a specific type
    val targetPiece = 1
    val positions = mutableListOf<Pair<Int, Int>>()
    
    search@ for (row in board.indices) {
        for (col in board[row].indices) {
            if (board[row][col] == targetPiece) {
                positions.add(Pair(row, col))
                
                // If we found enough pieces, stop searching
                if (positions.size >= 3) {
                    break@search
                }
            }
        }
    }
    
    println("Found ${positions.size} pieces of type $targetPiece")
    positions.forEach { (row, col) ->
        println("Position: [$row][$col]")
    }
}
```

#### **Data Validation**
```kotlin
fun dataValidationExample() {
    val users = listOf(
        mapOf("name" to "Alice", "age" to 25, "email" to "alice@example.com"),
        mapOf("name" to "Bob", "age" to -5, "email" to "invalid-email"),
        mapOf("name" to "Charlie", "age" to 30, "email" to "charlie@example.com")
    )
    
    val validUsers = mutableListOf<Map<String, Any>>()
    
    user@ for (user in users) {
        // Validate name
        if (user["name"] !is String || (user["name"] as String).isEmpty()) {
            println("Invalid name for user: $user")
            continue@user
        }
        
        // Validate age
        if (user["age"] !is Int || (user["age"] as Int) <= 0) {
            println("Invalid age for user: $user")
            continue@user
        }
        
        // Validate email
        if (user["email"] !is String || !(user["email"] as String).contains("@")) {
            println("Invalid email for user: $user")
            continue@user
        }
        
        validUsers.add(user)
        println("Valid user added: ${user["name"]}")
    }
    
    println("Total valid users: ${validUsers.size}")
}
```

## 🎯 Key Concepts Explained

### **1. Label Syntax**

**Basic Label:**
```kotlin
labelName@ for (item in collection) {
    // Loop body
}
```

**Using Label with Break:**
```kotlin
break@labelName
```

**Using Label with Continue:**
```kotlin
continue@labelName
```

### **2. When to Use Labels**

**Use Labels when:**
- You have deeply nested loops
- You need to break out of or continue specific loops
- You want to make your code more readable
- You're dealing with complex loop logic

**Don't Use Labels when:**
- You have simple, single loops
- The logic is straightforward
- You can refactor to avoid deep nesting

### **3. Label Naming Conventions**

- Use descriptive names: `outer@`, `inner@`, `search@`
- Keep names short but meaningful
- Use lowercase with descriptive words
- Avoid generic names like `loop@` or `break@`

## 🚀 Advanced Patterns

### **1. Functional Alternative**
```kotlin
// Instead of labelled loops, consider functional approaches
fun functionalAlternative() {
    val matrix = arrayOf(
        intArrayOf(1, 2, 3),
        intArrayOf(4, 5, 6),
        intArrayOf(7, 8, 9)
    )
    
    // Find first occurrence of target
    val target = 5
    val position = matrix.asSequence()
        .flatMapIndexed { rowIndex, row ->
            row.asSequence().mapIndexed { colIndex, value ->
                Triple(rowIndex, colIndex, value)
            }
        }
        .find { it.third == target }
    
    position?.let { (row, col, value) ->
        println("Found $value at position [$row][$col]")
    }
}
```

### **2. Early Return Pattern**
```kotlin
fun earlyReturnExample() {
    val data = listOf(
        listOf(1, 2, 3),
        listOf(4, 5, 6),
        listOf(7, 8, 9)
    )
    
    fun processData(): Boolean {
        for (list in data) {
            for (item in list) {
                if (item < 0) {
                    return false  // Early return instead of labelled break
                }
                if (item == 0) {
                    return true   // Early return for success
                }
            }
        }
        return false
    }
    
    val result = processData()
    println("Processing result: $result")
}
```

## 💡 Best Practices

### **1. Keep Labels Simple**
- Use clear, descriptive names
- Don't nest too deeply (max 3-4 levels)
- Consider refactoring complex nested loops

### **2. Use Labels Sparingly**
- Only when they significantly improve readability
- Consider functional alternatives first
- Document complex labelled loop logic

### **3. Consistent Naming**
- Use consistent label naming across your codebase
- Follow team conventions
- Make labels self-documenting

## 🔧 Common Pitfalls

### **1. Infinite Loops with Labels**
```kotlin
// ❌ Wrong - Infinite loop
outer@ while (true) {
    for (i in 1..5) {
        if (i == 3) {
            continue@outer  // This continues the infinite while loop!
        }
        println(i)
    }
}

// ✅ Correct - Limited loop
outer@ for (iteration in 1..10) {
    for (i in 1..5) {
        if (i == 3) {
            continue@outer
        }
        println("Iteration $iteration, value $i")
    }
}
```

### **2. Unreachable Code**
```kotlin
// ❌ Wrong - Unreachable code after break
for (i in 1..5) {
    if (i == 3) {
        break
        println("This will never execute")  // Unreachable
    }
}

// ✅ Correct - No unreachable code
for (i in 1..5) {
    if (i == 3) {
        break
    }
    println("Processing $i")
}
```

### **3. Label Scope Issues**
```kotlin
// ❌ Wrong - Label not in scope
fun badExample() {
    for (i in 1..5) {
        if (i == 3) {
            break@outer  // Error: label 'outer' is not defined
        }
    }
}

// ✅ Correct - Label in proper scope
fun goodExample() {
    outer@ for (i in 1..5) {
        if (i == 3) {
            break@outer  // Works correctly
        }
    }
}
```

## 📚 Summary

Labelled loops are powerful tools for controlling nested loop execution. They're essential for:
- **Complex nested loop logic**
- **Precise loop control**
- **Improved code readability**
- **Efficient algorithm implementation**

## 🎯 Practice Exercises

1. **Matrix Search**: Create a function that searches a 2D matrix and breaks out of both loops when a target is found
2. **Data Processing**: Implement a data validation loop that continues to the next item when invalid data is found
3. **Game Logic**: Build a simple game loop with multiple nested loops and appropriate labels
4. **Performance Optimization**: Use labels to optimize a nested loop that processes large datasets

## 🔗 Related Topics

- [For Loops](03-for-loops.md) - Basic loop structures
- [While Loops](04-while-loops.md) - Conditional loops
- [Break and Continue](05-break-continue.md) - Loop control statements
- [Collections](../collections/01-arrays.md) - Data structures for iteration

## 📖 Additional Resources

- [Official Kotlin Control Flow Documentation](https://kotlinlang.org/docs/control-flow.html)
- [Returns and Jumps](https://kotlinlang.org/docs/returns.html)
- [Loop Control Best Practices](https://kotlinlang.org/docs/returns.html#break-and-continue-labels)

---

**Next Lesson**: [Functions Basics](../functions/01-functions-basics.md) - Learn about function fundamentals

**Happy coding with Labelled Loops! 🏷️**
