# 🔧 Extension Functions in Kotlin

Welcome to the powerful world of extension functions! Extension functions allow you to add new functionality to existing classes without modifying their source code. This is one of Kotlin's most powerful features, enabling you to write more expressive and readable code.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create extension functions for existing classes
- ✅ Understand how extension functions work
- ✅ Use extension functions to enhance readability
- ✅ Apply extension functions to different data types
- ✅ Write more expressive and maintainable code

## 🔍 What You'll Learn

- **Extension function syntax** - How to define and use them
- **Receiver types** - Understanding the `this` context
- **Scope and visibility** - Where extension functions can be used
- **Best practices** - When and how to use extension functions
- **Real-world applications** - Practical use cases

## 📝 Prerequisites

- Basic understanding of functions
- Completed [Named Parameters](03-named-parameters.md) lesson
- Knowledge of classes and objects

## 💻 The Code

Let's examine the extension functions examples:

```kotlin
// Example 1: Extension function on custom class
fun Studentt.isScholar(marks: Int): Boolean {
    return marks > 95
}

class Studentt {
    fun hasPassed(marks: Int): Boolean {
        return marks > 40
    }
}

// Example 2: Extension functions on built-in types
fun String.add(s1: String, s2: String): String {
    return this + s1 + s2
}

fun Int.greaterValue(other: Int): Int {
    if (this > other)
        return this
    else
        return other
}
```

**📁 Files:** 
- [22_extension_function_one.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/22_extension_function_one.kt)
- [23_extension_function_two.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/23_extension_function_two.kt)

## 🔍 Code Breakdown

### **Extension Function on Custom Class**

```kotlin
fun Studentt.isScholar(marks: Int): Boolean {
    return marks > 95
}
```

- **`fun Studentt.isScholar`**: Extension function declaration
- **`Studentt`**: Receiver type (the class being extended)
- **`isScholar`**: Function name
- **`marks: Int`**: Parameter
- **`Boolean`**: Return type

### **Extension Function on Built-in Types**

```kotlin
fun String.add(s1: String, s2: String): String {
    return this + s1 + s2
}
```

- **`fun String.add`**: Extension function on String class
- **`this`**: Refers to the String instance being extended
- **`s1 + s2`**: Concatenates additional strings

## 🎯 Key Concepts Explained

### **1. Extension Function Syntax**

#### **Basic Syntax**

```kotlin
fun ReceiverType.functionName(parameters): ReturnType {
    // Function body
    // 'this' refers to the receiver object
}
```

**Components:**
- **`fun`**: Function keyword
- **`ReceiverType`**: The type being extended
- **`.`**: Dot separator
- **`functionName`**: Name of the extension function
- **`parameters`**: Function parameters (optional)
- **`ReturnType`**: Return type of the function

#### **Example with Different Types**

```kotlin
// Extension on Int
fun Int.isEven(): Boolean = this % 2 == 0

// Extension on String
fun String.capitalizeFirst(): String = 
    if (isNotEmpty()) this[0].uppercase() + substring(1) else this

// Extension on List<Int>
fun List<Int>.sumOfEvens(): Int = 
    filter { it % 2 == 0 }.sum()

// Extension on nullable types
fun String?.orEmpty(): String = this ?: ""
```

### **2. How Extension Functions Work**

#### **The `this` Context**

```kotlin
fun String.repeat(times: Int): String {
    var result = ""
    repeat(times) {
        result += this  // 'this' refers to the String instance
    }
    return result
}

// Usage
val result = "Hello".repeat(3)  // "HelloHelloHello"
```

**Key Points:**
- **`this`** refers to the receiver object
- Extension functions are **static** under the hood
- They don't modify the original class
- They're resolved **statically** at compile time

#### **Extension vs Member Functions**

```kotlin
class Person(val name: String) {
    // Member function
    fun greet(): String = "Hello, I'm $name"
}

// Extension function
fun Person.formalGreet(): String = "Good day, my name is $name"

// Usage
val person = Person("John")
println(person.greet())        // "Hello, I'm John"
println(person.formalGreet())  // "Good day, my name is John"
```

### **3. Extension Function Scope and Visibility**

#### **Top-level Extensions**

```kotlin
// File: StringExtensions.kt
fun String.reverse(): String = this.reversed()

fun String.isPalindrome(): Boolean = this == this.reversed()

// Can be used anywhere the file is imported
```

#### **Local Extensions**

```kotlin
fun main() {
    // Local extension function
    fun String.shout(): String = this.uppercase() + "!"
    
    val message = "hello"
    println(message.shout())  // "HELLO!"
}

// This extension is only available within main()
```

#### **Member Extensions**

```kotlin
class StringProcessor {
    fun String.process(): String = this.trim().uppercase()
    
    fun processText(text: String): String {
        return text.process()  // Can use the extension
    }
}

// Usage
val processor = StringProcessor()
val result = processor.processText("  hello world  ")  // "HELLO WORLD"
```

## 🧪 Hands-On Exercises

### **Exercise 1: Basic Extension Functions**
Create extension functions for common operations:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create these extension functions
    // 1. Int.isPositive()
    // 2. String.isEmail()
    // 3. List<Int>.average()
}
```

**Solution:**
```kotlin
// Extension function to check if Int is positive
fun Int.isPositive(): Boolean = this > 0

// Extension function to check if String is valid email (simplified)
fun String.isEmail(): Boolean = 
    this.contains("@") && this.contains(".") && this.length > 5

// Extension function to calculate average of List<Int>
fun List<Int>.average(): Double = 
    if (isEmpty()) 0.0 else sum().toDouble() / size

fun main(args: Array<String>) {
    val number = 42
    println("Is $number positive? ${number.isPositive()}")
    
    val email = "user@example.com"
    println("Is '$email' a valid email? ${email.isEmail()}")
    
    val numbers = listOf(1, 2, 3, 4, 5)
    println("Average of $numbers is ${numbers.average()}")
}
```

### **Exercise 2: String Extensions**
Create useful string extension functions:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create these string extension functions
    // 1. String.toTitleCase()
    // 2. String.wordCount()
    // 3. String.truncate(maxLength: Int)
}
```

**Solution:**
```kotlin
// Convert string to title case
fun String.toTitleCase(): String = 
    split(" ").joinToString(" ") { word ->
        if (word.isNotEmpty()) word[0].uppercase() + word.substring(1).lowercase() else word
    }

// Count words in string
fun String.wordCount(): Int = 
    if (trim().isEmpty()) 0 else trim().split("\\s+".toRegex()).size

// Truncate string to specified length
fun String.truncate(maxLength: Int): String = 
    if (length <= maxLength) this else substring(0, maxLength) + "..."

fun main(args: Array<String>) {
    val text = "hello world example"
    println("Original: '$text'")
    println("Title case: '${text.toTitleCase()}'")
    println("Word count: ${text.wordCount()}")
    println("Truncated (10): '${text.truncate(10)}'")
}
```

### **Exercise 3: Collection Extensions**
Create extension functions for collections:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create these collection extension functions
    // 1. List<T>.second()
    // 2. List<Int>.product()
    // 3. List<String>.longest()
}
```

**Solution:**
```kotlin
// Get second element safely
fun <T> List<T>.second(): T? = if (size >= 2) this[1] else null

// Calculate product of all integers
fun List<Int>.product(): Long = 
    if (isEmpty()) 0L else fold(1L) { acc, num -> acc * num }

// Find longest string
fun List<String>.longest(): String? = 
    maxByOrNull { it.length }

fun main(args: Array<String>) {
    val numbers = listOf(1, 2, 3, 4, 5)
    println("Second element: ${numbers.second()}")
    println("Product: ${numbers.product()}")
    
    val words = listOf("apple", "banana", "cherry", "date")
    println("Longest word: ${words.longest()}")
}
```

### **Exercise 4: Custom Class Extensions**
Create extension functions for a custom class:

```kotlin
fun main(args: Array<String>) {
    // TODO: Create a Rectangle class and extension functions
    // 1. Rectangle.area()
    // 2. Rectangle.isSquare()
    // 3. Rectangle.scale(factor: Double)
}
```

**Solution:**
```kotlin
data class Rectangle(val width: Double, val height: Double)

// Extension function to calculate area
fun Rectangle.area(): Double = width * height

// Extension function to check if rectangle is square
fun Rectangle.isSquare(): Boolean = width == height

// Extension function to scale rectangle
fun Rectangle.scale(factor: Double): Rectangle = 
    Rectangle(width * factor, height * factor)

fun main(args: Array<String>) {
    val rect = Rectangle(5.0, 3.0)
    println("Rectangle: $rect")
    println("Area: ${rect.area()}")
    println("Is square? ${rect.isSquare()}")
    
    val scaled = rect.scale(2.0)
    println("Scaled (2x): $scaled")
    println("New area: ${scaled.area()}")
}
```

## 🔍 Advanced Extension Function Patterns

### **1. Nullable Type Extensions**

```kotlin
// Safe string operations
fun String?.orEmpty(): String = this ?: ""
fun String?.isNullOrBlank(): Boolean = this?.isBlank() ?: true

// Safe number operations
fun Int?.orZero(): Int = this ?: 0
fun Double?.orDefault(default: Double): Double = this ?: default

// Usage
val nullableString: String? = null
val safeString = nullableString.orEmpty()  // ""
val length = nullableString?.length ?: 0   // 0
```

### **2. Generic Extensions**

```kotlin
// Generic list extensions
fun <T> List<T>.secondOrNull(): T? = if (size >= 2) this[1] else null
fun <T> List<T>.lastOrNull(): T? = if (isNotEmpty()) last() else null

// Generic comparison extensions
fun <T : Comparable<T>> T.isBetween(min: T, max: T): Boolean = 
    this in min..max

// Usage
val numbers = listOf(1, 2, 3, 4, 5)
val second = numbers.secondOrNull()  // 2
val last = numbers.lastOrNull()      // 5

val value = 42
val inRange = value.isBetween(0, 100)  // true
```

### **3. Infix Extension Functions**

```kotlin
// Infix extension for range checking
infix fun Int.inRange(range: IntRange): Boolean = this in range

// Infix extension for string concatenation
infix fun String.concat(other: String): String = this + other

// Usage
val age = 25
val isAdult = age inRange 18..65  // true

val greeting = "Hello" concat " World"  // "Hello World"
```

### **4. Extension Properties**

```kotlin
// Extension properties
val String.isEmail: Boolean
    get() = contains("@") && contains(".") && length > 5

val String.isPalindrome: Boolean
    get() = this == reversed()

val List<Int>.sum: Int
    get() = fold(0) { acc, num -> acc + num }

// Usage
val email = "user@example.com"
println("Is email? ${email.isEmail}")

val text = "racecar"
println("Is palindrome? ${text.isPalindrome}")

val numbers = listOf(1, 2, 3, 4, 5)
println("Sum: ${numbers.sum}")
```

## 🔍 When to Use Extension Functions

### **✅ Perfect for Extension Functions:**

1. **Utility functions**:
   ```kotlin
   fun String.capitalizeFirst() = 
       if (isNotEmpty()) this[0].uppercase() + substring(1) else this
   ```

2. **Domain-specific operations**:
   ```kotlin
   fun LocalDate.isWeekend(): Boolean = 
       dayOfWeek in listOf(DayOfWeek.SATURDAY, DayOfWeek.SUNDAY)
   ```

3. **Readability improvements**:
   ```kotlin
   fun List<Person>.adults(): List<Person> = 
       filter { it.age >= 18 }
   ```

### **❌ Avoid Extension Functions When:**

1. **Modifying internal state**:
   ```kotlin
   // ❌ Don't do this - modifies internal state
   fun MutableList<Int>.addOne() {
       for (i in indices) this[i] += 1
   }
   ```

2. **Breaking encapsulation**:
   ```kotlin
   // ❌ Don't do this - breaks encapsulation
   fun Person.setPassword(password: String) {
       this.password = password  // Assuming password is private
   }
   ```

3. **Overriding existing functionality**:
   ```kotlin
   // ❌ Don't do this - confusing
   fun String.length(): Int = this.count()  // Overrides existing length property
   ```

## 🚨 Common Mistakes to Avoid

### **1. Confusing Extension with Member Functions**

```kotlin
class Person(val name: String) {
    fun greet() = "Hello, $name"  // Member function
}

fun Person.formalGreet() = "Good day, $name"  // Extension function

// ❌ Don't expect extension to override member
val person = Person("John")
person.greet()        // Calls member function
person.formalGreet()  // Calls extension function
```

### **2. Extension Function Resolution**

```kotlin
// Extension functions are resolved statically
open class Animal
class Dog : Animal()

fun Animal.speak() = "Animal sound"
fun Dog.speak() = "Woof!"

fun Animal.makeSound() = speak()  // Always calls Animal.speak()

// Usage
val dog: Animal = Dog()
dog.makeSound()  // "Animal sound" (not "Woof!")
```

### **3. Nullable Extensions**

```kotlin
// ❌ This won't work as expected
fun String?.safeLength(): Int = this?.length ?: 0

// ✅ Better approach
fun String?.safeLength(): Int = this?.length ?: 0
fun String?.orEmpty(): String = this ?: ""

// Usage
val nullableString: String? = null
val length = nullableString.safeLength()  // 0
val text = nullableString.orEmpty()      // ""
```

## 🔍 Best Practices

### **✅ Do's**

1. **Use descriptive names**:
   ```kotlin
   // ✅ Clear and descriptive
   fun String.capitalizeFirst(): String = ...
   fun List<Int>.sumOfEvens(): Int = ...
   
   // ❌ Unclear names
   fun String.cap(): String = ...
   fun List<Int>.sum(): Int = ...
   ```

2. **Keep extensions focused**:
   ```kotlin
   // ✅ Single responsibility
   fun String.isValidEmail(): Boolean = ...
   fun String.formatAsPhone(): String = ...
   
   // ❌ Too many responsibilities
   fun String.process(): String = ...  // What does it process?
   ```

3. **Use extension functions for utilities**:
   ```kotlin
   // ✅ Good for utility functions
   fun String.reverse(): String = this.reversed()
   fun Int.isEven(): Boolean = this % 2 == 0
   ```

### **❌ Don'ts**

1. **Don't abuse extension functions**:
   ```kotlin
   // ❌ Don't create extensions for everything
   fun String.hello(): String = "Hello, $this"
   fun Int.addOne(): Int = this + 1
   ```

2. **Don't create confusing extensions**:
   ```kotlin
   // ❌ Confusing - what does it do?
   fun String.process(): String = this.trim().uppercase().replace(" ", "_")
   
   // ✅ Clear and focused
   fun String.toSnakeCase(): String = this.trim().uppercase().replace(" ", "_")
   ```

## 🎯 What's Next?

Excellent! You've mastered extension functions in Kotlin. Now you're ready to:

1. **Understand infix functions** → [Infix Functions](05-infix-functions.md)
2. **Master tailrec functions** → [Tailrec Functions](06-tailrec-functions.md)
3. **Learn about lambdas** → [Lambdas](../functional-programming/01-lambdas.md)
4. **Explore collections** → [Arrays](../collections/01-arrays.md)

## 📚 Additional Resources

- [Kotlin Extension Functions](https://kotlinlang.org/docs/extensions.html)
- [Extension Functions](https://kotlinlang.org/docs/extensions.html#extension-functions)
- [Extension Properties](https://kotlinlang.org/docs/extensions.html#extension-properties)

## 🏆 Summary

- ✅ You can create extension functions for existing classes
- ✅ You understand how extension functions work
- ✅ You can use extension functions to enhance readability
- ✅ You can apply extension functions to different data types
- ✅ You can write more expressive and maintainable code
- ✅ You're ready to extend any class with new functionality!

**Keep practicing and happy coding! 🎉**

