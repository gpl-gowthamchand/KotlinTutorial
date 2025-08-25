# 🎯 If Expressions in Kotlin

Welcome to the world of decision-making in Kotlin! If expressions allow your programs to make choices and execute different code based on conditions. This is where your programs start to become truly dynamic and intelligent.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write basic if-else statements
- ✅ Use if expressions to return values
- ✅ Understand the difference between statements and expressions
- ✅ Create nested if conditions
- ✅ Use logical operators in conditions

## 🔍 What You'll Learn

- **Basic if statements** - Simple decision-making
- **If expressions** - Using if to return values
- **If-else chains** - Multiple conditions
- **Nested if statements** - Complex decision trees
- **Logical operators** - Combining conditions

## 📝 Prerequisites

- Basic understanding of variables and data types
- Completed [String Interpolation](../basics/05-string-interpolation.md) lesson

## 💻 The Code

Let's examine the if expression example:

```kotlin
fun main(args: Array<String>) {
    val a = 2
    val b = 5

    var maxValue: Int = if (a > b) {
                            print("a is greater")
                            a
                        } else {
                            print("b is greater")
                            b
                        }

    println(maxValue)
}
```

**📁 File:** [10_if_expression.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/10_if_expression.kt)

## 🔍 Code Breakdown

### **Variable Declaration**

```kotlin
val a = 2
val b = 5
```

- **Two integers** for comparison
- **`val`** makes them immutable (cannot be changed)

### **If Expression**

```kotlin
var maxValue: Int = if (a > b) {
                        print("a is greater")
                        a
                    } else {
                        print("b is greater")
                        b
                    }
```

- **`if (a > b)`**: Condition to check if `a` is greater than `b`
- **`{ }`**: Code block for when condition is true
- **`else`**: Code block for when condition is false
- **`a` and `b`**: Values returned by the if expression
- **`maxValue`**: Variable that stores the result

## 🎯 Key Concepts Explained

### **1. If Statements vs If Expressions**

#### **Traditional If Statement (No Return Value)**

```kotlin
val a = 10
val b = 5

if (a > b) {
    println("a is greater")
} else {
    println("b is greater")
}
```

**Characteristics:**
- Executes code blocks
- No return value
- Used for side effects (printing, calculations)

#### **If Expression (Returns a Value)**

```kotlin
val a = 10
val b = 5

val maxValue = if (a > b) a else b
println("Maximum value: $maxValue")
```

**Characteristics:**
- Returns a value
- Can be assigned to variables
- More functional programming style

### **2. Basic If Statement Syntax**

```kotlin
if (condition) {
    // Code to execute when condition is true
} else {
    // Code to execute when condition is false
}
```

**Components:**
- **`if (condition)`**: Boolean expression that evaluates to true/false
- **`{ }`**: Code blocks containing statements
- **`else`**: Optional alternative execution path

### **3. If Expression Syntax**

```kotlin
val result = if (condition) {
    // Code block that returns a value
    value1
} else {
    // Code block that returns a value
    value2
}
```

**Key Points:**
- **Last expression** in each block becomes the return value
- **Same type** must be returned from both branches
- **Can be assigned** directly to variables

## 🧪 Hands-On Exercises

### **Exercise 1: Basic If Statement**
Create a program that checks if a number is positive, negative, or zero:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val number = -5
    
    if (number > 0) {
        println("$number is positive")
    } else if (number < 0) {
        println("$number is negative")
    } else {
        println("$number is zero")
    }
}
```

### **Exercise 2: If Expression for Grade Calculation**
Use if expressions to calculate a letter grade:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val score = 85
    
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
    
    println("Score: $score, Grade: $grade")
}
```

### **Exercise 3: Complex If Expression**
Create a program that determines the best discount based on purchase amount and customer type:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val purchaseAmount = 150.0
    val isPremiumCustomer = true
    
    val discount = if (isPremiumCustomer) {
        if (purchaseAmount >= 200) {
            purchaseAmount * 0.20  // 20% discount
        } else if (purchaseAmount >= 100) {
            purchaseAmount * 0.15  // 15% discount
        } else {
            purchaseAmount * 0.10  // 10% discount
        }
    } else {
        if (purchaseAmount >= 200) {
            purchaseAmount * 0.10  // 10% discount
        } else if (purchaseAmount >= 100) {
            purchaseAmount * 0.05  // 5% discount
        } else {
            0.0  // No discount
        }
    }
    
    val finalAmount = purchaseAmount - discount
    println("Purchase Amount: $${purchaseAmount}")
    println("Discount: $${discount}")
    println("Final Amount: $${finalAmount}")
}
```

### **Exercise 4: Logical Operators in If**
Create a program that checks multiple conditions:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val age = 25
    val hasLicense = true
    val hasInsurance = false
    
    val canDrive = if (age >= 18 && hasLicense) {
        if (hasInsurance) {
            "Can drive safely with insurance"
        } else {
            "Can drive but needs insurance"
        }
    } else if (age < 18) {
        "Too young to drive"
    } else {
        "Needs a driver's license"
    }
    
    println(canDrive)
}
```

## 🔍 Advanced If Expression Concepts

### **1. Single-Line If Expressions**

```kotlin
val max = if (a > b) a else b
val status = if (isActive) "Online" else "Offline"
val message = if (age >= 18) "Adult" else "Minor"
```

**Use when:**
- Simple conditions
- Single expressions
- Quick assignments

### **2. Multi-Line If Expressions**

```kotlin
val result = if (condition) {
    val temp = calculateTemp()
    val processed = process(temp)
    processed
} else {
    val default = getDefault()
    default
}
```

**Use when:**
- Complex calculations
- Multiple steps
- Need intermediate variables

### **3. Nested If Expressions**

```kotlin
val category = if (age < 13) {
    "Child"
} else if (age < 20) {
    if (isStudent) "Teen Student" else "Teen"
} else if (age < 65) {
    if (isWorking) "Working Adult" else "Adult"
} else {
    "Senior"
}
```

## 🔍 Logical Operators

### **Comparison Operators**

| Operator | Description | Example |
|----------|-------------|---------|
| **`==`** | Equal to | `a == b` |
| **`!=`** | Not equal to | `a != b` |
| **`>`** | Greater than | `a > b` |
| **`<`** | Less than | `a < b` |
| **`>=`** | Greater than or equal to | `a >= b` |
| **`<=`** | Less than or equal to | `a <= b` |

### **Logical Operators**

| Operator | Description | Example |
|----------|-------------|---------|
| **`&&`** | AND (both must be true) | `a > 0 && b > 0` |
| **`\|\|`** | OR (at least one must be true) | `a > 0 \|\| b > 0` |
| **`!`** | NOT (inverts the condition) | `!(a > 0)` |

### **Examples**

```kotlin
val age = 25
val hasLicense = true
val hasInsurance = false

// Multiple conditions
val canDrive = age >= 18 && hasLicense
val needsInsurance = canDrive && !hasInsurance
val isEligible = age >= 18 && (hasLicense || hasInsurance)
```

## 🚨 Common Mistakes to Avoid

1. **Missing else branch in expressions**:
   ```kotlin
   val result = if (a > b) a  // ❌ Missing else branch
   val result = if (a > b) a else b  // ✅ Correct
   ```

2. **Using assignment instead of comparison**:
   ```kotlin
   if (a = 5) { }  // ❌ Assignment, not comparison
   if (a == 5) { } // ✅ Comparison
   ```

3. **Forgetting curly braces for multiple statements**:
   ```kotlin
   if (a > b) println("a is greater"); a  // ❌ Only first statement executes
   if (a > b) { println("a is greater"); a }  // ✅ Both statements execute
   ```

4. **Inconsistent return types**:
   ```kotlin
   val result = if (a > b) "Greater" else 42  // ❌ Different types
   val result = if (a > b) "Greater" else "Less"  // ✅ Same type
   ```

## 🎯 What's Next?

Excellent! You've mastered if expressions in Kotlin. Now you're ready to:

1. **Learn when expressions** → [When Expressions](02-when-expressions.md)
2. **Understand loops** → [For Loops](03-for-loops.md)
3. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
4. **Explore collections** → [Arrays](../collections/01-arrays.md)

## 📚 Additional Resources

- [Kotlin Control Flow](https://kotlinlang.org/docs/control-flow.html)
- [If Expressions](https://kotlinlang.org/docs/control-flow.html#if-expression)
- [When Expression](https://kotlinlang.org/docs/control-flow.html#when-expression)

## 🏆 Summary

- ✅ You can write basic if-else statements
- ✅ You can use if expressions to return values
- ✅ You understand the difference between statements and expressions
- ✅ You can create nested if conditions
- ✅ You can use logical operators in conditions
- ✅ You're ready to make your programs intelligent!

**Keep practicing and happy coding! 🎉**
