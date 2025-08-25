# 🔗 Infix Functions in Kotlin

Infix functions are a special type of function in Kotlin that allows you to call functions using a more natural, operator-like syntax. They make your code more readable and expressive.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what infix functions are
- ✅ Create your own infix functions
- ✅ Use infix functions effectively
- ✅ Know the limitations and best practices
- ✅ Apply infix functions in real-world scenarios

## 🔍 What You'll Learn

- **Infix function syntax** - How to declare and use infix functions
- **Operator-like calls** - Calling functions without dots and parentheses
- **Use cases** - When and where to use infix functions
- **Limitations** - Understanding the constraints of infix functions
- **Best practices** - Guidelines for effective usage

## 📝 Prerequisites

- ✅ Basic understanding of functions in Kotlin
- ✅ Knowledge of function parameters and return types
- ✅ Familiarity with Kotlin syntax

## 💻 The Code

Let's examine the infix functions examples:

**📁 File:** [24_infix_function.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/24_infix_function.kt)

## 🔍 Code Breakdown

### **Basic Infix Function Declaration**
```kotlin
infix fun Int.times(str: String) = str.repeat(this)
```

**Key Components:**
- `infix` - Keyword that makes the function infix
- `fun` - Function declaration keyword
- `Int.times` - Extension function on Int type
- `str: String` - Parameter of type String
- `str.repeat(this)` - Function body using the receiver object

### **Infix Function Call**
```kotlin
// Regular function call
3.times("Hello ")

// Infix function call (more natural)
3 times "Hello "
```

## 🎯 Key Concepts Explained

### **1. What Makes a Function Infix?**

An infix function must:
- Be a **member function** or an **extension function**
- Have **exactly one parameter**
- Be marked with the `infix` keyword
- Not have default parameter values
- Not be a vararg function

### **2. Infix vs Regular Function Calls**

| Regular Call | Infix Call | Description |
|--------------|------------|-------------|
| `a.plus(b)` | `a plus b` | Addition operation |
| `str.repeat(n)` | `str repeat n` | String repetition |
| `list.add(item)` | `list add item` | List addition |

### **3. Common Use Cases**

#### **Mathematical Operations**
```kotlin
infix fun Int.pow(exponent: Int): Int {
    return this.toDouble().pow(exponent.toDouble()).toInt()
}

// Usage
val result = 2 pow 3  // Returns 8
```

#### **String Operations**
```kotlin
infix fun String.repeat(times: Int): String {
    return this.repeat(times)
}

// Usage
val repeated = "Hello " repeat 3  // Returns "Hello Hello Hello "
```

#### **Collection Operations**
```kotlin
infix fun <T> MutableList<T>.add(item: T) {
    this.add(item)
}

// Usage
val list = mutableListOf<String>()
list add "First"
list add "Second"
```

## 🧪 Examples and Exercises

### **Example 1: Custom Infix Function**
```kotlin
infix fun String.containsIgnoreCase(other: String): Boolean {
    return this.contains(other, ignoreCase = true)
}

// Usage
val text = "Hello World"
val contains = text containsIgnoreCase "world"  // true
```

### **Example 2: Range Creation**
```kotlin
infix fun Int.until(end: Int): IntRange {
    return this until end
}

// Usage
val range = 1 until 5  // Creates range 1..4
```

### **Example 3: Pair Creation**
```kotlin
infix fun <A, B> A.to(that: B): Pair<A, B> = Pair(this, that)

// Usage
val pair = "key" to "value"  // Creates Pair("key", "value")
```

## ⚠️ Limitations and Considerations

### **1. Parameter Constraints**
```kotlin
// ❌ Won't work - multiple parameters
infix fun Int.operation(a: Int, b: Int) = this + a + b

// ❌ Won't work - default parameter
infix fun Int.operation(a: Int = 0) = this + a

// ❌ Won't work - vararg parameter
infix fun Int.operation(vararg items: Int) = this + items.sum()

// ✅ Will work - single parameter, no defaults
infix fun Int.operation(a: Int) = this + a
```

### **2. Precedence and Associativity**
```kotlin
infix fun Int.add(other: Int) = this + other
infix fun Int.multiply(other: Int) = this * other

// Be careful with operator precedence
val result = 2 add 3 multiply 4  // Result: 14 (not 20)
// Equivalent to: 2.add(3.multiply(4))
```

## 🎯 Best Practices

### **1. Use for Simple Operations**
```kotlin
// ✅ Good - simple, clear operation
infix fun String.append(other: String) = this + other

// ❌ Avoid - complex logic in infix
infix fun String.processComplex(other: String): String {
    // Complex processing logic...
    return processedResult
}
```

### **2. Maintain Readability**
```kotlin
// ✅ Good - clear meaning
infix fun Int.isDivisibleBy(other: Int) = this % other == 0

// ❌ Avoid - unclear meaning
infix fun Int.x(other: Int) = this * other
```

### **3. Follow Kotlin Conventions**
```kotlin
// ✅ Good - follows Kotlin naming
infix fun Int.times(str: String) = str.repeat(this)

// ❌ Avoid - non-Kotlin style
infix fun Int.multiplyString(str: String) = str.repeat(this)
```

## 🔧 Practical Applications

### **1. DSL (Domain Specific Language)**
```kotlin
class Configuration {
    infix fun set(key: String, value: Any) {
        // Set configuration value
    }
}

val config = Configuration()
config set ("timeout", 5000)
```

### **2. Testing Frameworks**
```kotlin
infix fun String.should(condition: String) {
    // Assertion logic
}

"Hello" should "contain 'H'"
```

### **3. Custom Operators**
```kotlin
infix fun Int.`+`(other: Int) = this + other * 2

val result = 5 `+` 3  // Returns 11 (5 + 3*2)
```

## 📚 Summary

**Infix functions** are a powerful feature in Kotlin that:
- Make function calls more natural and readable
- Are useful for simple, single-parameter operations
- Follow specific rules and limitations
- Can improve code expressiveness when used appropriately

## 🎯 Key Takeaways

1. **Use `infix` keyword** for functions that benefit from operator-like syntax
2. **Single parameter only** - infix functions can't have multiple parameters
3. **Extension functions** work great with infix notation
4. **Maintain readability** - don't overuse infix functions
5. **Follow conventions** - use clear, descriptive names

## 🚀 Next Steps

- Practice creating your own infix functions
- Explore the standard library infix functions
- Learn about operator overloading
- Understand function precedence and associativity

---

**📁 Source Code:** [24_infix_function.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/24_infix_function.kt)

**🔗 Related Topics:**
- [Functions Basics](../functions/01-functions-basics.md)
- [Extension Functions](../functions/04-extension-functions.md)
- [Function Expressions](../functions/02-functions-as-expressions.md)
