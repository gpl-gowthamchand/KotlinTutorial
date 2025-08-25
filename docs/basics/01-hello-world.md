# 🚀 Hello World - Your First Kotlin Program

Welcome to Kotlin! This is your first step into the world of Kotlin programming. Let's start with the traditional "Hello World" program.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Write your first Kotlin program
- ✅ Understand the basic structure of a Kotlin application
- ✅ Use the `main` function as the entry point
- ✅ Output text to the console
- ✅ Understand basic syntax and formatting

## 🔍 What You'll Learn

- **Function declaration syntax** - How to create functions in Kotlin
- **Parameter handling** - Understanding the `main` function parameters
- **Basic output operations** - Using `print()` and `println()`
- **Kotlin code structure** - How Kotlin programs are organized

## 📝 Prerequisites

**None!** This is your starting point. You don't need any prior programming experience.

## 💻 The Code

Let's look at your first Kotlin program:

```kotlin
// Hello World App

fun main(args: Array<String>) {
    print("Hello World")
}
```

**📁 File:** [01_hello_world.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/01_hello_world.kt)

## 🔍 Code Breakdown

### **Line 1: Comment**
```kotlin
// Hello World App
```
- `//` indicates a single-line comment
- Comments are ignored by the compiler
- They help explain what your code does

### **Line 3: Main Function Declaration**
```kotlin
fun main(args: Array<String>) {
```
- `fun` - Keyword to declare a function
- `main` - Function name (this is special - it's the entry point)
- `args: Array<String>` - Parameter declaration
  - `args` - Parameter name
  - `Array<String>` - Type (array of strings)
- `{` - Opening brace for function body

### **Line 4: Function Body**
```kotlin
    print("Hello World")
```
- `print()` - Function to output text without a newline
- `"Hello World"` - String literal (text in quotes)
- `;` - Semicolon is optional in Kotlin (not needed here)

### **Line 5: Closing Brace**
```kotlin
}
```
- Closes the function body

## 🎯 Key Concepts Explained

### **1. The `main` Function**
- **Entry Point**: Every Kotlin program starts with the `main` function
- **Special Name**: The compiler looks for this specific function
- **Parameters**: `args` contains command-line arguments (we'll use these later)

### **2. Function Declaration**
```kotlin
fun functionName(parameters): returnType {
    // function body
}
```

### **3. Output Functions**
- **`print()`**: Outputs text without moving to the next line
- **`println()`**: Outputs text and moves to the next line

## 🧪 Running Your First Program

### **Step 1: Open IntelliJ IDEA**
1. Launch IntelliJ IDEA
2. Open the project folder
3. Navigate to [01_hello_world.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/01_hello_world.kt)

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '01_hello_worldKt'"
3. Or use the green play button

### **Step 3: See the Output**
```
Hello World
```

## 🎮 Hands-On Exercises

### **Exercise 1: Modify the Message**
Change "Hello World" to "Hello Kotlin!" and run the program.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    print("Hello Kotlin!")
}
```

### **Exercise 2: Use println()**
Replace `print()` with `println()` and see the difference.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    println("Hello World")
}
```

### **Exercise 3: Add Your Name**
Add another print statement with your name.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    print("Hello World")
    print("My name is [Your Name]")
}
```

### **Exercise 4: Multiple Lines**
Use multiple println statements to create a multi-line output.

**Solution:**
```kotlin
fun main(args: Array<String>) {
    println("Hello World")
    println("Welcome to Kotlin")
    println("Let's start coding!")
}
```

## 🔍 Understanding the Output

### **Using `print()`:**
```kotlin
print("Hello")
print("World")
```
**Output:** `HelloWorld` (no space, no newline)

### **Using `println()`:**
```kotlin
println("Hello")
println("World")
```
**Output:**
```
Hello
World
```

## 🚨 Common Mistakes to Avoid

1. **Missing quotes**: `print(Hello World)` ❌
   - **Correct**: `print("Hello World")` ✅

2. **Missing braces**: `fun main(args: Array<String>) print("Hello")` ❌
   - **Correct**: `fun main(args: Array<String>) { print("Hello") }` ✅

3. **Wrong function name**: `fun Main(args: Array<String>)` ❌
   - **Correct**: `fun main(args: Array<String>)` ✅

## 🎯 What's Next?

Congratulations! You've written your first Kotlin program. Now you're ready to:

1. **Learn about variables** → [Variables and Data Types](02-variables-data-types.md)
2. **Understand data types** → [Data Types Deep Dive](04-data-types.md)
3. **Explore more output** → [Exploring Your First App](../02-explore-first-app.md)

## 📚 Additional Resources

- [Official Kotlin Documentation](https://kotlinlang.org/docs/home.html)
- [Kotlin Playground](https://play.kotlinlang.org/) - Try code online
- [IntelliJ IDEA Tutorial](https://www.jetbrains.com/help/idea/creating-and-running-your-first-kotlin-application.html)

## 🏆 Summary

- ✅ You've written your first Kotlin program
- ✅ You understand the basic structure
- ✅ You can output text to the console
- ✅ You're ready to learn more!

**Keep practicing and happy coding! 🎉**
