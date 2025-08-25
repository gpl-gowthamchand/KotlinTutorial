# 🔄 Tailrec Functions in Kotlin

Tailrec functions in Kotlin are a powerful optimization feature that converts recursive functions into efficient loops, preventing stack overflow errors and improving performance.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what tailrec functions are
- ✅ Create tailrec functions correctly
- ✅ Know when to use tailrec optimization
- ✅ Understand the limitations and requirements
- ✅ Apply tailrec functions in real-world scenarios

## 🔍 What You'll Learn

- **Tailrec function syntax** - How to declare and use tailrec functions
- **Tail recursion** - Understanding what makes a function tail recursive
- **Optimization benefits** - How tailrec prevents stack overflow
- **Use cases** - When and where to use tailrec functions
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of functions in Kotlin
- ✅ Knowledge of recursion concepts
- ✅ Familiarity with Kotlin syntax
- ✅ Understanding of stack and memory concepts

## 💻 The Code

Let's examine the tailrec functions examples:

**📁 File:** [25_tailrec_function.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/25_tailrec_function.kt)

## 🔍 Code Breakdown

### **Basic Tailrec Function Declaration**
```kotlin
tailrec fun factorial(n: Int, accumulator: Int = 1): Int {
    return if (n <= 1) accumulator else factorial(n - 1, n * accumulator)
}
```

**Key Components:**
- `tailrec` - Keyword that enables tail recursion optimization
- `fun factorial` - Function declaration
- `n: Int, accumulator: Int = 1` - Parameters with default value
- `factorial(n - 1, n * accumulator)` - Tail recursive call

### **Tailrec vs Regular Recursion**
```kotlin
// ❌ Regular recursion (can cause stack overflow)
fun factorialRegular(n: Int): Int {
    return if (n <= 1) 1 else n * factorialRegular(n - 1)
}

// ✅ Tailrec function (optimized to loop)
tailrec fun factorialTailrec(n: Int, accumulator: Int = 1): Int {
    return if (n <= 1) accumulator else factorialTailrec(n - 1, n * accumulator)
}
```

## 🎯 Key Concepts Explained

### **1. What is Tail Recursion?**

A function is **tail recursive** when:
- The recursive call is the **last operation** in the function
- No additional computation is performed after the recursive call
- The result of the recursive call is returned directly

### **2. How Tailrec Optimization Works**

The Kotlin compiler converts tailrec functions into loops:
- **Eliminates stack frames** for each recursive call
- **Prevents stack overflow** errors
- **Improves performance** by reducing memory usage
- **Maintains readability** of recursive code

### **3. Tail Recursion vs Regular Recursion**

| Regular Recursion | Tail Recursion |
|-------------------|----------------|
| Performs computation after recursive call | No computation after recursive call |
| Can cause stack overflow | Optimized to prevent stack overflow |
| Less efficient | More efficient |
| Harder to optimize | Easy to optimize |

## 🧪 Examples and Exercises

### **Example 1: Factorial Function**
```kotlin
tailrec fun factorial(n: Int, accumulator: Int = 1): Int {
    return if (n <= 1) accumulator else factorial(n - 1, n * accumulator)
}

// Usage
val result = factorial(5)  // Returns 120 (5 * 4 * 3 * 2 * 1)
```

**How it works:**
1. `factorial(5, 1)` → `factorial(4, 5)`
2. `factorial(4, 5)` → `factorial(3, 20)`
3. `factorial(3, 20)` → `factorial(2, 60)`
4. `factorial(2, 60)` → `factorial(1, 120)`
5. `factorial(1, 120)` → returns `120`

### **Example 2: Fibonacci Function**
```kotlin
tailrec fun fibonacci(n: Int, a: Int = 0, b: Int = 1): Int {
    return when (n) {
        0 -> a
        1 -> b
        else -> fibonacci(n - 1, b, a + b)
    }
}

// Usage
val fib10 = fibonacci(10)  // Returns 55
```

### **Example 3: Sum of Numbers**
```kotlin
tailrec fun sumUpTo(n: Int, accumulator: Int = 0): Int {
    return if (n <= 0) accumulator else sumUpTo(n - 1, accumulator + n)
}

// Usage
val sum = sumUpTo(100)  // Returns 5050
```

### **Example 4: List Processing**
```kotlin
tailrec fun <T> reverseList(
    list: List<T>, 
    accumulator: List<T> = emptyList()
): List<T> {
    return if (list.isEmpty()) {
        accumulator
    } else {
        reverseList(list.drop(1), listOf(list.first()) + accumulator)
    }
}

// Usage
val original = listOf(1, 2, 3, 4, 5)
val reversed = reverseList(original)  // Returns [5, 4, 3, 2, 1]
```

## ⚠️ Important Requirements

### **1. The Recursive Call Must Be Last**
```kotlin
// ❌ Won't work - computation after recursive call
tailrec fun factorial(n: Int): Int {
    return if (n <= 1) 1 else n * factorial(n - 1)  // Multiplication after call
}

// ✅ Will work - recursive call is last operation
tailrec fun factorial(n: Int, accumulator: Int = 1): Int {
    return if (n <= 1) accumulator else factorial(n - 1, n * accumulator)
}
```

### **2. No Additional Operations After Recursive Call**
```kotlin
// ❌ Won't work - additional operation after call
tailrec fun process(n: Int): Int {
    return if (n <= 0) 0 else {
        val result = process(n - 1)  // Recursive call
        result + 1  // Additional operation
    }
}

// ✅ Will work - no operations after recursive call
tailrec fun process(n: Int, accumulator: Int = 0): Int {
    return if (n <= 0) accumulator else process(n - 1, accumulator + 1)
}
```

### **3. Only Direct Recursive Calls**
```kotlin
// ❌ Won't work - indirect recursive call
tailrec fun functionA(n: Int): Int {
    return if (n <= 0) 0 else functionB(n - 1)
}

fun functionB(n: Int): Int {
    return if (n <= 0) 0 else functionA(n - 1)
}

// ✅ Will work - direct recursive call
tailrec fun functionA(n: Int, accumulator: Int = 0): Int {
    return if (n <= 0) accumulator else functionA(n - 1, accumulator + 1)
}
```

## 🎯 Best Practices

### **1. Use Accumulator Pattern**
```kotlin
// ✅ Good - uses accumulator for tail recursion
tailrec fun factorial(n: Int, accumulator: Int = 1): Int {
    return if (n <= 1) accumulator else factorial(n - 1, n * accumulator)
}

// ❌ Avoid - doesn't use accumulator
fun factorial(n: Int): Int {
    return if (n <= 1) 1 else n * factorial(n - 1)
}
```

### **2. Keep Functions Simple**
```kotlin
// ✅ Good - simple and clear
tailrec fun countDown(n: Int): Int {
    return if (n <= 0) 0 else countDown(n - 1)
}

// ❌ Avoid - complex logic in tailrec
tailrec fun complexFunction(n: Int, data: ComplexData): ComplexResult {
    // Complex processing logic...
    return if (n <= 0) data.result else complexFunction(n - 1, processData(data))
}
```

### **3. Document the Tailrec Nature**
```kotlin
/**
 * Calculates factorial using tail recursion for efficiency
 * @param n The number to calculate factorial for
 * @param accumulator Current accumulated result (internal use)
 * @return The factorial of n
 */
tailrec fun factorial(n: Int, accumulator: Int = 1): Int {
    return if (n <= 1) accumulator else factorial(n - 1, n * accumulator)
}
```

## 🔧 Practical Applications

### **1. Mathematical Calculations**
```kotlin
tailrec fun power(base: Int, exponent: Int, accumulator: Int = 1): Int {
    return if (exponent <= 0) accumulator else power(base, exponent - 1, base * accumulator)
}

tailrec fun gcd(a: Int, b: Int): Int {
    return if (b == 0) a else gcd(b, a % b)
}
```

### **2. List Processing**
```kotlin
tailrec fun <T> findElement(
    list: List<T>, 
    predicate: (T) -> Boolean, 
    index: Int = 0
): T? {
    return when {
        index >= list.size -> null
        predicate(list[index]) -> list[index]
        else -> findElement(list, predicate, index + 1)
    }
}
```

### **3. Tree Traversal**
```kotlin
data class TreeNode<T>(val value: T, val left: TreeNode<T>?, val right: TreeNode<T>?)

tailrec fun <T> findInTree(
    node: TreeNode<T>?, 
    target: T, 
    path: List<T> = emptyList()
): List<T>? {
    return when {
        node == null -> null
        node.value == target -> path + node.value
        else -> {
            val leftResult = findInTree(node.left, target, path + node.value)
            if (leftResult != null) leftResult else findInTree(node.right, target, path + node.value)
        }
    }
}
```

## 📚 Summary

**Tailrec functions** in Kotlin provide:
- **Stack overflow prevention** through compiler optimization
- **Performance improvement** by converting recursion to loops
- **Maintainable code** with recursive logic
- **Memory efficiency** through stack frame elimination

## 🎯 Key Takeaways

1. **Use `tailrec` keyword** for functions that can be optimized
2. **Recursive call must be last** operation in the function
3. **Use accumulator pattern** to make functions tail recursive
4. **No computation after** recursive calls
5. **Compiler handles optimization** automatically

## 🚀 Next Steps

- Practice converting regular recursive functions to tailrec
- Learn about other optimization techniques
- Explore functional programming patterns
- Understand compiler optimizations

---

**📁 Source Code:** [25_tailrec_function.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/25_tailrec_function.kt)

**🔗 Related Topics:**
- [Functions Basics](../functions/01-functions-basics.md)
- [Function Expressions](../functions/02-functions-as-expressions.md)
- [Default Parameters](../functions/06-default-parameters.md)
