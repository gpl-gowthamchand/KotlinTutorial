# 🛡️ Null Safety in Kotlin

Null safety is one of Kotlin's most powerful features, designed to eliminate the dreaded `NullPointerException` that plagues many Java applications. Kotlin's type system distinguishes between nullable and non-nullable types, making your code safer and more predictable.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand the difference between nullable and non-nullable types
- ✅ Use safe call operators (`?.`) and null coalescing (`?:`)
- ✅ Implement null checks and smart casts
- ✅ Work with safe casting (`as?`)
- ✅ Use the `!!` operator safely and understand its risks

## 🔍 What You'll Learn

- **Type system** - How Kotlin distinguishes nullable from non-nullable types
- **Safe operators** - Using `?.`, `?:`, and `as?` safely
- **Null checks** - Implementing proper null checking strategies
- **Smart casts** - How Kotlin automatically handles null checks
- **Best practices** - When and how to use different null safety approaches

## 📝 Prerequisites

- Understanding of [Variables and Data Types](../basics/02-variables-data-types.md)
- Knowledge of [Functions](../functions/01-functions-basics.md)
- Familiarity with [Control Flow](../control-flow/01-if-expressions.md)

## 💻 The Code

Let's examine the null safety examples:

**📁 File:** [46_null_safety.kt](../src/46_null_safety.kt)

## 🔍 Code Breakdown

### **1. Nullable vs Non-Nullable Types**

#### **Non-Nullable Types (Default)**
```kotlin
// These variables cannot hold null values
val name: String = "Alice"           // Non-nullable String
val age: Int = 25                    // Non-nullable Int
val isStudent: Boolean = true        // Non-nullable Boolean

// This would cause a compilation error:
// val name: String = null  // ❌ Compilation error
```

#### **Nullable Types (Explicit Declaration)**
```kotlin
// These variables can hold null values
val nullableName: String? = "Alice"  // Nullable String
val nullableAge: Int? = 25           // Nullable Int
val nullableStudent: Boolean? = true // Nullable Boolean

// They can also be assigned null:
val nullName: String? = null         // ✅ Valid
val nullAge: Int? = null            // ✅ Valid
```

### **2. Safe Call Operator (`?.`)**

#### **Basic Safe Call**
```kotlin
val name: String? = "Alice"
val length = name?.length            // Safe call - returns Int? (nullable)

val nullName: String? = null
val nullLength = nullName?.length    // Safe call - returns null
```

#### **Chaining Safe Calls**
```kotlin
data class Person(val name: String?, val address: Address?)
data class Address(val street: String?, val city: String?)

val person: Person? = Person("Alice", Address("Main St", "New York"))
val city = person?.address?.city     // Safe call chain

val nullPerson: Person? = null
val nullCity = nullPerson?.address?.city  // Returns null safely
```

#### **Safe Call with Functions**
```kotlin
val name: String? = "Alice"
val upperName = name?.uppercase()    // Safe call to function

val nullName: String? = null
val upperNullName = nullName?.uppercase()  // Returns null safely
```

### **3. Null Coalescing Operator (`?:`)**

#### **Basic Null Coalescing**
```kotlin
val name: String? = "Alice"
val displayName = name ?: "Unknown"  // Use "Unknown" if name is null

val nullName: String? = null
val displayNullName = nullName ?: "Unknown"  // Returns "Unknown"
```

#### **Null Coalescing with Expressions**
```kotlin
val name: String? = null
val length = name?.length ?: 0       // Use 0 if name or length is null

val age: Int? = null
val status = age?.let { if (it >= 18) "Adult" else "Minor" } ?: "Unknown"
```

#### **Null Coalescing in Function Calls**
```kotlin
fun greet(name: String?) {
    val displayName = name ?: "Guest"
    println("Hello, $displayName!")
}

greet("Alice")    // Prints: Hello, Alice!
greet(null)       // Prints: Hello, Guest!
```

### **4. Null Checks and Smart Casts**

#### **Explicit Null Check**
```kotlin
fun processName(name: String?) {
    if (name != null) {
        // Kotlin knows name is not null in this block
        println("Name length: ${name.length}")  // Safe to call .length
        println("Uppercase: ${name.uppercase()}")  // Safe to call .uppercase()
    } else {
        println("Name is null")
    }
}
```

#### **Smart Cast with When Expression**
```kotlin
fun describeValue(value: Any?) {
    when (value) {
        null -> println("Value is null")
        is String -> println("String: ${value.length} characters")  // Smart cast to String
        is Int -> println("Integer: ${value + 10}")                 // Smart cast to Int
        is Boolean -> println("Boolean: ${value.not()}")            // Smart cast to Boolean
        else -> println("Other type: ${value.javaClass.simpleName}")
    }
}
```

#### **Smart Cast with Elvis Operator**
```kotlin
fun getLength(value: String?): Int {
    return value?.length ?: 0
}

fun getLengthAlternative(value: String?): Int {
    return if (value != null) value.length else 0  // Smart cast in if block
}
```

### **5. Safe Casting (`as?`)**

#### **Safe Cast Operator**
```kotlin
val anyValue: Any = "Hello"
val stringValue = anyValue as? String    // Safe cast to String
val intValue = anyValue as? Int          // Safe cast to Int (returns null)

println(stringValue)  // "Hello"
println(intValue)     // null
```

#### **Safe Cast with Null Coalescing**
```kotlin
val anyValue: Any = "42"
val intValue = (anyValue as? String)?.toIntOrNull() ?: 0

val nullValue: Any? = null
val safeInt = (nullValue as? String)?.toIntOrNull() ?: 0
```

### **6. The `!!` Operator (Use with Caution)**

#### **Non-Null Assertion**
```kotlin
val name: String? = "Alice"
val length = name!!.length  // Asserts name is not null

val nullName: String? = null
// val nullLength = nullName!!.length  // ❌ Throws NullPointerException at runtime
```

#### **When to Use `!!`**
```kotlin
// Only use !! when you're absolutely certain the value is not null
fun processNonNullName(name: String?) {
    requireNotNull(name) { "Name cannot be null" }  // Better than !!
    
    // Now Kotlin knows name is not null
    println("Processing: ${name.length}")  // Safe to use
}
```

### **7. Collection Null Safety**

#### **Nullable Collections**
```kotlin
val nullableList: List<String>? = listOf("Alice", "Bob")
val size = nullableList?.size ?: 0

val nullList: List<String>? = null
val safeSize = nullList?.size ?: 0
```

#### **Collections with Nullable Elements**
```kotlin
val names: List<String?> = listOf("Alice", null, "Bob", null, "Charlie")

// Filter out null values
val nonNullNames = names.filterNotNull()  // ["Alice", "Bob", "Charlie"]

// Safe processing
names.forEach { name ->
    name?.let { println("Name: $it") }  // Only print non-null names
}
```

## 🎯 Key Concepts Explained

### **1. Type System Safety**
```kotlin
// Kotlin's type system prevents null assignment to non-nullable types
var name: String = "Alice"  // Non-nullable
// name = null  // ❌ Compilation error

var nullableName: String? = "Alice"  // Nullable
nullableName = null  // ✅ Valid
```

### **2. Smart Casts**
```kotlin
fun example(value: String?) {
    if (value != null) {
        // Kotlin automatically casts value to non-nullable String
        val length = value.length  // Safe to use
        val upper = value.uppercase()  // Safe to use
    }
    // Outside this block, value is still nullable
}
```

### **3. Safe Call vs Null Check**
```kotlin
val name: String? = "Alice"

// Safe call - concise but returns nullable result
val length1 = name?.length  // Int?

// Null check - more verbose but gives non-nullable result
val length2 = if (name != null) name.length else 0  // Int
```

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/46_null_safety.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '46_null_safetyKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Safe String Processing**
Create functions that safely process nullable strings.

**Solution:**
```kotlin
fun processString(input: String?): String {
    return input?.trim()?.uppercase() ?: "DEFAULT"
}

fun getStringLength(input: String?): Int {
    return input?.length ?: 0
}

fun main() {
    println(processString("  hello world  "))  // "HELLO WORLD"
    println(processString(null))               // "DEFAULT"
    
    println(getStringLength("Hello"))          // 5
    println(getStringLength(null))             // 0
}
```

### **Exercise 2: Nullable Person Processing**
Create a Person class with nullable fields and process them safely.

**Solution:**
```kotlin
data class Person(
    val name: String?,
    val age: Int?,
    val email: String?
)

fun processPerson(person: Person?): String {
    if (person == null) return "No person data"
    
    val name = person.name ?: "Unknown"
    val age = person.age?.toString() ?: "Unknown"
    val email = person.email ?: "No email"
    
    return "Name: $name, Age: $age, Email: $email"
}

fun main() {
    val person1 = Person("Alice", 25, "alice@email.com")
    val person2 = Person("Bob", null, null)
    val person3 = Person(null, 30, "bob@email.com")
    
    println(processPerson(person1))  // "Name: Alice, Age: 25, Email: alice@email.com"
    println(processPerson(person2))  // "Name: Bob, Age: Unknown, Email: No email"
    println(processPerson(person3))  // "Name: Unknown, Age: 30, Email: bob@email.com"
    println(processPerson(null))     // "No person data"
}
```

### **Exercise 3: Safe Collection Processing**
Process collections that may contain null values.

**Solution:**
```kotlin
fun processNullableList(list: List<String?>?): List<String> {
    return list?.filterNotNull()?.map { it.uppercase() } ?: emptyList()
}

fun safeListOperations(list: List<Int?>?): Map<String, Any> {
    if (list == null) return mapOf("error" to "List is null")
    
    val nonNullNumbers = list.filterNotNull()
    if (nonNullNumbers.isEmpty()) return mapOf("error" to "No valid numbers")
    
    return mapOf(
        "count" to nonNullNumbers.size,
        "sum" to nonNullNumbers.sum(),
        "average" to nonNullNumbers.average(),
        "min" to nonNullNumbers.minOrNull() ?: 0,
        "max" to nonNullNumbers.maxOrNull() ?: 0
    )
}

fun main() {
    val list1 = listOf("hello", null, "world", null, "kotlin")
    val list2: List<String?>? = null
    val list3: List<Int?>? = listOf(1, null, 3, null, 5)
    
    println(processNullableList(list1))  // [HELLO, WORLD, KOTLIN]
    println(processNullableList(list2))  // []
    
    println(safeListOperations(list3))   // {count=3, sum=9.0, average=3.0, min=1, max=5}
}
```

### **Exercise 4: Complex Null Safety**
Handle complex nested nullable structures.

**Solution:**
```kotlin
data class Address(val street: String?, val city: String?, val country: String?)
data class Contact(val phone: String?, val email: String?)
data class Employee(val name: String?, val address: Address?, val contact: Contact?)

fun getEmployeeInfo(employee: Employee?): String {
    return employee?.let { emp ->
        val name = emp.name ?: "Unknown"
        val street = emp.address?.street ?: "No street"
        val city = emp.address?.city ?: "No city"
        val phone = emp.contact?.phone ?: "No phone"
        val email = emp.contact?.email ?: "No email"
        
        "Employee: $name\nAddress: $street, $city\nContact: $phone, $email"
    } ?: "No employee data"
}

fun main() {
    val employee1 = Employee(
        "Alice",
        Address("Main St", "New York", "USA"),
        Contact("123-456-7890", "alice@company.com")
    )
    
    val employee2 = Employee(
        "Bob",
        Address(null, "Boston", null),
        Contact(null, null)
    )
    
    println(getEmployeeInfo(employee1))
    println("\n" + getEmployeeInfo(employee2))
    println("\n" + getEmployeeInfo(null))
}
```

## 🚨 Common Mistakes to Avoid

1. **Using `!!` without null checks**: Can cause runtime exceptions ❌
   - **Better**: Use safe calls or explicit null checks ✅

2. **Forgetting nullable types**: Always consider if a value can be null ✅

3. **Ignoring smart casts**: Let Kotlin handle type safety automatically ✅

4. **Not using safe operators**: `?.` and `?:` make code more readable ✅

## 🎯 What's Next?

Now that you understand null safety, continue with:

1. **Lateinit and Lazy** → [Lateinit and Lazy Keywords](02-lateinit-lazy.md)
2. **Scope functions** → [Scope Functions](../functional-programming/02-scope-functions.md)
3. **Collections** → [Collections Overview](../collections/README.md)
4. **Coroutines** → [Coroutines](../coroutines/01-introduction.md)

## 📚 Additional Resources

- [Official Kotlin Null Safety Documentation](https://kotlinlang.org/docs/null-safety.html)
- [Kotlin Type System](https://kotlinlang.org/docs/types.html)
- [Safe Calls and Elvis Operator](https://kotlinlang.org/docs/null-safety.html#safe-calls)

## 🏆 Summary

- ✅ You understand nullable vs non-nullable types
- ✅ You can use safe call operators (`?.`) safely
- ✅ You know how to implement null checks and smart casts
- ✅ You understand when to use the `!!` operator (rarely!)
- ✅ You're ready to write safer, more robust Kotlin code!

**Null safety is one of Kotlin's greatest strengths. Use it to eliminate null pointer exceptions! 🎉**
