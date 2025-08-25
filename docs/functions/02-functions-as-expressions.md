# 🎭 Functions as Expressions in Kotlin

Welcome to the elegant world of functions as expressions! In Kotlin, functions can be written as single expressions, making your code more concise and readable. This powerful feature eliminates the need for explicit return statements and curly braces in many cases.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write single-expression functions
- ✅ Understand when to use expression syntax
- ✅ Convert traditional functions to expression syntax
- ✅ Use expression functions with control flow
- ✅ Write more concise and readable code

## 🔍 What You'll Learn

- **Single-expression functions** - Concise function syntax
- **Expression vs statement functions** - When to use each
- **Control flow in expressions** - If, when, and loops
- **Type inference** - Automatic return type detection
- **Best practices** - Readability and maintainability

## 📝 Prerequisites

- Basic understanding of functions
- Completed [Functions Basics](01-functions-basics.md) lesson
- Knowledge of if expressions and control flow

## 💻 The Code

Let's examine the functions as expressions example:

```kotlin
fun max(a: Int, b: Int): Int = if (a > b) {
    println("$a is greater")
    a
} else {
    println("$b is greater")
    b
}
```

**📁 File:** [18_functions_as_expressions.kt](src/18_functions_as_expressions.kt)

## 🔍 Code Breakdown

### **Function Declaration**

```kotlin
fun max(a: Int, b: Int): Int = if (a > b) {
    println("$a is greater")
    a
} else {
    println("$b is greater")
    b
}
```

- **`fun max(a: Int, b: Int): Int`**: Function signature with parameters and return type
- **`=`**: Expression syntax indicator (replaces `{ return }`)
- **`if (a > b) { ... } else { ... }`**: If expression that returns a value
- **`a` and `b`**: Return values from each branch

### **Main Function Usage**

```kotlin
fun main(args: Array<String>) {
    var largeValue = max(4, 6)
    println("The greater number is $largeValue")
}
```

- **`max(4, 6)`**: Function call with arguments
- **`largeValue`**: Stores the returned result
- **Output**: "The greater number is 6"

## 🎯 Key Concepts Explained

### **1. Expression vs Statement Functions**

#### **Traditional Function (Statement)**

```kotlin
fun add(a: Int, b: Int): Int {
    return a + b
}
```

**Characteristics:**
- Uses curly braces `{ }`
- Explicit `return` statement
- Can have multiple statements
- Good for complex logic

#### **Expression Function**

```kotlin
fun add(a: Int, b: Int): Int = a + b
```

**Characteristics:**
- Uses `=` instead of `{ }`
- No explicit `return`
- Single expression
- More concise

### **2. When to Use Expression Syntax**

#### **✅ Perfect for Expression Functions:**

1. **Simple calculations**:
   ```kotlin
   fun square(x: Int): Int = x * x
   fun cube(x: Int): Int = x * x * x
   fun abs(x: Int): Int = if (x < 0) -x else x
   ```

2. **Boolean checks**:
   ```kotlin
   fun isEven(n: Int): Boolean = n % 2 == 0
   fun isPositive(n: Int): Boolean = n > 0
   fun isInRange(n: Int, min: Int, max: Int): Boolean = n in min..max
   ```

3. **Simple transformations**:
   ```kotlin
   fun capitalize(str: String): String = str.capitalize()
   fun reverse(str: String): String = str.reversed()
   fun double(n: Int): Int = n * 2
   ```

#### **❌ Avoid Expression Functions When:**

1. **Multiple statements needed**:
   ```kotlin
   // ❌ Don't do this - too complex
   fun processData(data: String): String = data.trim().toLowerCase().replace(" ", "_")
   
   // ✅ Better as traditional function
   fun processData(data: String): String {
       return data.trim()
           .toLowerCase()
           .replace(" ", "_")
   }
   ```

2. **Complex logic with side effects**:
   ```kotlin
   // ❌ Don't do this - side effects in expression
   fun validateUser(user: User): Boolean = user.name.isNotEmpty() && user.email.isNotEmpty() && println("User validated")
   
   // ✅ Better as traditional function
   fun validateUser(user: User): Boolean {
       val isValid = user.name.isNotEmpty() && user.email.isNotEmpty()
       if (isValid) println("User validated")
       return isValid
   }
   ```

### **3. Type Inference with Expression Functions**

#### **Explicit Return Type**

```kotlin
fun max(a: Int, b: Int): Int = if (a > b) a else b
```

#### **Inferred Return Type**

```kotlin
fun max(a: Int, b: Int) = if (a > b) a else b  // Type inferred as Int
fun isEven(n: Int) = n % 2 == 0                 // Type inferred as Boolean
fun greet(name: String) = "Hello, $name!"       // Type inferred as String
```

**Type Inference Rules:**
- **Simple expressions**: Type is automatically inferred
- **Complex expressions**: Explicit type may be needed
- **Generic functions**: Usually need explicit type parameters

## 🧪 Hands-On Exercises

### **Exercise 1: Convert to Expression Function**
Convert this traditional function to an expression function:

```kotlin
fun isAdult(age: Int): Boolean {
    return age >= 18
}
```

**Solution:**
```kotlin
fun isAdult(age: Int): Boolean = age >= 18
```

### **Exercise 2: Create Expression Functions**
Create expression functions for these operations:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create these functions as expressions
    // 1. Check if number is prime
    // 2. Get the minimum of three numbers
    // 3. Check if string is palindrome
}
```

**Solution:**
```kotlin
// Check if number is prime (simplified)
fun isPrime(n: Int): Boolean = n > 1 && (2..n/2).none { n % it == 0 }

// Get minimum of three numbers
fun minOfThree(a: Int, b: Int, c: Int): Int = minOf(a, b, c)

// Check if string is palindrome
fun isPalindrome(str: String): Boolean = str == str.reversed()

fun main(args: Array<String>) {
    println("Is 17 prime? ${isPrime(17)}")
    println("Min of 5, 2, 8: ${minOfThree(5, 2, 8)}")
    println("Is 'racecar' palindrome? ${isPalindrome("racecar")}")
}
```

### **Exercise 3: Control Flow in Expressions**
Create expression functions using if and when expressions:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create these functions using control flow
    // 1. Grade calculator (A, B, C, D, F)
    // 2. Day of week name
    // 3. Season determiner
}
```

**Solution:**
```kotlin
// Grade calculator
fun getGrade(score: Int): String = when {
    score >= 90 -> "A"
    score >= 80 -> "B"
    score >= 70 -> "C"
    score >= 60 -> "D"
    else -> "F"
}

// Day of week name
fun getDayName(day: Int): String = when (day) {
    1 -> "Monday"
    2 -> "Tuesday"
    3 -> "Wednesday"
    4 -> "Thursday"
    5 -> "Friday"
    6 -> "Saturday"
    7 -> "Sunday"
    else -> "Invalid day"
}

// Season determiner
fun getSeason(month: Int): String = when (month) {
    in 3..5 -> "Spring"
    in 6..8 -> "Summer"
    in 9..11 -> "Fall"
    12, 1, 2 -> "Winter"
    else -> "Invalid month"
}

fun main(args: Array<String>) {
    println("Score 85: ${getGrade(85)}")
    println("Day 3: ${getDayName(3)}")
    println("Month 7: ${getSeason(7)}")
}
```

### **Exercise 4: Complex Expression Functions**
Create expression functions that combine multiple operations:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create these complex expression functions
    // 1. Format currency amount
    // 2. Validate email format (simplified)
    // 3. Calculate BMI category
}
```

**Solution:**
```kotlin
// Format currency amount
fun formatCurrency(amount: Double, currency: String = "$"): String = 
    "$currency${String.format("%.2f", amount)}"

// Validate email format (simplified)
fun isValidEmail(email: String): Boolean = 
    email.contains("@") && email.contains(".") && email.length > 5

// Calculate BMI category
fun getBMICategory(weight: Double, height: Double): String {
    val bmi = weight / (height * height)
    return when {
        bmi < 18.5 -> "Underweight"
        bmi < 25 -> "Normal"
        bmi < 30 -> "Overweight"
        else -> "Obese"
    }
}

fun main(args: Array<String>) {
    println("Price: ${formatCurrency(29.99)}")
    println("Email valid? ${isValidEmail("user@example.com")}")
    println("BMI Category: ${getBMICategory(70.0, 1.75)}")
}
```

## 🔍 Advanced Expression Function Patterns

### **1. Nested Expression Functions**

```kotlin
fun processNumber(n: Int): String = 
    if (n > 0) {
        if (n % 2 == 0) "Positive even" else "Positive odd"
    } else if (n < 0) {
        if (n % 2 == 0) "Negative even" else "Negative odd"
    } else "Zero"
```

### **2. Expression Functions with Collections**

```kotlin
fun getFirstEven(numbers: List<Int>): Int? = 
    numbers.firstOrNull { it % 2 == 0 }

fun getSumOfEvens(numbers: List<Int>): Int = 
    numbers.filter { it % 2 == 0 }.sum()

fun hasDuplicates(numbers: List<Int>): Boolean = 
    numbers.size != numbers.distinct().size
```

### **3. Expression Functions with Extension Functions**

```kotlin
fun String.isValidPassword(): Boolean = 
    length >= 8 && any { it.isUpperCase() } && any { it.isDigit() }

fun Int.isInRange(min: Int, max: Int): Boolean = 
    this in min..max

fun List<Int>.getStats(): String = 
    "Count: $size, Sum: ${sum()}, Average: ${average()}"
```

## 🔍 When to Use Each Approach

### **✅ Use Expression Functions When:**

1. **Single operation**:
   ```kotlin
   fun double(x: Int) = x * 2
   fun isEven(x: Int) = x % 2 == 0
   ```

2. **Simple conditional logic**:
   ```kotlin
   fun max(a: Int, b: Int) = if (a > b) a else b
   fun getStatus(age: Int) = if (age >= 18) "Adult" else "Minor"
   ```

3. **Property-like behavior**:
   ```kotlin
   fun getFullName() = "$firstName $lastName"
   fun getDisplayPrice() = "$$price"
   ```

### **✅ Use Traditional Functions When:**

1. **Multiple statements**:
   ```kotlin
   fun processUser(user: User): Boolean {
       val isValid = validateUser(user)
       if (isValid) {
           saveUser(user)
           sendWelcomeEmail(user)
       }
       return isValid
   }
   ```

2. **Complex logic**:
   ```kotlin
   fun calculateTax(income: Double): Double {
       var tax = 0.0
       when {
           income <= 50000 -> tax = income * 0.1
           income <= 100000 -> tax = 5000 + (income - 50000) * 0.2
           else -> tax = 15000 + (income - 100000) * 0.3
       }
       return tax
   }
   ```

3. **Side effects**:
   ```kotlin
   fun logAndProcess(data: String): String {
       println("Processing: $data")
       val result = data.trim().toLowerCase()
       println("Result: $result")
       return result
   }
   ```

## 🚨 Common Mistakes to Avoid

### **1. Forgetting Return Type for Complex Expressions**

```kotlin
// ❌ Type inference may fail for complex expressions
fun processData(data: String) = data.trim().toLowerCase().replace(" ", "_")

// ✅ Explicit type helps compiler and readability
fun processData(data: String): String = data.trim().toLowerCase().replace(" ", "_")
```

### **2. Using Expression Functions for Side Effects**

```kotlin
// ❌ Side effects in expression function
fun validateAndLog(data: String) = data.isNotEmpty() && println("Data is valid")

// ✅ Traditional function for side effects
fun validateAndLog(data: String): Boolean {
    val isValid = data.isNotEmpty()
    if (isValid) println("Data is valid")
    return isValid
}
```

### **3. Overly Complex Expression Functions**

```kotlin
// ❌ Too complex - hard to read
fun getComplexResult(a: Int, b: Int, c: Int) = 
    if (a > b) if (a > c) a else c else if (b > c) b else c

// ✅ Better as traditional function
fun getComplexResult(a: Int, b: Int, c: Int): Int {
    return when {
        a > b && a > c -> a
        b > c -> b
        else -> c
    }
}
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use expression functions for simple operations**:
   ```kotlin
   fun square(x: Int) = x * x
   fun isPositive(x: Int) = x > 0
   ```

2. **Keep expressions readable**:
   ```kotlin
   fun getStatus(age: Int) = if (age >= 18) "Adult" else "Minor"
   ```

3. **Use explicit types when helpful**:
   ```kotlin
   fun processString(input: String): String = input.trim().toLowerCase()
   ```

### **❌ Don'ts**

1. **Don't sacrifice readability for brevity**:
   ```kotlin
   // ❌ Hard to read
   fun f(x:Int,y:Int)=if(x>y)x else y
   
   // ✅ Clear and readable
   fun max(x: Int, y: Int) = if (x > y) x else y
   ```

2. **Don't use expressions for complex logic**:
   ```kotlin
   // ❌ Too complex for expression
   fun calculateComplex(a: Int, b: Int, c: Int) = 
       if (a > 0) if (b > 0) if (c > 0) a + b + c else a + b else if (c > 0) a + c else a else 0
   ```

## 🎯 What's Next?

Excellent! You've mastered functions as expressions in Kotlin. Now you're ready to:

1. **Learn named parameters** → [Named Parameters](03-named-parameters.md)
2. **Explore extension functions** → [Extension Functions](04-extension-functions.md)
3. **Understand infix functions** → [Infix Functions](05-infix-functions.md)
4. **Master tailrec functions** → [Tailrec Functions](06-tailrec-functions.md)

## 📚 Additional Resources

- [Kotlin Functions](https://kotlinlang.org/docs/functions.html)
- [Function Expressions](https://kotlinlang.org/docs/functions.html#single-expression-functions)
- [Type Inference](https://kotlinlang.org/docs/basic-types.html#type-inference)

## 🏆 Summary

- ✅ You can write single-expression functions
- ✅ You understand when to use expression syntax
- ✅ You can convert traditional functions to expression syntax
- ✅ You can use expression functions with control flow
- ✅ You can write more concise and readable code
- ✅ You're ready to create elegant, functional Kotlin code!

**Keep practicing and happy coding! 🎉**

