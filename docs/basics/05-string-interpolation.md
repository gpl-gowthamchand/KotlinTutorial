# 🔤 String Interpolation in Kotlin

Welcome to the world of string interpolation! This powerful feature allows you to embed variables and expressions directly into strings, making your code more readable and maintainable.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Use string interpolation with the `$` symbol
- ✅ Embed variables and expressions in strings
- ✅ Format complex expressions with `${}` syntax
- ✅ Create dynamic and readable string output
- ✅ Understand when and how to use string interpolation

## 🔍 What You'll Learn

- **Basic interpolation** - Embedding simple variables in strings
- **Expression interpolation** - Using complex expressions with `${}`
- **Formatting** - Controlling how values are displayed
- **Best practices** - When and how to use interpolation effectively
- **Performance considerations** - Understanding interpolation overhead

## 📝 Prerequisites

- Basic understanding of variables and data types
- Completed [Data Types Deep Dive](04-data-types.md) lesson

## 💻 The Code

Let's examine the string interpolation example:

```kotlin
fun main(args: Array<String>) {
    var rect = Rectangle()
    rect.length = 5
    rect.breadth = 3

    print("The length of the rectangle is ${rect.length} and breadth is ${rect.breadth}. The area is ${rect.length * rect.breadth}")
}

class Rectangle {
    var length: Int = 0
    var breadth: Int = 0
}
```

**📁 File:** [08_string_interpolation.kt](src/08_string_interpolation.kt)

## 🔍 Code Breakdown

### **Rectangle Class**

```kotlin
class Rectangle {
    var length: Int = 0
    var breadth: Int = 0
}
```

- **Simple class** with two properties
- **`length`** and **`breadth`** represent rectangle dimensions
- **Default values** of 0 for both properties

### **String Interpolation Usage**

```kotlin
print("The length of the rectangle is ${rect.length} and breadth is ${rect.breadth}. The area is ${rect.length * rect.breadth}")
```

- **`${rect.length}`**: Embeds the length value
- **`${rect.breadth}`**: Embeds the breadth value
- **`${rect.length * rect.breadth}`**: Embeds the calculated area

## 🎯 Key Concepts Explained

### **1. Basic String Interpolation**

#### **Simple Variable Interpolation**

```kotlin
val name = "John"
val age = 25
val message = "Hello, my name is $name and I am $age years old"
println(message)
// Output: Hello, my name is John and I am 25 years old
```

**Syntax:**
- **`$variableName`**: Embeds a simple variable
- **No spaces**: Variable name must immediately follow `$`
- **Simple types**: Works with strings, numbers, booleans

#### **Expression Interpolation**

```kotlin
val a = 10
val b = 5
val result = "Sum: ${a + b}, Product: ${a * b}, Difference: ${a - b}"
println(result)
// Output: Sum: 15, Product: 50, Difference: 5
```

**Syntax:**
- **`${expression}`**: Embeds any valid Kotlin expression
- **Curly braces**: Required for complex expressions
- **Arithmetic**: Can include calculations, function calls, etc.

### **2. When to Use Each Syntax**

#### **Use `$variable` for:**
- Simple variable names
- Properties without spaces
- Basic values

```kotlin
val name = "Alice"
val greeting = "Hello $name!"  // ✅ Simple variable
```

#### **Use `${expression}` for:**
- Complex expressions
- Function calls
- Calculations
- Properties with spaces
- Any expression that needs evaluation

```kotlin
val firstName = "John"
val lastName = "Doe"
val fullName = "${firstName} ${lastName}"  // ✅ Expression with spaces

val radius = 5.0
val area = "Area: ${Math.PI * radius * radius}"  // ✅ Complex calculation
```

### **3. Advanced Interpolation Examples**

#### **Function Calls in Interpolation**

```kotlin
fun getCurrentTime(): String = "12:00 PM"

val message = "Current time is ${getCurrentTime()}"
println(message)
// Output: Current time is 12:00 PM
```

#### **Conditional Expressions**

```kotlin
val score = 85
val grade = "Your grade is ${if (score >= 90) 'A' else if (score >= 80) 'B' else 'C'}"
println(grade)
// Output: Your grade is B
```

#### **Object Properties**

```kotlin
data class Person(val name: String, val age: Int)

val person = Person("Bob", 30)
val info = "Person: ${person.name}, Age: ${person.age}"
println(info)
// Output: Person: Bob, Age: 30
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic String Interpolation**
Create a program that uses string interpolation to display personal information:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val name = "Alice"
    val age = 25
    val city = "New York"
    val profession = "Software Developer"
    
    val bio = "Hi, I'm $name, a $age-year-old $profession from $city."
    println(bio)
    
    // Using expressions
    val birthYear = 2024 - age
    val message = "I was born in $birthYear and have been coding for ${age - 18} years."
    println(message)
}
```

### **Exercise 2: Mathematical Expressions**
Create a calculator that displays results using string interpolation:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val a = 15
    val b = 7
    
    println("Numbers: $a and $b")
    println("Sum: ${a + b}")
    println("Difference: ${a - b}")
    println("Product: ${a * b}")
    println("Quotient: ${a / b}")
    println("Remainder: ${a % b}")
    println("Power: ${a.toDouble().pow(b.toDouble())}")
    
    // Calculate average
    val average = (a + b) / 2.0
    println("Average: $average")
}
```

### **Exercise 3: Complex Object Interpolation**
Create a product catalog using string interpolation:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
data class Product(val name: String, val price: Double, val category: String)

fun main(args: Array<String>) {
    val products = listOf(
        Product("Laptop", 999.99, "Electronics"),
        Product("Book", 19.99, "Education"),
        Product("Coffee", 4.99, "Beverages")
    )
    
    for (product in products) {
        val description = """
            Product: ${product.name}
            Price: $${product.price}
            Category: ${product.category}
            Tax (8%): $${product.price * 0.08}
            Total: $${product.price * 1.08}
        """.trimIndent()
        
        println(description)
        println("---")
    }
}
```

### **Exercise 4: Dynamic Messages**
Create a weather app that generates dynamic messages:

```kotlin
fun main(args: Array<String>) {
    // TODO: Add your solution here
}
```

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val temperature = 28
    val humidity = 65
    val isRaining = false
    
    val weatherMessage = """
        🌤️  Weather Report
        Temperature: ${temperature}°C
        Humidity: ${humidity}%
        Conditions: ${if (isRaining) "Rainy" else "Clear"}
        
        ${when {
            temperature > 30 -> "It's hot today! Stay hydrated."
            temperature > 20 -> "Pleasant weather for outdoor activities."
            temperature > 10 -> "Cool weather, bring a light jacket."
            else -> "Cold weather, dress warmly."
        }}
        
        ${if (humidity > 70) "High humidity - expect muggy conditions." else "Comfortable humidity levels."}
    """.trimIndent()
    
    println(weatherMessage)
}
```

## 🔍 String Interpolation vs String Concatenation

### **String Interpolation (Recommended)**

```kotlin
val name = "John"
val age = 25
val message = "Hello $name, you are $age years old"
```

**Advantages:**
- ✅ More readable
- ✅ Less error-prone
- ✅ Better performance
- ✅ Cleaner syntax

### **String Concatenation (Old Way)**

```kotlin
val name = "John"
val age = 25
val message = "Hello " + name + ", you are " + age + " years old"
```

**Disadvantages:**
- ❌ Harder to read
- ❌ More error-prone
- ❌ Poorer performance
- ❌ Verbose syntax

## 🚨 Common Mistakes to Avoid

1. **Missing curly braces for expressions**:
   ```kotlin
   val a = 5
   val b = 3
   val result = "Sum: $a + b"  // ❌ Output: Sum: 5 + b
   val result = "Sum: ${a + b}" // ✅ Output: Sum: 8
   ```

2. **Using `$` in regular strings**:
   ```kotlin
   val price = 100
   val message = "Price: $price"  // ❌ Won't work if you want literal $
   val message = "Price: \$$price" // ✅ Escapes the $ symbol
   ```

3. **Complex expressions without braces**:
   ```kotlin
   val name = "John"
   val message = "Hello $name.toUpperCase()"  // ❌ Won't work
   val message = "Hello ${name.uppercase()}"  // ✅ Correct
   ```

4. **Forgetting to import functions**:
   ```kotlin
   val result = "Power: ${Math.pow(2.0, 3.0)}"  // ❌ Math not imported
   import kotlin.math.pow
   val result = "Power: ${2.0.pow(3.0)}"        // ✅ Correct
   ```

## 🎯 What's Next?

Excellent! You've mastered string interpolation in Kotlin. Now you're ready to:

1. **Learn control flow** → [If Expressions](../control-flow/01-if-expressions.md)
2. **Understand loops** → [For Loops](../control-flow/03-for-loops.md)
3. **Work with functions** → [Functions Basics](../functions/01-functions-basics.md)
4. **Explore collections** → [Arrays](../collections/01-arrays.md)

## 📚 Additional Resources

- [Kotlin Strings](https://kotlinlang.org/docs/strings.html)
- [String Templates](https://kotlinlang.org/docs/strings.html#string-templates)
- [String Formatting](https://kotlinlang.org/docs/strings.html#string-templates)

## 🏆 Summary

- ✅ You can use string interpolation with the `$` symbol
- ✅ You can embed variables and expressions in strings
- ✅ You understand when to use `${}` vs `$`
- ✅ You can create dynamic and readable string output
- ✅ You know the best practices for string interpolation!

**Keep practicing and happy coding! 🎉**
