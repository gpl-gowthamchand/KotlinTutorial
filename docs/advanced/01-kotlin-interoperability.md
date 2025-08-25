# 🔄 Kotlin-Java Interoperability

This lesson covers Kotlin-Java interoperability, which allows you to use Java code from Kotlin and vice versa. This is essential for working with existing Java libraries and gradually migrating Java projects to Kotlin.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Call Java code from Kotlin seamlessly
- ✅ Use Kotlin code from Java
- ✅ Handle null safety differences between languages
- ✅ Work with Java collections and Kotlin collections
- ✅ Apply best practices for interoperability

## 🔍 What You'll Learn

- **Java from Kotlin** - Calling Java methods and classes
- **Kotlin from Java** - Using Kotlin classes in Java
- **Null Safety** - Handling nullable types across languages
- **Collections** - Working with Java and Kotlin collections
- **Best Practices** - Guidelines for smooth interoperability

## 📝 Prerequisites

- Understanding of [Kotlin Basics](../basics/README.md)
- Knowledge of [Null Safety](../null-safety/01-null-safety.md)
- Familiarity with [Collections](../collections/README.md)
- Basic Java knowledge

## 💻 The Code

Let's examine the interoperability examples:

**📁 File:** [MyJavaFile.java](../src/MyJavaFile.java)
**📁 File:** [myKotlinInteroperability.kt](../src/myKotlinInteroperability.kt)

## 🔍 Code Breakdown

### **1. Calling Java from Kotlin**

#### **Basic Java Class Usage**
```kotlin
// Java class can be used directly in Kotlin
fun main() {
    val javaClass = MyJavaClass()
    
    // Call Java methods
    javaClass.setName("John Doe")
    javaClass.setAge(30)
    
    // Access Java properties (getters/setters)
    println("Name: ${javaClass.name}")
    println("Age: ${javaClass.age}")
    
    // Call Java methods with different signatures
    javaClass.printInfo()
    javaClass.printInfo("Custom prefix")
}
```

#### **Java Collections in Kotlin**
```kotlin
fun main() {
    // Java ArrayList
    val javaList = java.util.ArrayList<String>()
    javaList.add("Item 1")
    javaList.add("Item 2")
    
    // Use Kotlin collection functions
    val filtered = javaList.filter { it.contains("1") }
    val mapped = javaList.map { "Processed: $it" }
    
    println("Original: $javaList")
    println("Filtered: $filtered")
    println("Mapped: $mapped")
    
    // Convert to Kotlin collections
    val kotlinList = javaList.toList()
    val kotlinMutableList = javaList.toMutableList()
}
```

#### **Java Static Methods**
```kotlin
fun main() {
    // Call Java static methods
    val random = MyJavaClass.generateRandomNumber()
    val formatted = MyJavaClass.formatString("Hello", "World")
    
    println("Random number: $random")
    println("Formatted string: $formatted")
    
    // Access Java constants
    println("Max value: ${MyJavaClass.MAX_VALUE}")
    println("Default name: ${MyJavaClass.DEFAULT_NAME}")
}
```

### **2. Using Kotlin from Java**

#### **Kotlin Class in Java**
```java
public class JavaClient {
    public static void main(String[] args) {
        // Create Kotlin object
        MyKotlinClass kotlinObject = new MyKotlinClass("Kotlin", 42);
        
        // Call Kotlin methods
        String info = kotlinObject.getInfo();
        System.out.println("Info: " + info);
        
        // Access Kotlin properties
        String name = kotlinObject.getName();
        int value = kotlinObject.getValue();
        System.out.println("Name: " + name + ", Value: " + value);
        
        // Call Kotlin functions with default parameters
        String result = kotlinObject.processData("input", true);
        System.out.println("Result: " + result);
    }
}
```

#### **Kotlin Functions with Default Parameters**
```kotlin
class MyKotlinClass(val name: String, val value: Int) {
    fun getInfo(): String = "Name: $name, Value: $value"
    
    fun processData(input: String, verbose: Boolean = false): String {
        return if (verbose) {
            "Processing '$input' with verbose output"
        } else {
            "Processed: $input"
        }
    }
    
    fun getValue(): Int = value
}
```

### **3. Null Safety Interoperability**

#### **Java Nullable Types in Kotlin**
```kotlin
fun main() {
    val javaClass = MyJavaClass()
    
    // Java methods can return null
    val nullableString = javaClass.getNullableString()
    
    // Handle null safely
    if (nullableString != null) {
        println("String length: ${nullableString.length}")
    } else {
        println("String is null")
    }
    
    // Use safe call operator
    println("String length: ${nullableString?.length}")
    
    // Use Elvis operator for default value
    val safeString = nullableString ?: "Default string"
    println("Safe string: $safeString")
}
```

#### **Kotlin Non-Null Types in Java**
```kotlin
class KotlinService {
    fun getNonNullString(): String = "Always returns a string"
    
    fun getNullableString(): String? = null
    
    fun processString(input: String) {
        println("Processing: $input")
    }
}
```

```java
public class JavaClient {
    public static void main(String[] args) {
        KotlinService service = new KotlinService();
        
        // Kotlin non-null String becomes Java String
        String nonNull = service.getNonNullString();
        service.processString(nonNull); // Safe to call
        
        // Kotlin nullable String becomes Java String (with @Nullable annotation)
        String nullable = service.getNullableString();
        if (nullable != null) {
            service.processString(nullable);
        }
    }
}
```

### **4. Collection Interoperability**

#### **Java Collections in Kotlin**
```kotlin
fun main() {
    // Java HashMap
    val javaMap = java.util.HashMap<String, Int>()
    javaMap.put("one", 1)
    javaMap.put("two", 2)
    javaMap.put("three", 3)
    
    // Use Kotlin collection functions
    val filteredMap = javaMap.filter { (key, value) -> value > 1 }
    val keys = javaMap.keys.toList()
    val values = javaMap.values.toList()
    
    println("Original map: $javaMap")
    println("Filtered map: $filteredMap")
    println("Keys: $keys")
    println("Values: $values")
    
    // Convert to Kotlin collections
    val kotlinMap = javaMap.toMap()
    val kotlinMutableMap = javaMap.toMutableMap()
}
```

#### **Kotlin Collections in Java**
```kotlin
class KotlinCollectionProvider {
    fun getList(): List<String> = listOf("a", "b", "c")
    
    fun getMutableList(): MutableList<String> = mutableListOf("x", "y", "z")
    
    fun getMap(): Map<String, Int> = mapOf("one" to 1, "two" to 2)
    
    fun getSet(): Set<String> = setOf("alpha", "beta", "gamma")
}
```

```java
import java.util.List;
import java.util.Map;
import java.util.Set;

public class JavaCollectionClient {
    public static void main(String[] args) {
        KotlinCollectionProvider provider = new KotlinCollectionProvider();
        
        // Kotlin List becomes Java List
        List<String> list = provider.getList();
        System.out.println("List: " + list);
        
        // Kotlin MutableList becomes Java List
        List<String> mutableList = provider.getMutableList();
        mutableList.add("new");
        System.out.println("Mutable list: " + mutableList);
        
        // Kotlin Map becomes Java Map
        Map<String, Integer> map = provider.getMap();
        System.out.println("Map: " + map);
        
        // Kotlin Set becomes Java Set
        Set<String> set = provider.getSet();
        System.out.println("Set: " + set);
    }
}
```

### **5. Advanced Interoperability Patterns**

#### **Java Builder Pattern in Kotlin**
```kotlin
fun main() {
    // Use Java builder pattern
    val person = PersonBuilder()
        .setName("Jane Doe")
        .setAge(25)
        .setEmail("jane@example.com")
        .build()
    
    println("Person: $person")
    
    // Use Java fluent API
    val config = ConfigurationBuilder()
        .setHost("localhost")
        .setPort(8080)
        .setTimeout(5000)
        .build()
    
    println("Config: $config")
}
```

#### **Kotlin Extension Functions on Java Classes**
```kotlin
// Extend Java classes with Kotlin functions
fun java.util.ArrayList<String>.addIfNotExists(item: String): Boolean {
    return if (this.contains(item)) {
        false
    } else {
        this.add(item)
        true
    }
}

fun java.util.HashMap<String, Any>.getString(key: String): String? {
    return this[key] as? String
}

fun main() {
    val javaList = java.util.ArrayList<String>()
    javaList.addIfNotExists("first")
    javaList.addIfNotExists("second")
    javaList.addIfNotExists("first") // Won't add duplicate
    
    println("List: $javaList")
    
    val javaMap = java.util.HashMap<String, Any>()
    javaMap["name"] = "John"
    javaMap["age"] = 30
    
    val name = javaMap.getString("name")
    println("Name: $name")
}
```

#### **Java SAM (Single Abstract Method) Interfaces**
```kotlin
fun main() {
    // Java Runnable interface
    val runnable = java.lang.Runnable { println("Running from Kotlin") }
    
    // Java Thread with Kotlin lambda
    val thread = java.lang.Thread { println("Thread running") }
    thread.start()
    
    // Java Comparator
    val names = listOf("Charlie", "Alice", "Bob")
    val sortedNames = names.sortedWith(java.util.Comparator { a, b -> a.compareTo(b) })
    
    println("Sorted names: $sortedNames")
}
```

## 🎯 Key Concepts Explained

### **1. Type Mapping**

| Kotlin Type | Java Type | Notes |
|-------------|-----------|-------|
| `String` | `String` | Non-null String |
| `String?` | `String` | Nullable String (with annotations) |
| `Int` | `int` | Primitive int |
| `Int?` | `Integer` | Nullable Integer |
| `List<String>` | `List<String>` | Read-only list |
| `MutableList<String>` | `List<String>` | Mutable list |

### **2. Null Safety Differences**
- **Kotlin**: Compile-time null safety
- **Java**: Runtime null safety
- **Interop**: Kotlin nullable types become Java types with `@Nullable` annotations
- **Best Practice**: Always check for null when calling Java methods

### **3. Collection Differences**
- **Kotlin**: Read-only vs mutable collections
- **Java**: All collections are mutable
- **Interop**: Kotlin read-only collections become Java collections (mutable)

## 🧪 Running the Examples

### **Step 1: Open the Files**
1. Navigate to `src/MyJavaFile.java`
2. Navigate to `src/myKotlinInteroperability.kt`
3. Open them in IntelliJ IDEA

### **Step 2: Run the Programs**
1. Right-click on the Kotlin file
2. Select "Run 'myKotlinInteroperabilityKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Java Library Integration**
Create a Kotlin program that uses Java libraries like Apache Commons.

**Solution:**
```kotlin
import org.apache.commons.lang3.StringUtils
import java.util.Random

fun main() {
    // Use Java Random class
    val random = Random()
    val randomNumber = random.nextInt(100)
    println("Random number: $randomNumber")
    
    // Use Apache Commons StringUtils
    val text = "  hello world  "
    val trimmed = StringUtils.trim(text)
    val capitalized = StringUtils.capitalize(trimmed)
    val reversed = StringUtils.reverse(capitalized)
    
    println("Original: '$text'")
    println("Trimmed: '$trimmed'")
    println("Capitalized: '$capitalized'")
    println("Reversed: '$reversed'")
    
    // Use Java Collections
    val javaList = java.util.ArrayList<String>()
    javaList.add("item1")
    javaList.add("item2")
    
    // Convert to Kotlin and use Kotlin functions
    val kotlinList = javaList.toList()
    val processed = kotlinList.map { "Processed: $it" }
    println("Processed: $processed")
}
```

### **Exercise 2: Kotlin Service in Java**
Create a Kotlin service that can be easily used from Java.

**Solution:**
```kotlin
// Kotlin service designed for Java interop
class UserService {
    private val users = mutableMapOf<String, User>()
    
    fun createUser(name: String, email: String): User {
        val user = User(name, email)
        users[email] = user
        return user
    }
    
    fun getUser(email: String): User? = users[email]
    
    fun getAllUsers(): List<User> = users.values.toList()
    
    fun updateUser(email: String, newName: String): Boolean {
        val user = users[email] ?: return false
        users[email] = user.copy(name = newName)
        return true
    }
    
    fun deleteUser(email: String): Boolean {
        return users.remove(email) != null
    }
}

data class User(val name: String, val email: String)
```

```java
// Java client using Kotlin service
public class JavaUserClient {
    public static void main(String[] args) {
        UserService service = new UserService();
        
        // Create users
        User user1 = service.createUser("John Doe", "john@example.com");
        User user2 = service.createUser("Jane Smith", "jane@example.com");
        
        System.out.println("Created users: " + user1 + ", " + user2);
        
        // Get all users
        List<User> allUsers = service.getAllUsers();
        System.out.println("All users: " + allUsers);
        
        // Update user
        boolean updated = service.updateUser("john@example.com", "John Updated");
        System.out.println("Update successful: " + updated);
        
        // Get updated user
        User updatedUser = service.getUser("john@example.com");
        System.out.println("Updated user: " + updatedUser);
    }
}
```

### **Exercise 3: Collection Interoperability**
Create a program that demonstrates collection interoperability.

**Solution:**
```kotlin
fun main() {
    // Java collections
    val javaArrayList = java.util.ArrayList<Int>()
    val javaHashMap = java.util.HashMap<String, Int>()
    
    // Populate Java collections
    for (i in 1..5) {
        javaArrayList.add(i * i)
        javaHashMap["key$i"] = i
    }
    
    println("Java ArrayList: $javaArrayList")
    println("Java HashMap: $javaHashMap")
    
    // Convert to Kotlin collections
    val kotlinList = javaArrayList.toList()
    val kotlinMap = javaHashMap.toMap()
    
    // Use Kotlin collection functions
    val filteredList = kotlinList.filter { it > 10 }
    val transformedMap = kotlinMap.mapValues { (key, value) -> value * 2 }
    
    println("Filtered list (>10): $filteredList")
    println("Transformed map (values * 2): $transformedMap")
    
    // Convert back to Java collections
    val backToJavaList = kotlinList.toMutableList()
    val backToJavaMap = kotlinMap.toMutableMap()
    
    // Use Java collection methods
    backToJavaList.add(36)
    backToJavaMap.put("newKey", 100)
    
    println("Modified Java list: $backToJavaList")
    println("Modified Java map: $backToJavaMap")
}
```

### **Exercise 4: Null Safety Bridge**
Create a system that safely bridges null safety between Kotlin and Java.

**Solution:**
```kotlin
// Kotlin class with null safety
class SafeDataProcessor {
    fun processData(data: String): String {
        return "Processed: $data"
    }
    
    fun processNullableData(data: String?): String? {
        return data?.let { "Processed: $it" }
    }
    
    fun getDefaultValue(): String = "Default value"
    
    fun getNullableValue(): String? = null
}

// Java-friendly wrapper
class JavaFriendlyWrapper {
    private val processor = SafeDataProcessor()
    
    fun processData(data: String): String {
        return processor.processData(data)
    }
    
    fun processNullableData(data: String?): String {
        return processor.processNullableData(data) ?: "No data provided"
    }
    
    fun getDefaultValue(): String = processor.getDefaultValue()
    
    fun getNullableValue(): String? = processor.getNullableValue()
}
```

```java
public class JavaNullSafetyClient {
    public static void main(String[] args) {
        JavaFriendlyWrapper wrapper = new JavaFriendlyWrapper();
        
        // Safe non-null operations
        String result1 = wrapper.processData("Hello");
        System.out.println("Result 1: " + result1);
        
        // Handle nullable data safely
        String result2 = wrapper.processNullableData("World");
        System.out.println("Result 2: " + result2);
        
        String result3 = wrapper.processNullableData(null);
        System.out.println("Result 3: " + result3);
        
        // Get values
        String defaultValue = wrapper.getDefaultValue();
        System.out.println("Default: " + defaultValue);
        
        String nullableValue = wrapper.getNullableValue();
        if (nullableValue != null) {
            System.out.println("Nullable: " + nullableValue);
        } else {
            System.out.println("Nullable value is null");
        }
    }
}
```

## 🚨 Common Mistakes to Avoid

1. **Ignoring null safety**: Always check for null when calling Java methods ✅
2. **Collection mutability**: Remember that Java collections are always mutable ✅
3. **Type mismatches**: Be aware of primitive vs wrapper type differences ✅
4. **Forgetting annotations**: Use proper annotations for Java interop ✅

## 🎯 What's Next?

Now that you understand Kotlin-Java interoperability, continue with:

1. **Advanced Coroutines** → [Coroutines Introduction](../coroutines/01-introduction.md)
2. **Functional Programming** → [Lambdas and Higher-Order Functions](../functional-programming/01-lambdas.md)
3. **Collections** → [Collections Overview](../collections/README.md)
4. **Advanced OOP** → [Enums and Sealed Classes](../oop/07-enums-sealed-classes.md)

## 📚 Additional Resources

- [Official Kotlin-Java Interop Guide](https://kotlinlang.org/docs/java-interop.html)
- [Calling Java from Kotlin](https://kotlinlang.org/docs/java-interop.html#calling-java-code-from-kotlin)
- [Calling Kotlin from Java](https://kotlinlang.org/docs/java-interop.html#calling-kotlin-code-from-java)

## 🏆 Summary

- ✅ You can call Java code from Kotlin seamlessly
- ✅ You know how to use Kotlin code from Java
- ✅ You understand how to handle null safety differences
- ✅ You can work with Java collections and Kotlin collections
- ✅ You're ready to apply best practices for interoperability!

**Kotlin-Java interoperability is essential for real-world development. Master it for seamless integration with existing Java codebases! 🎉**
