# 💬 Comments and Documentation in Kotlin

Welcome to the world of code documentation! Comments are essential for making your code readable and maintainable. In this lesson, you'll learn how to write clear, helpful comments in Kotlin.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write single-line comments using `//`
- ✅ Create multi-line comments using `/* */`
- ✅ Understand when and how to use comments effectively
- ✅ Write self-documenting code
- ✅ Follow Kotlin documentation best practices

## 🔍 What You'll Learn

- **Single-line comments** - Quick explanations for individual lines
- **Multi-line comments** - Detailed explanations for code blocks
- **Documentation comments** - Professional documentation standards
- **Comment best practices** - When and how to comment effectively
- **Self-documenting code** - Writing code that explains itself

## 📝 Prerequisites

- Basic understanding of Kotlin syntax
- Completed [Hello World](01-hello-world.md) lesson

## 💻 The Code

Let's examine the comments example:

```kotlin
/*
* This is comment line 1
*
* This is comment line 2
*
* This is main function. Entry point of the application. 
* */

fun main(args: Array<String>) {     // This is inline comment ...
    print("Hello World")
}
```

**📁 File:** [03_comments.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/03_comments.kt)

## 🔍 Code Breakdown

### **Multi-line Comment Block**

```kotlin
/*
* This is comment line 1
*
* This is comment line 2
*
* This is main function. Entry point of the application. 
* */
```

- **`/*`**: Starts a multi-line comment block
- **`*`**: Each line can start with an asterisk for readability
- **`*/`**: Ends the multi-line comment block
- **Purpose**: Explains what the following code does

### **Single-line Comment**

```kotlin
fun main(args: Array<String>) {     // This is inline comment ...
    print("Hello World")
}
```

- **`//`**: Starts a single-line comment
- **Inline comment**: Appears on the same line as code
- **Purpose**: Quick explanation of the specific line

## 🎯 Key Concepts Explained

### **1. Single-line Comments (`//`)**

```kotlin
// This is a single-line comment
val name = "John"  // This comment explains the variable
val age = 25       // Age in years
```

**Use cases:**
- Quick explanations for single lines
- Clarifying complex expressions
- Adding context to variables
- Explaining "why" not "what"

### **2. Multi-line Comments (`/* */`)**

```kotlin
/*
 * This is a multi-line comment
 * It can span multiple lines
 * Useful for explaining complex logic
 * or documenting functions
 */
fun calculateArea(radius: Double): Double {
    return Math.PI * radius * radius
}
```

**Use cases:**
- Explaining complex algorithms
- Documenting functions and classes
- Providing context for code blocks
- License information or file headers

### **3. KDoc Comments (`/** */`)**

```kotlin
/**
 * Calculates the area of a circle
 * 
 * @param radius The radius of the circle
 * @return The area of the circle
 * @throws IllegalArgumentException if radius is negative
 */
fun calculateArea(radius: Double): Double {
    require(radius >= 0) { "Radius cannot be negative" }
    return Math.PI * radius * radius
}
```

**Use cases:**
- API documentation
- Function and class documentation
- Parameter and return value descriptions
- Exception documentation

## 🧪 Hands-On Exercises

### **Exercise 1: Add Comments to Code**
Add appropriate comments to this code:

```kotlin
fun main(args: Array<String>) {
    val temperature = 25
    val isHot = temperature > 30
    if (isHot) {
        println("It's hot today!")
    } else {
        println("It's not too hot.")
    }
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    // Get current temperature in Celsius
    val temperature = 25
    
    // Check if temperature is considered hot (above 30°C)
    val isHot = temperature > 30
    
    // Display appropriate message based on temperature
    if (isHot) {
        println("It's hot today!")
    } else {
        println("It's not too hot.")
    }
}
```

### **Exercise 2: Create a Well-Documented Function**
Write a function with comprehensive comments:

```kotlin
// TODO: Add your solution here
```

**Solution:**
```kotlin
/**
 * Calculates the grade based on a numerical score
 * 
 * @param score The numerical score (0-100)
 * @return The letter grade (A, B, C, D, or F)
 * @throws IllegalArgumentException if score is not between 0 and 100
 */
fun calculateGrade(score: Int): Char {
    // Validate input range
    require(score in 0..100) { "Score must be between 0 and 100" }
    
    // Determine grade based on score ranges
    return when {
        score >= 90 -> 'A'  // 90-100: A grade
        score >= 80 -> 'B'  // 80-89: B grade
        score >= 70 -> 'C'  // 70-79: C grade
        score >= 60 -> 'D'  // 60-69: D grade
        else -> 'F'          // 0-59: F grade
    }
}
```

### **Exercise 3: Comment Types Practice**
Create examples of all three comment types:

```kotlin
// TODO: Add your solution here
```

**Solution:**
```kotlin
// Single-line comment: This function calculates the factorial
fun factorial(n: Int): Int {
    /*
     * Multi-line comment:
     * This function uses recursion to calculate factorial
     * Factorial of n = n * (n-1) * (n-2) * ... * 1
     */
    
    /**
     * KDoc comment:
     * Calculates the factorial of a non-negative integer
     * 
     * @param n The number to calculate factorial for
     * @return The factorial of n
     * @throws IllegalArgumentException if n is negative
     */
    
    require(n >= 0) { "Factorial is not defined for negative numbers" }
    
    return if (n <= 1) 1 else n * factorial(n - 1)
}
```

## 🔍 Comment Best Practices

### **✅ Do's**

1. **Explain "why" not "what"**:
   ```kotlin
   // Good: Explains the reasoning
   val timeout = 5000  // 5 seconds timeout for network operations
   
   // Bad: Obvious from code
   val timeout = 5000  // Sets timeout to 5000
   ```

2. **Keep comments up-to-date**:
   ```kotlin
   // Update this comment when you change the logic
   val maxRetries = 3  // Maximum number of retry attempts
   ```

3. **Use clear, concise language**:
   ```kotlin
   // Good: Clear and specific
   val bufferSize = 1024  // Buffer size optimized for 4K displays
   
   // Bad: Vague and unhelpful
   val bufferSize = 1024  // Some buffer size
   ```

### **❌ Don'ts**

1. **Don't comment obvious code**:
   ```kotlin
   // Bad: Comment adds no value
   val name = "John"  // Assigns "John" to name variable
   
   // Good: No comment needed
   val name = "John"
   ```

2. **Don't leave outdated comments**:
   ```kotlin
   // Bad: Comment is wrong
   val maxUsers = 100  // Maximum 50 users allowed
   
   // Good: Comment matches code
   val maxUsers = 100  // Maximum 100 users allowed
   ```

3. **Don't use comments to fix bad code**:
   ```kotlin
   // Bad: Comment tries to explain confusing code
   val x = a + b * c  // Add a to the product of b and c
   
   // Good: Self-documenting code
   val result = a + (b * c)
   ```

## 🎯 When to Use Comments

### **✅ Good Times to Comment**

1. **Complex algorithms** - Explain the logic step by step
2. **Business rules** - Document why certain decisions are made
3. **Workarounds** - Explain temporary solutions or known issues
4. **API usage** - Document how to use your functions
5. **Non-obvious code** - Explain code that isn't self-explanatory

### **❌ Avoid Commenting**

1. **Obvious code** - Code that explains itself
2. **Temporary code** - Code that will be removed
3. **Bad code** - Fix the code instead of explaining it
4. **Implementation details** - Focus on what and why, not how

## 🔍 Self-Documenting Code Examples

### **Instead of Comments, Use Better Names**

```kotlin
// Bad: Needs comment to explain
val x = 86400000  // Milliseconds in a day

// Good: Self-documenting
val millisecondsInDay = 86400000
```

### **Use Constants for Magic Numbers**

```kotlin
// Bad: Magic number with comment
if (score >= 90) {  // 90 is the threshold for A grade
    grade = 'A'
}

// Good: Named constant
const val A_GRADE_THRESHOLD = 90
if (score >= A_GRADE_THRESHOLD) {
    grade = 'A'
}
```

### **Break Complex Logic into Functions**

```kotlin
// Bad: Complex logic with comments
fun processUser(user: User) {
    // Check if user is eligible for premium features
    if (user.age >= 18 && user.subscriptionType == "premium" && user.paymentStatus == "active") {
        // Enable premium features
        enablePremiumFeatures(user)
    }
}

// Good: Self-documenting functions
fun processUser(user: User) {
    if (isEligibleForPremium(user)) {
        enablePremiumFeatures(user)
    }
}

private fun isEligibleForPremium(user: User): Boolean {
    return user.age >= 18 && 
           user.subscriptionType == "premium" && 
           user.paymentStatus == "active"
}
```

## 🚨 Common Mistakes to Avoid

1. **Commenting obvious code**:
   ```kotlin
   val name = "John"  // Sets name to John  ❌
   ```

2. **Outdated comments**:
   ```kotlin
   val maxUsers = 100  // Maximum 50 users  ❌
   ```

3. **Using comments to explain bad code**:
   ```kotlin
   // This is a hack because the API is broken  ❌
   val result = hackyWorkaround()
   ```

4. **Too many comments**:
   ```kotlin
   // Get the name
   val name = getName()
   // Print the name
   println(name)  ❌
   ```

## 🎯 What's Next?

Excellent! You've learned about comments and documentation. Now you're ready to:

1. **Explore data types** → [Data Types Deep Dive](04-data-types.md)
2. **Learn string operations** → [String Interpolation](05-string-interpolation.md)
3. **Understand control flow** → [If Expressions](../control-flow/01-if-expressions.md)
4. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)

## 📚 Additional Resources

- [Kotlin Documentation](https://kotlinlang.org/docs/kotlin-doc.html)
- [KDoc Reference](https://kotlinlang.org/docs/kotlin-doc.html)
- [Comment Best Practices](https://blog.jetbrains.com/kotlin/2019/02/kotlin-1-3-50-released/)

## 🏆 Summary

- ✅ You can write single-line and multi-line comments
- ✅ You understand when and how to use comments effectively
- ✅ You know how to write self-documenting code
- ✅ You follow Kotlin documentation best practices
- ✅ You're ready to write clear, maintainable code!

**Keep practicing and happy coding! 🎉**
