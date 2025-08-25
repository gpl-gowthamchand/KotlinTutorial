# 📚 Sets and HashSets in Kotlin

Sets are collections that store unique elements without any specific order. They're perfect for removing duplicates, checking membership, and performing mathematical set operations like union, intersection, and difference.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create and initialize sets in different ways
- ✅ Understand the difference between immutable and mutable sets
- ✅ Add, remove, and check for elements in sets
- ✅ Use set methods for mathematical operations
- ✅ Work with set properties and iteration

## 🔍 What You'll Learn

- **Set creation** - Different ways to create sets
- **Uniqueness** - How sets ensure no duplicate elements
- **Element manipulation** - Adding, removing, and checking elements
- **Set operations** - Union, intersection, difference, and subset operations
- **Functional operations** - Using lambdas with sets

## 📝 Prerequisites

- Understanding of [Maps](03-maps.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Control Flow](../control-flow/01-if-expressions.md)

## 💻 The Code

Let's examine the sets example:

**📁 File:** [43_set_hashset.kt](../src/43_set_hashset.kt)

## 🔍 Code Breakdown

### **1. Set Creation**

#### **Immutable Sets with `setOf()`**
```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
val names = setOf("Alice", "Bob", "Charlie")
val empty = setOf<Int>()  // Empty set with explicit type
```

#### **Mutable Sets with `mutableSetOf()`**
```kotlin
val mutableNumbers = mutableSetOf(1, 2, 3, 4, 5)
val mutableNames = mutableSetOf("Alice", "Bob", "Charlie")
```

#### **Using `HashSet()` Constructor**
```kotlin
val hashSet = HashSet<String>()
hashSet.add("Alice")
hashSet.add("Bob")
```

### **2. Adding and Removing Elements**

#### **Adding Elements**
```kotlin
val names = mutableSetOf<String>()
names.add("Alice")                    // Add single element
names.addAll(listOf("Bob", "Charlie")) // Add multiple elements
names += "David"                      // Using += operator
```

#### **Removing Elements**
```kotlin
val names = mutableSetOf("Alice", "Bob", "Charlie", "David")
names.remove("Bob")                   // Remove by value
names.removeAll { it.startsWith("A") } // Remove all names starting with "A"
names.clear()                         // Remove all elements
```

### **3. Checking Set Membership**

#### **Basic Membership Tests**
```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
val hasThree = 3 in numbers           // true
val hasTen = 10 in numbers            // false
val notHasTen = 10 !in numbers        // true
```

#### **Using Methods**
```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
val containsThree = numbers.contains(3)    // true
val containsTen = numbers.contains(10)     // false
```

### **4. Set Properties**

```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
println("Size: ${numbers.size}")           // 5
println("Is empty: ${numbers.isEmpty()}")   // false
println("Is not empty: ${numbers.isNotEmpty()}") // true
```

### **5. Iterating Through Sets**

#### **Using for loop**
```kotlin
val names = setOf("Alice", "Bob", "Charlie")
for (name in names) {
    println("Name: $name")
}
```

#### **Using forEach function**
```kotlin
val names = setOf("Alice", "Bob", "Charlie")
names.forEach { name ->
    println("Name: $name")
}
```

#### **Using forEachIndexed**
```kotlin
val names = setOf("Alice", "Bob", "Charlie")
names.forEachIndexed { index, name ->
    println("Index $index: $name")
}
```

### **6. Set Mathematical Operations**

#### **Union (Combining Sets)**
```kotlin
val set1 = setOf(1, 2, 3)
val set2 = setOf(3, 4, 5)
val union = set1.union(set2)         // [1, 2, 3, 4, 5]
val unionOperator = set1 + set2      // Same result using + operator
```

#### **Intersection (Common Elements)**
```kotlin
val set1 = setOf(1, 2, 3, 4)
val set2 = setOf(3, 4, 5, 6)
val intersection = set1.intersect(set2)  // [3, 4]
```

#### **Difference (Elements in First Set but Not in Second)**
```kotlin
val set1 = setOf(1, 2, 3, 4)
val set2 = setOf(3, 4, 5, 6)
val difference = set1.subtract(set2)     // [1, 2]
```

#### **Symmetric Difference (Elements in Either Set but Not Both)**
```kotlin
val set1 = setOf(1, 2, 3, 4)
val set2 = setOf(3, 4, 5, 6)
val symmetricDiff = set1.union(set2).subtract(set1.intersect(set2))  // [1, 2, 5, 6]
```

### **7. Set Relationships**

#### **Subset and Superset**
```kotlin
val set1 = setOf(1, 2, 3)
val set2 = setOf(1, 2, 3, 4, 5)
val isSubset = set1.all { it in set2 }      // true
val isSuperset = set2.all { it in set1 }    // false
```

#### **Disjoint Sets (No Common Elements)**
```kotlin
val set1 = setOf(1, 2, 3)
val set2 = setOf(4, 5, 6)
val areDisjoint = set1.none { it in set2 }  // true
```

### **8. Set Filtering and Transformation**

#### **Filtering Elements**
```kotlin
val numbers = setOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
val evenNumbers = numbers.filter { it % 2 == 0 }    // [2, 4, 6, 8, 10]
val oddNumbers = numbers.filterNot { it % 2 == 0 }  // [1, 3, 5, 7, 9]
```

#### **Transforming Elements**
```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
val doubled = numbers.map { it * 2 }                // [2, 4, 6, 8, 10]
val squared = numbers.map { it * it }               // [1, 4, 9, 16, 25]
```

## 🎯 Key Concepts Explained

### **1. Uniqueness Guarantee**
```kotlin
val numbers = mutableSetOf(1, 2, 3, 3, 4, 4, 5)
println(numbers)  // [1, 2, 3, 4, 5] - duplicates automatically removed
```

### **2. Ordering**
```kotlin
// Sets don't guarantee order
val set1 = setOf(3, 1, 4, 1, 5, 9)
val set2 = setOf(9, 5, 1, 4, 3, 1)
println(set1 == set2)  // true - order doesn't matter for equality
```

### **3. Set vs List vs Array**
```kotlin
// Array - indexed, can have duplicates, fixed size
val array = arrayOf(1, 2, 2, 3)
array[0] = 10  // ✅ Can modify

// List - indexed, can have duplicates, dynamic size
val list = listOf(1, 2, 2, 3)
// list[0] = 10  // ❌ Compilation error

// Set - no index, no duplicates, dynamic size
val set = setOf(1, 2, 3)  // Note: 2 appears only once
// set[0] = 10  // ❌ No indexing
```

### **4. Performance Characteristics**
- **Add/Remove**: O(1) - very fast (average case)
- **Contains check**: O(1) - very fast (average case)
- **Iteration**: O(n) - linear time
- **Memory usage**: Similar to lists

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/43_set_hashset.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '43_set_hashsetKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Unique Word Counter**
Create a set to count unique words in a sentence.

**Solution:**
```kotlin
fun main() {
    val sentence = "Hello world! Hello Kotlin! Welcome to the world of Kotlin programming."
    val words = sentence.lowercase().split(" ")
    val uniqueWords = words.toSet()
    
    println("All words: $words")
    println("Unique words: $uniqueWords")
    println("Total words: ${words.size}")
    println("Unique word count: ${uniqueWords.size}")
    println("Duplicate words: ${words.size - uniqueWords.size}")
}
```

### **Exercise 2: Set Operations**
Perform various set operations on two sets of numbers.

**Solution:**
```kotlin
fun main() {
    val setA = setOf(1, 2, 3, 4, 5)
    val setB = setOf(4, 5, 6, 7, 8)
    
    println("Set A: $setA")
    println("Set B: $setB")
    println("Union: ${setA.union(setB)}")
    println("Intersection: ${setA.intersect(setB)}")
    println("A - B: ${setA.subtract(setB)}")
    println("B - A: ${setB.subtract(setA)}")
    println("Symmetric difference: ${setA.union(setB).subtract(setA.intersect(setB))}")
}
```

### **Exercise 3: Student Course Registration**
Manage student course registrations using sets.

**Solution:**
```kotlin
fun main() {
    val mathStudents = mutableSetOf("Alice", "Bob", "Charlie")
    val physicsStudents = mutableSetOf("Bob", "David", "Eve")
    val programmingStudents = mutableSetOf("Alice", "Charlie", "Frank")
    
    println("Math students: $mathStudents")
    println("Physics students: $physicsStudents")
    println("Programming students: $programmingStudents")
    
    // Students taking multiple courses
    val multiCourseStudents = mathStudents.intersect(physicsStudents)
        .union(mathStudents.intersect(programmingStudents))
        .union(physicsStudents.intersect(programmingStudents))
    
    println("Students taking multiple courses: $multiCourseStudents")
    
    // All unique students
    val allStudents = mathStudents.union(physicsStudents).union(programmingStudents)
    println("All students: $allStudents")
    
    // Students taking only one course
    val singleCourseStudents = allStudents.subtract(multiCourseStudents)
    println("Students taking only one course: $singleCourseStudents")
}
```

### **Exercise 4: Set Filtering and Analysis**
Create a set of numbers and perform various analyses.

**Solution:**
```kotlin
fun analyzeNumberSet(numbers: Set<Int>) {
    val evenNumbers = numbers.filter { it % 2 == 0 }
    val oddNumbers = numbers.filter { it % 2 != 0 }
    val primeNumbers = numbers.filter { isPrime(it) }
    val perfectSquares = numbers.filter { isPerfectSquare(it) }
    
    println("Original set: $numbers")
    println("Even numbers: $evenNumbers")
    println("Odd numbers: $oddNumbers")
    println("Prime numbers: $primeNumbers")
    println("Perfect squares: $perfectSquares")
    println("Sum: ${numbers.sum()}")
    println("Average: ${numbers.average()}")
}

fun isPrime(n: Int): Boolean {
    if (n < 2) return false
    for (i in 2 until n) {
        if (n % i == 0) return false
    }
    return true
}

fun isPerfectSquare(n: Int): Boolean {
    val sqrt = kotlin.math.sqrt(n.toDouble()).toInt()
    return sqrt * sqrt == n
}

fun main() {
    val numbers = setOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 16, 25)
    analyzeNumberSet(numbers)
}
```

## 🚨 Common Mistakes to Avoid

1. **Expecting order**: Sets don't maintain insertion order ❌
   - **Correct**: Use `LinkedHashSet` if order matters ✅

2. **Using sets for indexed access**: Sets don't support indexing ❌
   - **Correct**: Use lists or arrays for indexed access ✅

3. **Forgetting uniqueness**: Adding duplicate elements has no effect ✅

4. **Modifying immutable sets**: `setOf(1, 2, 3).add(4)` ❌
   - **Correct**: Use `mutableSetOf()` for mutable sets ✅

## 🎯 What's Next?

Now that you understand sets, continue with:

1. **Functional operations** → [Filter, Map, and Sorting](05-filter-map-sorting.md)
2. **Advanced collections** → [Collections Overview](../README.md#collections)
3. **Null safety** → [Null Safety](../null-safety/01-null-safety.md)
4. **Functional programming** → [Functional Programming](../functional-programming/01-lambdas.md)

## 📚 Additional Resources

- [Official Kotlin Sets Documentation](https://kotlinlang.org/docs/collections-overview.html#set)
- [Kotlin Collections API](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)
- [Set Methods Reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-set/)

## 🏆 Summary

- ✅ You can create both immutable and mutable sets
- ✅ You understand how sets ensure uniqueness
- ✅ You know how to perform mathematical set operations
- ✅ You can use functional operations like filter and map
- ✅ You're ready to work with advanced collection operations!

**Sets are perfect for managing unique collections and performing mathematical operations! 🎉**
