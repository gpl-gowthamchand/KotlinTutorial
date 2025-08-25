# 📚 Maps and HashMaps in Kotlin

Maps are key-value pair collections that allow you to store and retrieve data using unique keys. They're essential for creating lookup tables, caches, and organizing related data.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Create and initialize maps in different ways
- ✅ Understand the difference between immutable and mutable maps
- ✅ Add, remove, and modify map entries
- ✅ Use map methods for searching, filtering, and transformation
- ✅ Work with map keys, values, and entries

## 🔍 What You'll Learn

- **Map creation** - Different ways to create maps
- **Key-value pairs** - Understanding map structure
- **Element manipulation** - Adding, removing, and updating entries
- **Map methods** - Built-in functions for map operations
- **Functional operations** - Using lambdas with maps

## 📝 Prerequisites

- Understanding of [Lists](02-lists.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Control Flow](../control-flow/01-if-expressions.md)

## 💻 The Code

Let's examine the maps example:

**📁 File:** [42_map_hashmap.kt](../src/42_map_hashmap.kt)

## 🔍 Code Breakdown

### **1. Map Creation**

#### **Immutable Maps with `mapOf()`**
```kotlin
val countries = mapOf(
    "US" to "United States",
    "UK" to "United Kingdom",
    "CA" to "Canada"
)

val scores = mapOf(
    "Alice" to 95,
    "Bob" to 87,
    "Charlie" to 92
)
```

#### **Mutable Maps with `mutableMapOf()`**
```kotlin
val mutableCountries = mutableMapOf(
    "US" to "United States",
    "UK" to "United Kingdom"
)

val mutableScores = mutableMapOf<String, Int>()
```

#### **Using `HashMap()` Constructor**
```kotlin
val hashMap = HashMap<String, Int>()
hashMap["Alice"] = 95
hashMap["Bob"] = 87
```

### **2. Accessing Map Elements**

#### **Using Square Brackets**
```kotlin
val countries = mapOf("US" to "United States", "UK" to "United Kingdom")
val usName = countries["US"]        // "United States"
val caName = countries["CA"]        // null (key doesn't exist)
```

#### **Safe Access Methods**
```kotlin
val countries = mapOf("US" to "United States", "UK" to "United Kingdom")
val usName = countries.get("US")                    // "United States"
val caName = countries.getOrDefault("CA", "Unknown") // "Unknown"
val frName = countries.getOrElse("FR") { "France" }  // "France"
```

### **3. Modifying Mutable Maps**

#### **Adding and Updating Entries**
```kotlin
val scores = mutableMapOf<String, Int>()
scores["Alice"] = 95        // Add new entry
scores["Bob"] = 87          // Add new entry
scores["Alice"] = 98        // Update existing entry
scores.put("Charlie", 92)   // Using put() method
```

#### **Removing Entries**
```kotlin
val scores = mutableMapOf("Alice" to 95, "Bob" to 87, "Charlie" to 92)
scores.remove("Bob")                    // Remove by key
scores.remove("Alice", 95)              // Remove by key-value pair
scores.clear()                          // Remove all entries
```

### **4. Map Properties**

```kotlin
val countries = mapOf("US" to "United States", "UK" to "United Kingdom")
println("Size: ${countries.size}")           // 2
println("Is empty: ${countries.isEmpty()}")   // false
println("Keys: ${countries.keys}")           // [US, UK]
println("Values: ${countries.values}")       // [United States, United Kingdom]
```

### **5. Iterating Through Maps**

#### **Using for loop with entries**
```kotlin
val countries = mapOf("US" to "United States", "UK" to "United Kingdom")
for ((code, name) in countries) {
    println("$code -> $name")
}
```

#### **Using forEach function**
```kotlin
val countries = mapOf("US" to "United States", "UK" to "United Kingdom")
countries.forEach { (code, name) ->
    println("$code -> $name")
}
```

#### **Iterating over keys and values separately**
```kotlin
val countries = mapOf("US" to "United States", "UK" to "United Kingdom")

// Iterate over keys
for (code in countries.keys) {
    println("Country code: $code")
}

// Iterate over values
for (name in countries.values) {
    println("Country name: $name")
}
```

### **6. Map Searching and Filtering**

#### **Finding Entries**
```kotlin
val scores = mapOf("Alice" to 95, "Bob" to 87, "Charlie" to 92)
val aliceScore = scores["Alice"]                    // 95
val hasHighScore = scores.any { it.value >= 90 }   // true
val allHighScores = scores.all { it.value >= 80 }  // true
```

#### **Filtering Entries**
```kotlin
val scores = mapOf("Alice" to 95, "Bob" to 87, "Charlie" to 92, "David" to 78)
val highScores = scores.filter { it.value >= 90 }      // {Alice=95, Charlie=92}
val lowScores = scores.filterNot { it.value >= 80 }    // {David=78}
val topThree = scores.toList().sortedByDescending { it.second }.take(3).toMap()
```

### **7. Map Transformation**

#### **Transforming Keys and Values**
```kotlin
val scores = mapOf("Alice" to 95, "Bob" to 87, "Charlie" to 92)

// Transform values
val letterGrades = scores.mapValues { (_, score) ->
    when {
        score >= 90 -> "A"
        score >= 80 -> "B"
        score >= 70 -> "C"
        else -> "D"
    }
}

// Transform keys
val upperCaseNames = scores.mapKeys { (name, _) -> name.uppercase() }
```

#### **Creating Lists from Maps**
```kotlin
val scores = mapOf("Alice" to 95, "Bob" to 87, "Charlie" to 92)

val names = scores.keys.toList()           // [Alice, Bob, Charlie]
val scoreValues = scores.values.toList()   // [95, 87, 92]
val entries = scores.toList()              // [(Alice, 95), (Bob, 87), (Charlie, 92)]
```

## 🎯 Key Concepts Explained

### **1. Immutable vs Mutable Maps**
```kotlin
// Immutable Map - cannot be modified
val immutableMap = mapOf("A" to 1, "B" to 2)
// immutableMap["C"] = 3  // ❌ Compilation error

// Mutable Map - can be modified
val mutableMap = mutableMapOf("A" to 1, "B" to 2)
mutableMap["C"] = 3  // ✅ Can modify
```

### **2. Map vs List vs Array**
```kotlin
// Array - indexed by position, fixed size
val array = arrayOf("Alice", "Bob", "Charlie")
val name = array[0]  // "Alice"

// List - indexed by position, dynamic size
val list = listOf("Alice", "Bob", "Charlie")
val name = list[0]   // "Alice"

// Map - indexed by key, dynamic size
val map = mapOf("first" to "Alice", "second" to "Bob")
val name = map["first"]  // "Alice"
```

### **3. Map Performance Characteristics**
- **Access by key**: O(1) - very fast (average case)
- **Search by value**: O(n) - linear time
- **Add/Remove**: O(1) - very fast (average case)
- **Memory usage**: Higher than lists due to key storage

### **4. Key Requirements**
```kotlin
// Keys must be unique
val scores = mutableMapOf<String, Int>()
scores["Alice"] = 95
scores["Alice"] = 98  // Overwrites previous value

// Keys must be immutable (or at least stable)
val badMap = mutableMapOf<MutableList<Int>, String>()  // ❌ Don't do this
val goodMap = mutableMapOf<String, String>()           // ✅ Do this
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/42_map_hashmap.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '42_map_hashmapKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Student Grades**
Create a map to store student grades and perform various operations.

**Solution:**
```kotlin
fun main() {
    val grades = mutableMapOf<String, Int>()
    
    // Add grades
    grades["Alice"] = 95
    grades["Bob"] = 87
    grades["Charlie"] = 92
    grades["David"] = 78
    
    println("All grades: $grades")
    
    // Update a grade
    grades["Bob"] = 89
    println("After update: $grades")
    
    // Remove a student
    grades.remove("David")
    println("After removal: $grades")
    
    // Find average grade
    val average = grades.values.average()
    println("Average grade: $average")
}
```

### **Exercise 2: Word Frequency Counter**
Count the frequency of words in a sentence.

**Solution:**
```kotlin
fun countWords(sentence: String): Map<String, Int> {
    val words = sentence.lowercase().split(" ")
    val frequency = mutableMapOf<String, Int>()
    
    for (word in words) {
        val cleanWord = word.trim('.', ',', '!', '?')
        frequency[cleanWord] = frequency.getOrDefault(cleanWord, 0) + 1
    }
    
    return frequency
}

fun main() {
    val sentence = "Hello world! Hello Kotlin! Welcome to the world of Kotlin programming."
    val wordCount = countWords(sentence)
    
    println("Word frequencies:")
    wordCount.forEach { (word, count) ->
        println("$word: $count")
    }
}
```

### **Exercise 3: Map Filtering and Transformation**
Create a map of products and prices, then filter and transform it.

**Solution:**
```kotlin
fun main() {
    val products = mapOf(
        "Laptop" to 999.99,
        "Mouse" to 29.99,
        "Keyboard" to 79.99,
        "Monitor" to 299.99,
        "Headphones" to 149.99
    )
    
    // Find expensive products (>$100)
    val expensive = products.filter { it.value > 100 }
    println("Expensive products: $expensive")
    
    // Apply 20% discount
    val discounted = products.mapValues { (_, price) -> price * 0.8 }
    println("Discounted prices: $discounted")
    
    // Find total value
    val total = products.values.sum()
    println("Total value: $total")
}
```

### **Exercise 4: Nested Maps**
Create a nested map structure for organizing data.

**Solution:**
```kotlin
fun main() {
    val students = mapOf(
        "Alice" to mapOf(
            "age" to 20,
            "major" to "Computer Science",
            "grades" to mapOf("Math" to 95, "Physics" to 88, "Programming" to 92)
        ),
        "Bob" to mapOf(
            "age" to 22,
            "major" to "Mathematics",
            "grades" to mapOf("Math" to 98, "Physics" to 85, "Programming" to 78)
        )
    )
    
    // Access nested data
    val aliceAge = students["Alice"]?.get("age")
    val bobMathGrade = students["Bob"]?.get("grades")?.get("Math")
    
    println("Alice's age: $aliceAge")
    println("Bob's Math grade: $bobMathGrade")
    
    // Print all student information
    students.forEach { (name, info) ->
        println("\n$name:")
        info.forEach { (key, value) ->
            println("  $key: $value")
        }
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Accessing non-existent keys**: `map["key"]` might return `null` ❌
   - **Better**: Use `getOrDefault()` or `getOrElse()` ✅

2. **Modifying immutable maps**: `mapOf("A" to 1)["B"] = 2` ❌
   - **Correct**: Use `mutableMapOf()` for mutable maps ✅

3. **Using mutable objects as keys**: Keys should be immutable ✅

4. **Forgetting map keys are unique**: Adding same key overwrites value ✅

## 🎯 What's Next?

Now that you understand maps, continue with:

1. **Sets** → [Sets and HashSets](04-sets.md)
2. **Functional operations** → [Filter, Map, and Sorting](05-filter-map-sorting.md)
3. **Advanced collections** → [Collections Overview](../README.md#collections)
4. **Null safety** → [Null Safety](../null-safety/01-null-safety.md)

## 📚 Additional Resources

- [Official Kotlin Maps Documentation](https://kotlinlang.org/docs/collections-overview.html#map)
- [Kotlin Collections API](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)
- [Map Methods Reference](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-map/)

## 🏆 Summary

- ✅ You can create both immutable and mutable maps
- ✅ You understand how to add, remove, and modify entries
- ✅ You know map properties and iteration methods
- ✅ You can use functional operations like filter, map, and transform
- ✅ You're ready to work with sets and other collections!

**Maps are powerful for organizing data by keys. Use them to create efficient lookups! 🎉**
