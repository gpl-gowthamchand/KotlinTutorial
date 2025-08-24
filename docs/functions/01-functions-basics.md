# ⚙️ Functions Basics in Kotlin

Welcome to the world of functions! Functions are the building blocks of reusable code in Kotlin. They allow you to organize your code into logical, reusable pieces.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Declare and call functions in Kotlin
- ✅ Understand function parameters and return types
- ✅ Create functions that perform specific tasks
- ✅ Call functions from the main function
- ✅ Understand basic function syntax and structure

## 🔍 What You'll Learn

- **Function declaration** - How to create functions in Kotlin
- **Parameters** - Input values that functions can receive
- **Return types** - The type of value the function returns
- **Function calls** - How to execute a function
- **Code organization** - How to structure your programs

## 📝 Prerequisites

- Basic understanding of variables and data types
- Completed [Variables and Data Types](../basics/02-variables-data-types.md) lesson

## 💻 The Code

Let's examine the functions basics example:

```kotlin
fun main(args: Array<String>) {
    // Calling the add function with two integer parameters
    val sum = add(2, 4)
    println("Sum is $sum")
    
    // You can call functions multiple times with different values
    val anotherSum = add(10, 20)
    println("Another sum is $anotherSum")
    
    // Functions can be called in expressions
    val total = add(5, 3) + add(1, 2)
    println("Total of multiple additions: $total")
}

/**
 * Adds two integers and returns their sum
 * 
 * @param a The first integer to add
 * @param b The second integer to add
 * @return The sum of a and b
 * 
 * This is a simple function that demonstrates:
 * - Parameter declaration
 * - Return type specification
 * - Basic arithmetic operations
 * - Return statement usage
 */
fun add(a: Int, b: Int): Int {
    return a + b
}
```

**📁 File:** [17_functions_basics.kt](src/17_functions_basics.kt)

## 🔍 Code Breakdown

### **Main Function**

```kotlin
fun main(args: Array<String>) {
    // Function calls and logic here
}
```

- **Entry point** of the program
- **Calls other functions** to perform tasks
- **Demonstrates** how functions work together

### **Function Declaration**

```kotlin
fun add(a: Int, b: Int): Int {
    return a + b
}
```

- **`fun`**: Keyword to declare a function
- **`add`**: Function name (descriptive and meaningful)
- **`(a: Int, b: Int)`**: Parameter list
  - `a: Int` - First parameter named `a` of type `Int`
  - `b: Int` - Second parameter named `b` of type `Int`
- **`: Int`**: Return type (function returns an integer)
- **`{ return a + b }`**: Function body with return statement

### **Function Calls**

```kotlin
val sum = add(2, 4)
val anotherSum = add(10, 20)
val total = add(5, 3) + add(1, 2)
```

- **`add(2, 4)`**: Calls the function with arguments `2` and `4`
- **Arguments**: The actual values passed to the function
- **Return value**: The result is stored in variables

## 🎯 Key Concepts Explained

### **1. Function Declaration Syntax**

```kotlin
fun functionName(parameter1: Type1, parameter2: Type2): ReturnType {
    // Function body
    return result
}
```

**Components:**
- **`fun`**: Function keyword
- **`functionName`**: Descriptive name (use camelCase)
- **`(parameters)`**: Input values the function needs
- **`: ReturnType`**: Type of value the function returns
- **`{ }`**: Function body containing the logic
- **`return`**: Statement that sends back the result

### **2. Parameters vs Arguments**

```kotlin
// Function declaration (parameters)
fun greet(name: String, age: Int): String {
    return "Hello $name, you are $age years old"
}

// Function call (arguments)
val message = greet("Alice", 25)
```

- **Parameters**: Variables declared in the function signature
- **Arguments**: Actual values passed when calling the function

### **3. Return Types**

```kotlin
fun noReturn(): Unit {        // Unit is default, can be omitted
    println("Hello")
}

fun returnString(): String {
    return "Hello"
}

fun returnNumber(): Int {
    return 42
}

fun returnBoolean(): Boolean {
    return true
}
```

- **`Unit`**: No return value (like `void` in other languages)
- **`String`**: Returns text
- **`Int`**: Returns a number
- **`Boolean`**: Returns true/false

## 🧪 Hands-On Exercises

### **Exercise 1: Create a Multiply Function**
Create a function that multiplies two numbers and returns the result.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val result = multiply(5, 3)
    println("5 * 3 = $result")
}

fun multiply(a: Int, b: Int): Int {
    return a * b
}
```

### **Exercise 2: Create a Greet Function**
Create a function that takes a name and returns a greeting message.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val message = greet("John")
    println(message)
}

fun greet(name: String): String {
    return "Hello, $name! Welcome to Kotlin!"
}
```

### **Exercise 3: Create an isEven Function**
Create a function that checks if a number is even and returns true/false.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    println("Is 4 even? ${isEven(4)}")
    println("Is 7 even? ${isEven(7)}")
}

fun isEven(number: Int): Boolean {
    return number % 2 == 0
}
```

### **Exercise 4: Create a calculateArea Function**
Create a function that calculates the area of a rectangle.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    val area = calculateArea(5.0, 3.0)
    println("Area of rectangle: $area")
}

fun calculateArea(length: Double, width: Double): Double {
    return length * width
}
```

## 🔍 Function Syntax Breakdown

```kotlin
fun add(a: Int, b: Int): Int {
│   │   │   │   │   │   │
│   │   │   │   │   │   └─ Function body (what the function does)
│   │   │   │   │   └───── Return type (Int in this case)
│   │   │   │   └───────── Second parameter (b of type Int)
│   │   │   └───────────── First parameter (a of type Int)
│   │   └───────────────── Function name
│   └───────────────────── Function keyword
```

## 🚨 Common Mistakes to Avoid

1. **Missing return type for non-Unit functions**:
   ```kotlin
   fun add(a: Int, b: Int) {  // ❌ Missing return type
       return a + b
   }
   
   fun add(a: Int, b: Int): Int {  // ✅ Correct
       return a + b
   }
   ```

2. **Wrong parameter types**:
   ```kotlin
   fun greet(name: String) {
       println("Hello $name")
   }
   
   greet(42)  // ❌ Wrong type, should be String
   greet("42")  // ✅ Correct
   ```

3. **Missing return statement**:
   ```kotlin
   fun getNumber(): Int {
       // ❌ Missing return statement
   }
   
   fun getNumber(): Int {
       return 42  // ✅ Correct
   }
   ```

4. **Function name conflicts**:
   ```kotlin
   fun add(a: Int, b: Int): Int { return a + b }
   fun add(a: Int, b: Int): Int { return a + b }  // ❌ Duplicate function
   ```

## 🎯 What's Next?

Excellent! You've learned the basics of functions. Now you're ready to:

1. **Learn functions as expressions** → [Functions as Expressions](02-functions-expressions.md)
2. **Explore extension functions** → [Extension Functions](03-extension-functions.md)
3. **Understand named parameters** → [Named Parameters](05-named-parameters.md)
4. **Work with classes** → [Classes and Constructors](../oop/01-classes-constructors.md)

## 📚 Additional Resources

- [Kotlin Functions Documentation](https://kotlinlang.org/docs/functions.html)
- [Function Parameters](https://kotlinlang.org/docs/functions.html#function-parameters)
- [Function Return Types](https://kotlinlang.org/docs/functions.html#function-scope)

## 🏆 Summary

- ✅ You can declare and call functions in Kotlin
- ✅ You understand function parameters and return types
- ✅ You can create functions that perform specific tasks
- ✅ You know how to organize code into reusable pieces
- ✅ You're ready to explore more advanced function concepts!

**Keep practicing and happy coding! 🎉**
