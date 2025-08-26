# 🔄 Iterators in Kotlin

Iterators are the foundation of collection iteration in Kotlin. They provide a way to traverse through collections one element at a time, giving you fine-grained control over how you process data.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what iterators are and how they work
- ✅ Use different types of iterators (forward, backward, bidirectional)
- ✅ Create custom iterators for your own classes
- ✅ Understand the relationship between iterators and collections
- ✅ Use iterator patterns effectively in your code

## 🔍 What You'll Learn

- **Iterator fundamentals** - What iterators are and how they work
- **Iterator interface** - Understanding the Iterator interface
- **Collection iterators** - How collections implement iteration
- **Custom iterators** - Creating iterators for your own classes
- **Iterator patterns** - Common patterns and best practices

## 📝 Prerequisites

- Understanding of [Collections](../collections/01-arrays.md)
- Knowledge of [For Loops](03-for-loops.md)
- Familiarity with [Control Flow](01-if-expressions.md)

## 💻 The Code

Let's examine iterators in action:

**📁 File:** [12_for_loop.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/12_for_loop.kt)

## 🔍 Code Breakdown

### **1. Understanding Iterators**

#### **What is an Iterator?**
An iterator is an object that allows you to traverse through a collection one element at a time. It provides three main operations:
- **`hasNext()`**: Check if there are more elements
- **`next()`**: Get the next element
- **`remove()`**: Remove the last returned element (optional)

#### **Basic Iterator Usage**
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    
    // Get iterator from list
    val iterator = numbers.iterator()
    
    // Manual iteration
    while (iterator.hasNext()) {
        val number = iterator.next()
        println("Number: $number")
    }
}
```

### **2. Iterator Interface**

#### **Iterator Interface Definition**
```kotlin
interface Iterator<T> {
    fun hasNext(): Boolean
    fun next(): T
    fun remove() // Optional, not always implemented
}
```

#### **Using Iterator Methods**
```kotlin
fun demonstrateIterator() {
    val fruits = listOf("Apple", "Banana", "Cherry")
    val iterator = fruits.iterator()
    
    println("Iterating through fruits:")
    while (iterator.hasNext()) {
        val fruit = iterator.next()
        println("- $fruit")
    }
}
```

### **3. Collection Iterators**

#### **List Iterator**
```kotlin
fun listIteratorExample() {
    val numbers = listOf(10, 20, 30, 40, 50)
    
    // Forward iteration
    println("Forward:")
    val forwardIterator = numbers.listIterator()
    while (forwardIterator.hasNext()) {
        println("${forwardIterator.nextIndex()}: ${forwardIterator.next()}")
    }
    
    // Backward iteration
    println("\nBackward:")
    val backwardIterator = numbers.listIterator(numbers.size)
    while (backwardIterator.hasPrevious()) {
        println("${backwardIterator.previousIndex()}: ${backwardIterator.previous()}")
    }
}
```

#### **Mutable List Iterator**
```kotlin
fun mutableIteratorExample() {
    val mutableNumbers = mutableListOf(1, 2, 3, 4, 5)
    val iterator = mutableNumbers.listIterator()
    
    while (iterator.hasNext()) {
        val number = iterator.next()
        if (number % 2 == 0) {
            // Remove even numbers
            iterator.remove()
        }
    }
    
    println("After removing even numbers: $mutableNumbers")
}
```

### **4. Custom Iterators**

#### **Creating a Custom Iterator**
```kotlin
class NumberRange(private val start: Int, private val end: Int) {
    fun iterator(): Iterator<Int> = object : Iterator<Int> {
        private var current = start
        
        override fun hasNext(): Boolean = current <= end
        
        override fun next(): Int {
            if (!hasNext()) {
                throw NoSuchElementException()
            }
            return current++
        }
    }
}

fun customIteratorExample() {
    val range = NumberRange(1, 5)
    
    for (number in range) {
        println("Custom range: $number")
    }
}
```

#### **Iterator with Custom Logic**
```kotlin
class StepIterator(
    private val start: Int,
    private val end: Int,
    private val step: Int
) : Iterator<Int> {
    private var current = start
    
    override fun hasNext(): Boolean = current <= end
    
    override fun next(): Int {
        if (!hasNext()) {
            throw NoSuchElementException()
        }
        val result = current
        current += step
        return result
    }
}

fun stepIteratorExample() {
    val stepRange = object : Iterable<Int> {
        override fun iterator(): Iterator<Int> = StepIterator(0, 10, 2)
    }
    
    for (number in stepRange) {
        println("Step by 2: $number")
    }
}
```

### **5. Iterator Patterns**

#### **Filtering with Iterator**
```kotlin
class FilteringIterator<T>(
    private val iterator: Iterator<T>,
    private val predicate: (T) -> Boolean
) : Iterator<T> {
    private var nextElement: T? = null
    private var hasNextElement = false
    
    override fun hasNext(): Boolean {
        if (hasNextElement) return true
        
        while (iterator.hasNext()) {
            val element = iterator.next()
            if (predicate(element)) {
                nextElement = element
                hasNextElement = true
                return true
            }
        }
        return false
    }
    
    override fun next(): T {
        if (!hasNext()) {
            throw NoSuchElementException()
        }
        hasNextElement = false
        return nextElement!!
    }
}

fun filteringIteratorExample() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    val evenNumbers = object : Iterable<Int> {
        override fun iterator(): Iterator<Int> = 
            FilteringIterator(numbers.iterator()) { it % 2 == 0 }
    }
    
    for (number in evenNumbers) {
        println("Even number: $number")
    }
}
```

## 🎯 Key Concepts Explained

### **1. Iterator vs For Loop**

**Iterator (Manual Control):**
```kotlin
val iterator = list.iterator()
while (iterator.hasNext()) {
    val element = iterator.next()
    // Process element
}
```

**For Loop (Automatic):**
```kotlin
for (element in list) {
    // Process element
}
```

**Key Differences:**
- **Iterator**: Manual control, can modify during iteration
- **For Loop**: Automatic, cleaner syntax, can't modify during iteration

### **2. Iterator Types**

- **`Iterator<T>`**: Basic forward-only iterator
- **`ListIterator<T>`**: Bidirectional iterator with index access
- **`MutableIterator<T>`**: Iterator that can modify collections
- **Custom Iterators**: User-defined iteration behavior

### **3. When to Use Iterators**

**Use Iterators when:**
- You need to modify the collection during iteration
- You want custom iteration logic
- You need bidirectional traversal
- You're implementing custom collection types

**Use For Loops when:**
- You want simple, readable iteration
- You don't need to modify the collection
- You're doing standard collection traversal

## 🚀 Advanced Iterator Concepts

### **1. Lazy Iteration**
```kotlin
fun fibonacciIterator(): Iterator<Long> = object : Iterator<Long> {
    private var current = 0L
    private var next = 1L
    
    override fun hasNext(): Boolean = true // Infinite sequence
    
    override fun next(): Long {
        val result = current
        current = next
        next = result + next
        return result
    }
}

fun lazyIterationExample() {
    val fibonacci = fibonacciIterator()
    
    // Take first 10 Fibonacci numbers
    repeat(10) {
        println("Fibonacci ${it + 1}: ${fibonacci.next()}")
    }
}
```

### **2. Chaining Iterators**
```kotlin
fun <T> Iterator<T>.filter(predicate: (T) -> Boolean): Iterator<T> {
    return FilteringIterator(this, predicate)
}

fun <T, R> Iterator<T>.map(transform: (T) -> R): Iterator<R> {
    return object : Iterator<R> {
        override fun hasNext(): Boolean = this@map.hasNext()
        override fun next(): R = transform(this@map.next())
    }
}

fun chainingExample() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    val result = numbers.iterator()
        .filter { it % 2 == 0 }
        .map { it * it }
    
    for (number in result) {
        println("Even squared: $number")
    }
}
```

## 💡 Best Practices

### **1. Iterator Safety**
- Always check `hasNext()` before calling `next()`
- Don't modify collections during iteration (unless using mutable iterators)
- Handle `NoSuchElementException` appropriately

### **2. Performance Considerations**
- Iterators are memory-efficient for large collections
- Use `forEach` for simple operations
- Consider lazy evaluation for expensive operations

### **3. Custom Iterator Design**
- Keep iterators simple and focused
- Implement proper error handling
- Consider thread safety if needed

## 🔧 Common Pitfalls

### **1. Concurrent Modification**
```kotlin
// ❌ Wrong - Concurrent modification
val list = mutableListOf(1, 2, 3, 4, 5)
for (i in list) {
    if (i % 2 == 0) {
        list.remove(i) // Throws ConcurrentModificationException
    }
}

// ✅ Correct - Use iterator
val list = mutableListOf(1, 2, 3, 4, 5)
val iterator = list.listIterator()
while (iterator.hasNext()) {
    val i = iterator.next()
    if (i % 2 == 0) {
        iterator.remove() // Safe removal
    }
}
```

### **2. Infinite Iterators**
```kotlin
// ❌ Wrong - Infinite loop
val infiniteIterator = object : Iterator<Int> {
    override fun hasNext(): Boolean = true
    override fun next(): Int = 1
}

// Always have a termination condition
val limitedIterator = object : Iterator<Int> {
    private var count = 0
    private val limit = 10
    
    override fun hasNext(): Boolean = count < limit
    override fun next(): Int = ++count
}
```

## 📚 Summary

Iterators are powerful tools that give you fine-grained control over collection iteration. They're essential for:
- **Custom iteration logic**
- **Modifying collections during iteration**
- **Implementing custom collection types**
- **Advanced iteration patterns**

## 🎯 Practice Exercises

1. **Basic Iterator**: Create an iterator that counts from 1 to 10
2. **Filter Iterator**: Build an iterator that only returns even numbers
3. **Custom Collection**: Implement a custom collection with its own iterator
4. **Bidirectional Iterator**: Create an iterator that can go both forward and backward

## 🔗 Related Topics

- [For Loops](03-for-loops.md) - Automatic iteration
- [Collections](../collections/01-arrays.md) - Data structures
- [Control Flow](01-if-expressions.md) - Program flow control
- [Functions](../functions/01-functions-basics.md) - Function fundamentals

## 📖 Additional Resources

- [Official Kotlin Collections Documentation](https://kotlinlang.org/docs/collections-overview.html)
- [Iterator Interface](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-iterator/)
- [Collection Iteration](https://kotlinlang.org/docs/iterators.html)

---

**Next Lesson**: [For Loops](03-for-loops.md) - Learn how for loops use iterators internally

**Happy coding with Iterators! 🚀**
