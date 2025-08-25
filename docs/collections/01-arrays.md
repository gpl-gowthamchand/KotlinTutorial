# 📚 Arrays in Kotlin

Arrays are one of the fundamental collection types in Kotlin. They store multiple values of the same type in a fixed-size, ordered collection.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create and initialize arrays in different ways
- ✅ Access and modify array elements
- ✅ Use array properties and methods
- ✅ Understand array limitations and when to use them
- ✅ Work with different data types in arrays

## 🔍 What You'll Learn

- **Array creation** - Different ways to create arrays
- **Element access** - How to read and write array elements
- **Array properties** - Size, indices, and other useful properties
- **Array methods** - Built-in functions for array manipulation
- **Type safety** - How Kotlin ensures type consistency

## 📝 Prerequisites

- Basic understanding of [variables and data types](../basics/02-variables-data-types.md)
- Knowledge of [control flow](../control-flow/01-if-expressions.md)
- Familiarity with [functions](../functions/01-functions-basics.md)

## 💻 The Code

Let's examine the arrays example:

**📁 File:** [40_arrays.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/40_arrays.kt)

## 🔍 Code Breakdown

### **1. Array Creation**

#### **Using `arrayOf()`**
```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
val names = arrayOf("Alice", "Bob", "Charlie")
val mixed = arrayOf(1, "Hello", 3.14, true)
```

#### **Using `Array()` Constructor**
```kotlin
val squares = Array(5) { i -> i * i }  // [0, 1, 4, 9, 16]
val zeros = Array(3) { 0 }             // [0, 0, 0]
```

#### **Type-Specific Arrays**
```kotlin
val intArray = intArrayOf(1, 2, 3, 4, 5)
val doubleArray = doubleArrayOf(1.1, 2.2, 3.3)
val charArray = charArrayOf('a', 'b', 'c')
```

### **2. Accessing Array Elements**

#### **Index-based Access**
```kotlin
val numbers = arrayOf(10, 20, 30, 40, 50)
val first = numbers[0]      // 10
val third = numbers[2]      // 30
val last = numbers[4]       // 50
```

#### **Safe Access with `get()`**
```kotlin
val numbers = arrayOf(10, 20, 30, 40, 50)
val element = numbers.get(2)  // 30
```

### **3. Modifying Array Elements**

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
numbers[0] = 100        // Direct assignment
numbers.set(1, 200)     // Using set() method
// Result: [100, 200, 3, 4, 5]
```

### **4. Array Properties**

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
println("Size: ${numbers.size}")           // 5
println("Indices: ${numbers.indices}")     // 0..4
println("Last index: ${numbers.lastIndex}") // 4
```

### **5. Iterating Through Arrays**

#### **Using for loop with indices**
```kotlin
val numbers = arrayOf(10, 20, 30, 40, 50)
for (i in numbers.indices) {
    println("Index $i: ${numbers[i]}")
}
```

#### **Using for-each loop**
```kotlin
val numbers = arrayOf(10, 20, 30, 40, 50)
for (number in numbers) {
    println("Number: $number")
}
```

#### **Using forEach function**
```kotlin
val numbers = arrayOf(10, 20, 30, 40, 50)
numbers.forEach { number ->
    println("Number: $number")
}
```

## 🎯 Key Concepts Explained

### **1. Array Characteristics**
- **Fixed Size**: Once created, array size cannot change
- **Ordered**: Elements maintain their position
- **Indexed**: Access elements using zero-based indices
- **Type Consistent**: All elements must be of the same type

### **2. Array vs List**
```kotlin
// Array - fixed size, mutable
val array = arrayOf(1, 2, 3)
array[0] = 10  // ✅ Can modify

// List - dynamic size, immutable by default
val list = listOf(1, 2, 3)
// list[0] = 10  // ❌ Compilation error
```

### **3. Array Bounds**
```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
// Valid indices: 0, 1, 2, 3, 4
// numbers[5]  // ❌ ArrayIndexOutOfBoundsException
// numbers[-1] // ❌ ArrayIndexOutOfBoundsException
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/40_arrays.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '40_arraysKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Create and Modify Arrays**
Create an array of your favorite colors and change the second color.

**Solution:**
```kotlin
fun main() {
    val colors = arrayOf("Red", "Blue", "Green", "Yellow")
    println("Original: ${colors.joinToString()}")
    
    colors[1] = "Purple"
    println("Modified: ${colors.joinToString()}")
}
```

### **Exercise 2: Find Maximum Value**
Write a function to find the maximum value in an array of numbers.

**Solution:**
```kotlin
fun findMax(numbers: Array<Int>): Int {
    var max = numbers[0]
    for (i in 1 until numbers.size) {
        if (numbers[i] > max) {
            max = numbers[i]
        }
    }
    return max
}

fun main() {
    val numbers = arrayOf(23, 45, 12, 67, 34)
    println("Maximum: ${findMax(numbers)}")
}
```

### **Exercise 3: Reverse Array**
Create a function to reverse the elements of an array.

**Solution:**
```kotlin
fun reverseArray(numbers: Array<Int>): Array<Int> {
    val reversed = Array(numbers.size) { 0 }
    for (i in numbers.indices) {
        reversed[i] = numbers[numbers.lastIndex - i]
    }
    return reversed
}

fun main() {
    val numbers = arrayOf(1, 2, 3, 4, 5)
    val reversed = reverseArray(numbers)
    println("Original: ${numbers.joinToString()}")
    println("Reversed: ${reversed.joinToString()}")
}
```

### **Exercise 4: Array Statistics**
Calculate the sum, average, and count of even numbers in an array.

**Solution:**
```kotlin
fun analyzeArray(numbers: Array<Int>) {
    val sum = numbers.sum()
    val average = sum.toDouble() / numbers.size
    val evenCount = numbers.count { it % 2 == 0 }
    
    println("Sum: $sum")
    println("Average: $average")
    println("Even numbers: $evenCount")
}

fun main() {
    val numbers = arrayOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    analyzeArray(numbers)
}
```

## 🚨 Common Mistakes to Avoid

1. **Array bounds error**: `array[array.size]` ❌
   - **Correct**: `array[array.lastIndex]` ✅

2. **Type mismatch**: `arrayOf(1, "hello", 3.14)` ❌
   - **Correct**: Use specific types or `Array<Any>` ✅

3. **Modifying immutable arrays**: `arrayOf(1, 2, 3)[0] = 10` ❌
   - **Correct**: Store in variable first ✅

4. **Forgetting zero-based indexing**: `array[1]` is second element ✅

## 🎯 What's Next?

Now that you understand arrays, continue with:

1. **Lists** → [Lists and Collections](02-lists.md)
2. **Maps** → [Maps and HashMaps](03-maps.md)
3. **Sets** → [Sets and HashSets](04-sets.md)
4. **Functional operations** → [Filter, Map, and Sorting](05-filter-map-sorting.md)

## 📚 Additional Resources

- [Official Kotlin Arrays Documentation](https://kotlinlang.org/docs/arrays.html)
- [Kotlin Collections Overview](https://kotlinlang.org/docs/collections-overview.html)
- [Array Methods Reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/)

## 🏆 Summary

- ✅ You can create arrays using different methods
- ✅ You understand how to access and modify elements
- ✅ You know array properties and iteration methods
- ✅ You're ready to work with more complex collections!

**Arrays are the foundation of collections in Kotlin. Master them well! 🎉**
