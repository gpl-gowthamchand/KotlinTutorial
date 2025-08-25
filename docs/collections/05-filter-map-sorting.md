# 📚 Filter, Map, and Sorting in Kotlin Collections

Functional operations on collections allow you to transform, filter, and organize data in a clean and readable way. These operations are fundamental to functional programming and make your code more expressive and maintainable.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Use `filter` and `filterNot` to select elements based on conditions
- ✅ Transform collections with `map` and `mapIndexed`
- ✅ Sort collections using various sorting methods
- ✅ Chain multiple operations together for complex transformations
- ✅ Understand the difference between eager and lazy evaluation

## 🔍 What You'll Learn

- **Filtering operations** - Selecting elements based on predicates
- **Mapping operations** - Transforming elements from one form to another
- **Sorting operations** - Organizing elements in various orders
- **Chaining operations** - Combining multiple operations efficiently
- **Performance considerations** - Understanding when to use different approaches

## 📝 Prerequisites

- Understanding of [Lists](02-lists.md), [Maps](03-maps.md), and [Sets](04-sets.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Lambdas](../functional-programming/01-lambdas.md)

## 💻 The Code

Let's examine the functional operations examples:

**📁 File:** [44_filter_map_sorting.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/44_filter_map_sorting.kt)

## 🔍 Code Breakdown

### **1. Filtering Operations**

#### **Basic Filtering with `filter()`**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Filter even numbers
val evenNumbers = numbers.filter { it % 2 == 0 }        // [2, 4, 6, 8, 10]

// Filter numbers greater than 5
val largeNumbers = numbers.filter { it > 5 }            // [6, 7, 8, 9, 10]

// Filter numbers in a range
val rangeNumbers = numbers.filter { it in 3..7 }        // [3, 4, 5, 6, 7]
```

#### **Filtering with `filterNot()`**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Filter out even numbers (keep odd numbers)
val oddNumbers = numbers.filterNot { it % 2 == 0 }      // [1, 3, 5, 7, 9]

// Filter out numbers less than 5
val highNumbers = numbers.filterNot { it < 5 }          // [5, 6, 7, 8, 9, 10]
```

#### **Filtering with Index**
```kotlin
val names = listOf("Alice", "Bob", "Charlie", "David", "Eve")

// Filter names with even indices
val evenIndexNames = names.filterIndexed { index, _ -> index % 2 == 0 }
// Result: ["Alice", "Charlie", "Eve"]

// Filter names that start with a letter and have index > 1
val filteredNames = names.filterIndexed { index, name ->
    index > 1 && name.startsWith("C")
}
// Result: ["Charlie"]
```

#### **Filtering with Predicates**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Using predefined predicates
val isEven = { n: Int -> n % 2 == 0 }
val isPositive = { n: Int -> n > 0 }
val isInRange = { n: Int -> n in 1..5 }

val filtered = numbers.filter { isEven(it) && isPositive(it) && isInRange(it) }
// Result: [2, 4]
```

### **2. Mapping Operations**

#### **Basic Mapping with `map()`**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// Double each number
val doubled = numbers.map { it * 2 }                    // [2, 4, 6, 8, 10]

// Square each number
val squared = numbers.map { it * it }                   // [1, 4, 9, 16, 25]

// Convert to string
val strings = numbers.map { "Number: $it" }             // ["Number: 1", "Number: 2", ...]
```

#### **Mapping with Index using `mapIndexed()`**
```kotlin
val names = listOf("Alice", "Bob", "Charlie")

// Add index to each name
val indexedNames = names.mapIndexed { index, name ->
    "${index + 1}. $name"
}
// Result: ["1. Alice", "2. Bob", "3. Charlie"]

// Create pairs of index and name
val pairs = names.mapIndexed { index, name ->
    index to name
}
// Result: [(0, "Alice"), (1, "Bob"), (2, "Charlie")]
```

#### **Mapping with Conditions**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Map even numbers to their square, odd numbers to their double
val transformed = numbers.map { n ->
    when {
        n % 2 == 0 -> n * n      // Even: square
        else -> n * 2             // Odd: double
    }
}
// Result: [2, 4, 6, 16, 10, 36, 14, 64, 18, 100]
```

### **3. Sorting Operations**

#### **Basic Sorting with `sorted()`**
```kotlin
val numbers = listOf(3, 1, 4, 1, 5, 9, 2, 6)

// Sort in ascending order
val ascending = numbers.sorted()                         // [1, 1, 2, 3, 4, 5, 6, 9]

// Sort in descending order
val descending = numbers.sortedDescending()              // [9, 6, 5, 4, 3, 2, 1, 1]
```

#### **Custom Sorting with `sortedBy()`**
```kotlin
val names = listOf("Alice", "Bob", "Charlie", "David", "Eve")

// Sort by length
val byLength = names.sortedBy { it.length }             // ["Bob", "Eve", "Alice", "David", "Charlie"]

// Sort by length in descending order
val byLengthDesc = names.sortedByDescending { it.length } // ["Charlie", "David", "Alice", "Bob", "Eve"]

// Sort by first letter
val byFirstLetter = names.sortedBy { it.first() }       // ["Alice", "Bob", "Charlie", "David", "Eve"]
```

#### **Sorting with Multiple Criteria**
```kotlin
data class Person(val name: String, val age: Int, val city: String)

val people = listOf(
    Person("Alice", 25, "New York"),
    Person("Bob", 30, "Boston"),
    Person("Charlie", 25, "New York"),
    Person("David", 30, "Chicago")
)

// Sort by age first, then by name
val sortedPeople = people.sortedWith(
    compareBy<Person> { it.age }.thenBy { it.name }
)
```

### **4. Chaining Operations**

#### **Filter then Map**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Filter even numbers, then square them
val evenSquares = numbers
    .filter { it % 2 == 0 }
    .map { it * it }
// Result: [4, 16, 36, 64, 100]
```

#### **Map then Filter**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// Double numbers, then filter those greater than 5
val doubledAndFiltered = numbers
    .map { it * 2 }
    .filter { it > 5 }
// Result: [6, 8, 10]
```

#### **Complex Chain**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val result = numbers
    .filter { it % 2 == 0 }           // Keep even numbers
    .map { it * it }                   // Square them
    .filter { it > 20 }                // Keep squares > 20
    .sorted()                          // Sort in ascending order
// Result: [36, 64, 100]
```

### **5. Advanced Operations**

#### **Flattening with `flatMap()`**
```kotlin
val words = listOf("hello", "world", "kotlin")

// Split each word into characters and flatten
val characters = words.flatMap { it.toList() }
// Result: ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd', 'k', 'o', 't', 'l', 'i', 'n']

// Create all possible pairs
val pairs = words.flatMap { word1 ->
    words.map { word2 -> "$word1-$word2" }
}
```

#### **Grouping with `groupBy()`**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Group by even/odd
val groupedByParity = numbers.groupBy { it % 2 == 0 }
// Result: {false=[1, 3, 5, 7, 9], true=[2, 4, 6, 8, 10]}

// Group by range
val groupedByRange = numbers.groupBy { 
    when {
        it <= 3 -> "Small"
        it <= 7 -> "Medium"
        else -> "Large"
    }
}
// Result: {Small=[1, 2, 3], Medium=[4, 5, 6, 7], Large=[8, 9, 10]}
```

#### **Partitioning with `partition()`**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// Partition into even and odd
val (even, odd) = numbers.partition { it % 2 == 0 }
// even: [2, 4, 6, 8, 10], odd: [1, 3, 5, 7, 9]

// Partition into small and large
val (small, large) = numbers.partition { it <= 5 }
// small: [1, 2, 3, 4, 5], large: [6, 7, 8, 9, 10]
```

## 🎯 Key Concepts Explained

### **1. Eager vs Lazy Evaluation**
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// Eager evaluation - operations are performed immediately
val eagerResult = numbers.filter { it % 2 == 0 }.map { it * it }

// Lazy evaluation - operations are performed only when needed
val lazyResult = numbers.asSequence()
    .filter { it % 2 == 0 }
    .map { it * it }
    .toList()
```

### **2. Performance Considerations**
```kotlin
val largeList = (1..1000000).toList()

// Less efficient - creates intermediate collections
val result1 = largeList
    .filter { it % 2 == 0 }
    .map { it * it }
    .take(10)

// More efficient - uses sequences for lazy evaluation
val result2 = largeList.asSequence()
    .filter { it % 2 == 0 }
    .map { it * it }
    .take(10)
    .toList()
```

### **3. Immutability**
```kotlin
val original = listOf(1, 2, 3, 4, 5)

// These operations don't modify the original list
val filtered = original.filter { it > 3 }    // [4, 5]
val mapped = original.map { it * 2 }         // [2, 4, 6, 8, 10]

println(original)  // Still [1, 2, 3, 4, 5]
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/44_filter_map_sorting.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '44_filter_map_sortingKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Student Grade Analysis**
Create a list of student grades and perform various analyses.

**Solution:**
```kotlin
data class Student(val name: String, val grade: Int, val subject: String)

fun main() {
    val students = listOf(
        Student("Alice", 95, "Math"),
        Student("Bob", 87, "Math"),
        Student("Charlie", 92, "Math"),
        Student("Alice", 88, "Physics"),
        Student("Bob", 91, "Physics"),
        Student("Charlie", 85, "Physics")
    )
    
    // Find top students in Math
    val topMathStudents = students
        .filter { it.subject == "Math" }
        .sortedByDescending { it.grade }
        .take(2)
        .map { "${it.name}: ${it.grade}" }
    
    println("Top Math students: $topMathStudents")
    
    // Calculate average grade by subject
    val avgBySubject = students
        .groupBy { it.subject }
        .mapValues { (_, students) -> students.map { it.grade }.average() }
    
    println("Average by subject: $avgBySubject")
}
```

### **Exercise 2: Text Processing Pipeline**
Process text through multiple transformation steps.

**Solution:**
```kotlin
fun main() {
    val text = "Hello World! Welcome to Kotlin Programming. Let's learn together!"
    
    val processedText = text
        .lowercase()                    // Convert to lowercase
        .split(" ")                     // Split into words
        .filter { it.length > 3 }       // Keep words longer than 3 characters
        .map { it.trim('.', '!', ',') } // Remove punctuation
        .filter { it.isNotEmpty() }     // Remove empty strings
        .distinct()                     // Remove duplicates
        .sorted()                       // Sort alphabetically
    
    println("Original: $text")
    println("Processed: $processedText")
    
    // Word frequency analysis
    val wordFreq = text
        .lowercase()
        .split(" ")
        .filter { it.isNotEmpty() }
        .groupBy { it.trim('.', '!', ',') }
        .mapValues { it.value.size }
        .toList()
        .sortedByDescending { it.second }
    
    println("Word frequencies: $wordFreq")
}
```

### **Exercise 3: Number Sequence Analysis**
Analyze a sequence of numbers using functional operations.

**Solution:**
```kotlin
fun analyzeNumbers(numbers: List<Int>) {
    val analysis = numbers
        .filter { it > 0 }              // Keep positive numbers
        .let { positiveNumbers ->
            mapOf(
                "count" to positiveNumbers.size,
                "sum" to positiveNumbers.sum(),
                "average" to positiveNumbers.average(),
                "even" to positiveNumbers.filter { it % 2 == 0 },
                "odd" to positiveNumbers.filter { it % 2 != 0 },
                "squares" to positiveNumbers.map { it * it },
                "sorted" to positiveNumbers.sorted(),
                "reversed" to positiveNumbers.sortedDescending()
            )
        }
    
    analysis.forEach { (key, value) ->
        println("$key: $value")
    }
}

fun main() {
    val numbers = listOf(-2, 1, 3, -4, 5, 6, -7, 8, 9, -10)
    analyzeNumbers(numbers)
}
```

### **Exercise 4: Complex Data Transformation**
Transform complex data structures using functional operations.

**Solution:**
```kotlin
data class Product(val name: String, val price: Double, val category: String, val rating: Double)

fun main() {
    val products = listOf(
        Product("Laptop", 999.99, "Electronics", 4.5),
        Product("Mouse", 29.99, "Electronics", 4.2),
        Product("Book", 19.99, "Books", 4.8),
        Product("Chair", 199.99, "Furniture", 4.1),
        Product("Table", 299.99, "Furniture", 4.3),
        Product("Pen", 2.99, "Office", 4.0)
    )
    
    // Find expensive electronics with high ratings
    val expensiveElectronics = products
        .filter { it.category == "Electronics" && it.price > 100 && it.rating >= 4.0 }
        .sortedByDescending { it.rating }
        .map { "${it.name} ($${it.price}) - Rating: ${it.rating}" }
    
    println("Expensive electronics: $expensiveElectronics")
    
    // Group by category and calculate statistics
    val categoryStats = products
        .groupBy { it.category }
        .mapValues { (_, products) ->
            mapOf(
                "count" to products.size,
                "avgPrice" to products.map { it.price }.average(),
                "avgRating" to products.map { it.rating }.average(),
                "totalValue" to products.map { it.price }.sum()
            )
        }
    
    println("Category statistics: $categoryStats")
}
```

## 🚨 Common Mistakes to Avoid

1. **Chaining too many operations**: Can reduce readability ❌
   - **Better**: Break into multiple lines or extract functions ✅

2. **Forgetting immutability**: Operations don't modify original collections ✅

3. **Using sequences unnecessarily**: For small collections, regular operations are fine ✅

4. **Inefficient filtering**: Filter before map when possible ✅

## 🎯 What's Next?

Now that you understand functional operations, continue with:

1. **Advanced collections** → [Collections Overview](../README.md#collections)
2. **Functional programming** → [Functional Programming](../functional-programming/01-lambdas.md)
3. **Null safety** → [Null Safety](../null-safety/01-null-safety.md)
4. **Coroutines** → [Coroutines](../coroutines/01-introduction.md)

## 📚 Additional Resources

- [Official Kotlin Collections Documentation](https://kotlinlang.org/docs/collections-overview.html)
- [Kotlin Collections API](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)
- [Functional Programming in Kotlin](https://kotlinlang.org/docs/fun-interfaces.html)

## 🏆 Summary

- ✅ You can filter collections using various predicates
- ✅ You can transform collections with map operations
- ✅ You can sort collections in multiple ways
- ✅ You can chain operations for complex transformations
- ✅ You understand performance considerations and best practices

**Functional operations make your code more readable and maintainable. Use them wisely! 🎉**
