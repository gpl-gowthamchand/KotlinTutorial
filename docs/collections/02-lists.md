# 📚 Lists in Kotlin

Lists are one of the most commonly used collection types in Kotlin. Unlike arrays, lists can grow or shrink dynamically and provide many useful methods for manipulation.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create and initialize lists in different ways
- ✅ Understand the difference between immutable and mutable lists
- ✅ Add, remove, and modify list elements
- ✅ Use list methods for searching, filtering, and transformation
- ✅ Work with list indices and ranges

## 🔍 What You'll Learn

- **List creation** - Different ways to create lists
- **Immutability vs Mutability** - Understanding `List` vs `MutableList`
- **Element manipulation** - Adding, removing, and updating elements
- **List methods** - Built-in functions for list operations
- **Functional operations** - Using lambdas with lists

## 📝 Prerequisites

- Understanding of [Arrays](01-arrays.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Control Flow](../control-flow/01-if-expressions.md)

## 💻 The Code

Let's examine the lists example:

**📁 File:** [41_list.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/41_list.kt)

## 🔍 Code Breakdown

### **1. List Creation**

#### **Immutable Lists with `listOf()`**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val names = listOf("Alice", "Bob", "Charlie")
val empty = listOf<Int>()  // Empty list with explicit type
```

#### **Mutable Lists with `mutableListOf()`**
```kotlin
val mutableNumbers = mutableListOf(1, 2, 3, 4, 5)
val mutableNames = mutableListOf("Alice", "Bob", "Charlie")
```

#### **Using `List()` Constructor**
```kotlin
val squares = List(5) { i -> i * i }  // [0, 1, 4, 9, 16]
val repeated = List(3) { "Hello" }    // ["Hello", "Hello", "Hello"]
```

### **2. Accessing List Elements**

#### **Index-based Access**
```kotlin
val numbers = listOf(10, 20, 30, 40, 50)
val first = numbers[0]      // 10
val third = numbers[2]      // 30
val last = numbers.last()   // 50
```

#### **Safe Access Methods**
```kotlin
val numbers = listOf(10, 20, 30, 40, 50)
val element = numbers.getOrNull(10)  // null (safe access)
val elementWithDefault = numbers.getOrElse(10) { -1 }  // -1 (default value)
```

### **3. Modifying Mutable Lists**

#### **Adding Elements**
```kotlin
val numbers = mutableListOf(1, 2, 3)
numbers.add(4)              // Add to end
numbers.add(0, 0)           // Add at specific index
numbers.addAll(listOf(5, 6)) // Add multiple elements
```

#### **Removing Elements**
```kotlin
val numbers = mutableListOf(1, 2, 3, 4, 5)
numbers.remove(3)           // Remove by value
numbers.removeAt(1)         // Remove by index
numbers.removeAll { it % 2 == 0 }  // Remove all even numbers
```

#### **Updating Elements**
```kotlin
val numbers = mutableListOf(1, 2, 3, 4, 5)
numbers[0] = 100            // Direct assignment
numbers.set(1, 200)         // Using set() method
```

### **4. List Properties**

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
println("Size: ${numbers.size}")           // 5
println("Is empty: ${numbers.isEmpty()}")   // false
println("Is not empty: ${numbers.isNotEmpty()}") // true
println("First element: ${numbers.first()}")     // 1
println("Last element: ${numbers.last()}")       // 5
```

### **5. Iterating Through Lists**

#### **Using for loop with indices**
```kotlin
val numbers = listOf(10, 20, 30, 40, 50)
for (i in numbers.indices) {
    println("Index $i: ${numbers[i]}")
}
```

#### **Using for-each loop**
```kotlin
val numbers = listOf(10, 20, 30, 40, 50)
for (number in numbers) {
    println("Number: $number")
}
```

#### **Using forEach function**
```kotlin
val numbers = listOf(10, 20, 30, 40, 50)
numbers.forEach { number ->
    println("Number: $number")
}
```

#### **Using forEachIndexed**
```kotlin
val numbers = listOf(10, 20, 30, 40, 50)
numbers.forEachIndexed { index, number ->
    println("Index $index: $number")
}
```

### **6. List Searching and Filtering**

#### **Finding Elements**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
val firstEven = numbers.find { it % 2 == 0 }        // 2
val lastEven = numbers.findLast { it % 2 == 0 }     // 10
val hasEven = numbers.any { it % 2 == 0 }           // true
val allEven = numbers.all { it % 2 == 0 }           // false
```

#### **Filtering Elements**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
val evenNumbers = numbers.filter { it % 2 == 0 }    // [2, 4, 6, 8, 10]
val oddNumbers = numbers.filterNot { it % 2 == 0 }  // [1, 3, 5, 7, 9]
val firstThree = numbers.take(3)                    // [1, 2, 3]
val lastThree = numbers.takeLast(3)                 // [8, 9, 10]
```

### **7. List Transformation**

#### **Mapping Elements**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val doubled = numbers.map { it * 2 }                // [2, 4, 6, 8, 10]
val squared = numbers.map { it * it }               // [1, 4, 9, 16, 25]
val withIndex = numbers.mapIndexed { index, value -> "$index: $value" }
```

#### **Flattening Lists**
```kotlin
val listOfLists = listOf(
    listOf(1, 2, 3),
    listOf(4, 5, 6),
    listOf(7, 8, 9)
)
val flattened = listOfLists.flatten()  // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 🎯 Key Concepts Explained

### **1. Immutable vs Mutable Lists**
```kotlin
// Immutable List - cannot be modified
val immutableList = listOf(1, 2, 3)
// immutableList.add(4)  // ❌ Compilation error

// Mutable List - can be modified
val mutableList = mutableListOf(1, 2, 3)
mutableList.add(4)  // ✅ Can modify
```

### **2. List vs Array**
```kotlin
// Array - fixed size, mutable
val array = arrayOf(1, 2, 3)
array[0] = 10  // ✅ Can modify

// List - dynamic size, immutable by default
val list = listOf(1, 2, 3)
// list[0] = 10  // ❌ Compilation error

// MutableList - dynamic size, mutable
val mutableList = mutableListOf(1, 2, 3)
mutableList[0] = 10  // ✅ Can modify
```

### **3. List Performance Characteristics**
- **Access by index**: O(1) - very fast
- **Search by value**: O(n) - linear time
- **Add/Remove at end**: O(1) - very fast
- **Add/Remove at beginning/middle**: O(n) - slower

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/41_list.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '41_listKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: List Manipulation**
Create a mutable list of fruits and perform various operations.

**Solution:**
```kotlin
fun main() {
    val fruits = mutableListOf("Apple", "Banana", "Orange")
    println("Original: $fruits")
    
    fruits.add("Grape")
    fruits.add(0, "Strawberry")
    fruits.remove("Banana")
    
    println("Modified: $fruits")
    println("Size: ${fruits.size}")
}
```

### **Exercise 2: List Filtering and Mapping**
Create a list of numbers and perform filtering and mapping operations.

**Solution:**
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    val evenSquares = numbers
        .filter { it % 2 == 0 }
        .map { it * it }
    
    println("Original: $numbers")
    println("Even squares: $evenSquares")
    println("Sum of even squares: ${evenSquares.sum()}")
}
```

### **Exercise 3: List Statistics**
Calculate various statistics for a list of numbers.

**Solution:**
```kotlin
fun analyzeList(numbers: List<Int>) {
    val count = numbers.size
    val sum = numbers.sum()
    val average = sum.toDouble() / count
    val min = numbers.minOrNull() ?: 0
    val max = numbers.maxOrNull() ?: 0
    val evenCount = numbers.count { it % 2 == 0 }
    val oddCount = numbers.count { it % 2 != 0 }
    
    println("Count: $count")
    println("Sum: $sum")
    println("Average: $average")
    println("Min: $min, Max: $max")
    println("Even: $evenCount, Odd: $oddCount")
}

fun main() {
    val numbers = listOf(23, 45, 12, 67, 34, 89, 56, 78)
    analyzeList(numbers)
}
```

### **Exercise 4: List Transformation**
Transform a list of strings in various ways.

**Solution:**
```kotlin
fun main() {
    val words = listOf("hello", "world", "kotlin", "programming", "language")
    
    val capitalized = words.map { it.capitalize() }
    val longWords = words.filter { it.length > 5 }
    val wordLengths = words.map { it.length }
    val totalLength = wordLengths.sum()
    
    println("Original: $words")
    println("Capitalized: $capitalized")
    println("Long words: $longWords")
    println("Word lengths: $wordLengths")
    println("Total length: $totalLength")
}
```

## 🚨 Common Mistakes to Avoid

1. **Modifying immutable lists**: `listOf(1, 2, 3).add(4)` ❌
   - **Correct**: Use `mutableListOf()` for mutable lists ✅

2. **Index out of bounds**: `list[list.size]` ❌
   - **Correct**: Use `list.lastIndex` or check bounds ✅

3. **Forgetting list is immutable by default**: Always check if you need `mutableListOf()` ✅

4. **Inefficient operations**: `list.removeAt(0)` for large lists ❌
   - **Better**: Use `LinkedList` for frequent insertions/removals ✅

## 🎯 What's Next?

Now that you understand lists, continue with:

1. **Maps** → [Maps and HashMaps](03-maps.md)
2. **Sets** → [Sets and HashSets](04-sets.md)
3. **Functional operations** → [Filter, Map, and Sorting](05-filter-map-sorting.md)
4. **Advanced collections** → [Collections Overview](../README.md#collections)

## 📚 Additional Resources

- [Official Kotlin Lists Documentation](https://kotlinlang.org/docs/collections-overview.html#list)
- [Kotlin Collections API](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)
- [List Methods Reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/)

## 🏆 Summary

- ✅ You can create both immutable and mutable lists
- ✅ You understand how to add, remove, and modify elements
- ✅ You know list properties and iteration methods
- ✅ You can use functional operations like filter, map, and find
- ✅ You're ready to work with more complex collections!

**Lists are powerful and flexible collections in Kotlin. Use them wisely! 🎉**
