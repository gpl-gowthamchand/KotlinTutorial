# 🔍 Predicates in Kotlin

This lesson covers predicates in Kotlin - functions that return boolean values and are commonly used with collections for filtering, searching, and validation operations.

## 📋 Learning Objectives

By the end of this lesson, you will be able to:
- ✅ Understand what predicates are and how they work
- ✅ Use predicates with collection functions like filter, any, all, none
- ✅ Create custom predicates for complex conditions
- ✅ Chain predicates for sophisticated filtering
- ✅ Apply predicates in real-world scenarios

## 🔍 What You'll Learn

- **Predicate Basics** - What predicates are and their syntax
- **Collection Predicates** - Using predicates with filter, any, all, none
- **Custom Predicates** - Creating your own predicate functions
- **Predicate Chaining** - Combining multiple predicates
- **Real-world Applications** - Practical use cases and patterns

## 📝 Prerequisites

- Understanding of [Lambdas and Higher-Order Functions](01-lambdas.md)
- Knowledge of [Collections Overview](../collections/README.md)
- Familiarity with [Control Flow](../control-flow/README.md)

## 💻 The Code

Let's examine the predicate examples:

**📁 File:** [45_predicate.kt](https://github.com/gpl-gowthamchand/KotlinTutorial/blob/feature/documentation-improvements/src/45_predicate.kt)

## 🔍 Code Breakdown

### **1. Basic Predicates**

#### **Simple Predicates**
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    // Predicate: is even
    val isEven: (Int) -> Boolean = { it % 2 == 0 }
    
    // Predicate: is greater than 5
    val isGreaterThan5: (Int) -> Boolean = { it > 5 }
    
    // Predicate: is prime
    val isPrime: (Int) -> Boolean = { num ->
        if (num < 2) false
        else (2..num / 2).none { num % it == 0 }
    }
    
    println("Even numbers: ${numbers.filter(isEven)}")
    println("Numbers > 5: ${numbers.filter(isGreaterThan5)}")
    println("Prime numbers: ${numbers.filter(isPrime)}")
}
```

#### **Predicate with Multiple Parameters**
```kotlin
fun main() {
    val people = listOf(
        Person("Alice", 25, "Engineer"),
        Person("Bob", 30, "Manager"),
        Person("Charlie", 22, "Developer"),
        Person("Diana", 35, "Designer")
    )
    
    // Predicate: person is young (under 30)
    val isYoung: (Person) -> Boolean = { it.age < 30 }
    
    // Predicate: person is in tech role
    val isInTech: (Person) -> Boolean = { person ->
        person.role in listOf("Engineer", "Developer", "Designer")
    }
    
    // Predicate: person meets both criteria
    val isYoungAndInTech: (Person) -> Boolean = { person ->
        isYoung(person) && isInTech(person)
    }
    
    println("Young people: ${people.filter(isYoung)}")
    println("Tech people: ${people.filter(isInTech)}")
    println("Young tech people: ${people.filter(isYoungAndInTech)}")
}

data class Person(val name: String, val age: Int, val role: String)
```

### **2. Collection Predicates**

#### **Filter with Predicates**
```kotlin
fun main() {
    val words = listOf("apple", "banana", "cherry", "date", "elderberry", "fig")
    
    // Predicate: word starts with specific letter
    val startsWith = { letter: Char -> { word: String -> word.startsWith(letter) } }
    
    // Predicate: word has specific length
    val hasLength = { length: Int -> { word: String -> word.length == length } }
    
    // Predicate: word contains specific substring
    val contains = { substring: String -> { word: String -> word.contains(substring) } }
    
    println("Words starting with 'a': ${words.filter(startsWith('a'))}")
    println("Words with 5 letters: ${words.filter(hasLength(5))}")
    println("Words containing 'er': ${words.filter(contains("er"))}")
}
```

#### **Any, All, None with Predicates**
```kotlin
fun main() {
    val numbers = listOf(2, 4, 6, 8, 10, 12, 14, 16, 18, 20)
    
    // Predicate: number is even
    val isEven: (Int) -> Boolean = { it % 2 == 0 }
    
    // Predicate: number is divisible by 4
    val isDivisibleBy4: (Int) -> Boolean = { it % 4 == 0 }
    
    // Predicate: number is greater than 15
    val isGreaterThan15: (Int) -> Boolean = { it > 15 }
    
    println("All numbers are even: ${numbers.all(isEven)}")
    println("Any number is divisible by 4: ${numbers.any(isDivisibleBy4)}")
    println("No number is greater than 15: ${numbers.none(isGreaterThan15)}")
    println("All numbers are divisible by 4: ${numbers.all(isDivisibleBy4)}")
}
```

#### **Find and FindLast with Predicates**
```kotlin
fun main() {
    val products = listOf(
        Product("Laptop", 999.99, "Electronics"),
        Product("Mouse", 29.99, "Electronics"),
        Product("Book", 19.99, "Books"),
        Product("Chair", 199.99, "Furniture"),
        Product("Pen", 2.99, "Office")
    )
    
    // Predicate: product is expensive (> $100)
    val isExpensive: (Product) -> Boolean = { it.price > 100.0 }
    
    // Predicate: product is in electronics category
    val isElectronics: (Product) -> Boolean = { it.category == "Electronics" }
    
    // Predicate: product is affordable (< $50)
    val isAffordable: (Product) -> Boolean = { it.price < 50.0 }
    
    val firstExpensive = products.find(isExpensive)
    val lastElectronics = products.findLast(isElectronics)
    val firstAffordable = products.find(isAffordable)
    
    println("First expensive product: $firstExpensive")
    println("Last electronics product: $lastElectronics")
    println("First affordable product: $firstAffordable")
}

data class Product(val name: String, val price: Double, val category: String)
```

### **3. Custom Predicates**

#### **Complex Predicates**
```kotlin
fun main() {
    val students = listOf(
        Student("Alice", 85, listOf("Math", "Physics", "Chemistry")),
        Student("Bob", 92, listOf("Math", "English", "History")),
        Student("Charlie", 78, listOf("Physics", "Chemistry", "Biology")),
        Student("Diana", 95, listOf("Math", "Physics", "English")),
        Student("Eve", 88, listOf("Chemistry", "Biology", "Math"))
    )
    
    // Predicate: student is high achiever (grade > 90)
    val isHighAchiever: (Student) -> Boolean = { it.grade > 90 }
    
    // Predicate: student studies math
    val studiesMath: (Student) -> Boolean = { it.subjects.contains("Math") }
    
    // Predicate: student has balanced subjects (mix of sciences and humanities)
    val hasBalancedSubjects: (Student) -> Boolean = { student ->
        val sciences = listOf("Math", "Physics", "Chemistry", "Biology")
        val humanities = listOf("English", "History", "Literature")
        
        val scienceCount = student.subjects.count { it in sciences }
        val humanitiesCount = student.subjects.count { it in humanities }
        
        scienceCount > 0 && humanitiesCount > 0
    }
    
    // Predicate: student is math high achiever
    val isMathHighAchiever: (Student) -> Boolean = { student ->
        isHighAchiever(student) && studiesMath(student)
    }
    
    println("High achievers: ${students.filter(isHighAchiever)}")
    println("Math students: ${students.filter(studiesMath)}")
    println("Balanced students: ${students.filter(hasBalancedSubjects)}")
    println("Math high achievers: ${students.filter(isMathHighAchiever)}")
}

data class Student(val name: String, val grade: Int, val subjects: List<String>)
```

#### **Predicate Factories**
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15)
    
    // Predicate factory: creates range predicate
    fun inRange(min: Int, max: Int): (Int) -> Boolean = { it in min..max }
    
    // Predicate factory: creates multiple predicate
    fun isMultipleOf(factor: Int): (Int) -> Boolean = { it % factor == 0 }
    
    // Predicate factory: creates comparison predicate
    fun compareWith(operator: String, value: Int): (Int) -> Boolean = { num ->
        when (operator) {
            ">" -> num > value
            ">=" -> num >= value
            "<" -> num < value
            "<=" -> num <= value
            "==" -> num == value
            "!=" -> num != value
            else -> false
        }
    }
    
    // Predicate factory: creates composite predicate
    fun <T> and(vararg predicates: (T) -> Boolean): (T) -> Boolean = { item ->
        predicates.all { it(item) }
    }
    
    fun <T> or(vararg predicates: (T) -> Boolean): (T) -> Boolean = { item ->
        predicates.any { it(item) }
    }
    
    fun <T> not(predicate: (T) -> Boolean): (T) -> Boolean = { item ->
        !predicate(item)
    }
    
    val inRange5to10 = inRange(5, 10)
    val isMultipleOf3 = isMultipleOf(3)
    val isGreaterThan7 = compareWith(">", 7)
    
    // Composite predicates
    val inRangeAndMultipleOf3 = and(inRange5to10, isMultipleOf3)
    val greaterThan7OrMultipleOf5 = or(isGreaterThan7, isMultipleOf(5))
    val notInRange5to10 = not(inRange5to10)
    
    println("Numbers in range 5-10: ${numbers.filter(inRange5to10)}")
    println("Multiples of 3: ${numbers.filter(isMultipleOf3)}")
    println("Numbers > 7: ${numbers.filter(isGreaterThan7)}")
    println("In range 5-10 AND multiple of 3: ${numbers.filter(inRangeAndMultipleOf3)}")
    println("> 7 OR multiple of 5: ${numbers.filter(greaterThan7OrMultipleOf5)}")
    println("NOT in range 5-10: ${numbers.filter(notInRange5to10)}")
}
```

### **4. Advanced Predicate Patterns**

#### **Predicate Composition**
```kotlin
fun main() {
    val employees = listOf(
        Employee("Alice", "Engineer", 3, 75000),
        Employee("Bob", "Manager", 7, 95000),
        Employee("Charlie", "Developer", 2, 65000),
        Employee("Diana", "Designer", 5, 80000),
        Employee("Eve", "Engineer", 4, 78000),
        Employee("Frank", "Manager", 10, 110000)
    )
    
    // Base predicates
    val isEngineer: (Employee) -> Boolean = { it.position == "Engineer" }
    val isManager: (Employee) -> Boolean = { it.position == "Manager" }
    val hasExperience: (Employee) -> Boolean = { it.yearsExperience >= 5 }
    val isWellPaid: (Employee) -> Boolean = { it.salary > 80000 }
    
    // Composite predicates
    val isSeniorEngineer = and(isEngineer, hasExperience)
    val isExperiencedManager = and(isManager, hasExperience)
    val isHighEarningEmployee = and(hasExperience, isWellPaid)
    val isJuniorOrLowPaid = or(not(hasExperience), not(isWellPaid))
    
    println("Senior Engineers: ${employees.filter(isSeniorEngineer)}")
    println("Experienced Managers: ${employees.filter(isExperiencedManager)}")
    println("High Earning Experienced: ${employees.filter(isHighEarningEmployee)}")
    println("Junior or Low Paid: ${employees.filter(isJuniorOrLowPaid)}")
}

data class Employee(val name: String, val position: String, val yearsExperience: Int, val salary: Int)
```

#### **Predicate with State**
```kotlin
fun main() {
    val transactions = listOf(
        Transaction("T1", 100.0, "credit"),
        Transaction("T2", 50.0, "debit"),
        Transaction("T3", 200.0, "credit"),
        Transaction("T4", 75.0, "debit"),
        Transaction("T5", 150.0, "credit")
    )
    
    // Predicate with running total
    fun createRunningTotalPredicate(threshold: Double): (Transaction) -> Boolean {
        var runningTotal = 0.0
        
        return { transaction ->
            when (transaction.type) {
                "credit" -> runningTotal += transaction.amount
                "debit" -> runningTotal -= transaction.amount
            }
            runningTotal >= threshold
        }
    }
    
    // Predicate: transaction brings running total above threshold
    val bringsTotalAbove200 = createRunningTotalPredicate(200.0)
    
    val significantTransactions = transactions.filter(bringsTotalAbove200)
    println("Transactions that bring total above 200: $significantTransactions")
}

data class Transaction(val id: String, val amount: Double, val type: String)
```

## 🎯 Key Concepts Explained

### **1. Predicate Characteristics**
- **Return Type**: Always returns `Boolean`
- **Single Responsibility**: Should test one specific condition
- **Reusability**: Can be stored in variables and reused
- **Composability**: Can be combined with logical operators

### **2. Predicate Composition Patterns**
```kotlin
// AND composition
val isAdultAndEmployed = and(isAdult, isEmployed)

// OR composition  
val isStudentOrRetired = or(isStudent, isRetired)

// NOT composition
val isNotMinor = not(isMinor)

// Complex composition
val isEligibleForLoan = and(
    isAdult,
    isEmployed,
    or(hasGoodCredit, hasCoSigner),
    not(hasBankruptcy)
)
```

### **3. Performance Considerations**
- **Short-circuit evaluation**: `all` and `none` stop at first false/true
- **Lazy evaluation**: Use `asSequence()` for large collections
- **Predicate reuse**: Store predicates in variables to avoid recreation

## 🧪 Running the Examples

### **Step 1: Open the File**
1. Navigate to `src/45_predicate.kt`
2. Open it in IntelliJ IDEA

### **Step 2: Run the Program**
1. Right-click on the file
2. Select "Run '45_predicateKt'"
3. Observe the output

## 🎮 Hands-On Exercises

### **Exercise 1: Email Validation Predicates**
Create predicates for validating email addresses.

**Solution:**
```kotlin
fun main() {
    val emails = listOf(
        "user@example.com",
        "invalid-email",
        "test@domain",
        "user.name@company.co.uk",
        "@example.com",
        "user@.com"
    )
    
    // Email validation predicates
    val hasAtSymbol: (String) -> Boolean = { it.contains("@") }
    val hasDomain: (String) -> Boolean = { email ->
        val parts = email.split("@")
        parts.size == 2 && parts[1].contains(".")
    }
    val hasValidLength: (String) -> Boolean = { it.length in 5..254 }
    val doesntStartWithAt: (String) -> Boolean = { !it.startsWith("@") }
    val doesntEndWithAt: (String) -> Boolean = { !it.endsWith("@") }
    
    // Composite email validator
    val isValidEmail = and(
        hasAtSymbol,
        hasDomain,
        hasValidLength,
        doesntStartWithAt,
        doesntEndWithAt
    )
    
    emails.forEach { email ->
        val isValid = isValidEmail(email)
        println("$email: ${if (isValid) "✅ Valid" else "❌ Invalid"}")
    }
}
```

### **Exercise 2: Product Filtering System**
Create a product filtering system using predicates.

**Solution:**
```kotlin
fun main() {
    val products = listOf(
        Product("Laptop", 999.99, "Electronics", 4.5),
        Product("Mouse", 29.99, "Electronics", 4.2),
        Product("Book", 19.99, "Books", 4.8),
        Product("Chair", 199.99, "Furniture", 4.0),
        Product("Pen", 2.99, "Office", 3.5),
        Product("Tablet", 499.99, "Electronics", 4.6)
    )
    
    // Product predicates
    val inCategory = { category: String -> { product: Product -> product.category == category } }
    val inPriceRange = { min: Double, max: Double -> 
        { product: Product -> product.price in min..max } 
    }
    val hasRating = { minRating: Double -> { product: Product -> product.rating >= minRating } }
    val isExpensive = { product: Product -> product.price > 100.0 }
    val isAffordable = { product: Product -> product.price < 50.0 }
    
    // Filter combinations
    val electronicsUnder500 = and(inCategory("Electronics"), inPriceRange(0.0, 500.0))
    val highRatedExpensive = and(hasRating(4.5), isExpensive)
    val affordableOrHighRated = or(isAffordable, hasRating(4.5))
    
    println("Electronics under $500: ${products.filter(electronicsUnder500)}")
    println("High-rated expensive items: ${products.filter(highRatedExpensive)}")
    println("Affordable or high-rated: ${products.filter(affordableOrHighRated)}")
}

data class Product(val name: String, val price: Double, val category: String, val rating: Double)
```

### **Exercise 3: Student Grade Analysis**
Create predicates for analyzing student grades and performance.

**Solution:**
```kotlin
fun main() {
    val students = listOf(
        Student("Alice", listOf(85, 92, 78, 95, 88)),
        Student("Bob", listOf(72, 68, 75, 80, 85)),
        Student("Charlie", listOf(95, 98, 92, 89, 96)),
        Student("Diana", listOf(78, 82, 75, 79, 81)),
        Student("Eve", listOf(88, 85, 90, 87, 89))
    )
    
    // Grade analysis predicates
    val hasHighAverage = { threshold: Double -> 
        { student: Student -> student.grades.average() >= threshold } 
    }
    val hasConsistentGrades = { maxVariation: Double ->
        { student: Student ->
            val grades = student.grades
            grades.maxOrNull()!! - grades.minOrNull()!! <= maxVariation
        }
    }
    val hasImprovingTrend = { student: Student ->
        val grades = student.grades
        grades.zipWithNext().all { (current, next) -> next >= current }
    }
    val hasNoFailures = { threshold: Int -> 
        { student: Student -> student.grades.all { it >= threshold } } 
    }
    
    // Analysis combinations
    val highAchievers = hasHighAverage(90.0)
    val consistentStudents = hasConsistentGrades(10.0)
    val improvingStudents = hasImprovingTrend
    val passingStudents = hasNoFailures(60)
    
    println("High achievers (90+ avg): ${students.filter(highAchievers)}")
    println("Consistent students (≤10 variation): ${students.filter(consistentStudents)}")
    println("Improving students: ${students.filter(improvingStudents)}")
    println("Passing students (60+ all): ${students.filter(passingStudents)}")
}

data class Student(val name: String, val grades: List<Int>)
```

### **Exercise 4: Predicate Builder DSL**
Create a domain-specific language for building complex predicates.

**Solution:**
```kotlin
class PredicateBuilder<T> {
    private var predicate: (T) -> Boolean = { true }
    
    fun and(p: (T) -> Boolean): PredicateBuilder<T> {
        val current = predicate
        predicate = { item -> current(item) && p(item) }
        return this
    }
    
    fun or(p: (T) -> Boolean): PredicateBuilder<T> {
        val current = predicate
        predicate = { item -> current(item) || p(item) }
        return this
    }
    
    fun not(p: (T) -> Boolean): PredicateBuilder<T> {
        val current = predicate
        predicate = { item -> current(item) && !p(item) }
        return this
    }
    
    fun build(): (T) -> Boolean = predicate
}

fun <T> predicate(init: PredicateBuilder<T>.() -> Unit): (T) -> Boolean {
    return PredicateBuilder<T>().apply(init).build()
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15)
    
    // Using the predicate builder DSL
    val complexPredicate = predicate<Int> {
        and { it > 5 }
        and { it % 2 == 0 }
        or { it % 3 == 0 }
        not { it == 10 }
    }
    
    val result = numbers.filter(complexPredicate)
    println("Numbers matching complex predicate: $result")
    
    // Another example
    val rangePredicate = predicate<Int> {
        and { it in 1..20 }
        and { it % 2 == 0 }
        or { it % 7 == 0 }
    }
    
    val rangeResult = numbers.filter(rangePredicate)
    println("Numbers in range with conditions: $rangeResult")
}
```

## 🚨 Common Mistakes to Avoid

1. **Complex predicates**: Keep predicates simple and focused ✅
2. **Ignoring performance**: Use sequences for large collections ✅
3. **Forgetting composition**: Leverage predicate composition patterns ✅
4. **Hardcoding values**: Use predicate factories for flexibility ✅

## 🎯 What's Next?

Now that you understand predicates, continue with:

1. **Scope Functions** → [Advanced Scope Functions](03-let-also-run.md)
2. **Collections** → [Collections Overview](../collections/README.md)
3. **Coroutines** → [Coroutines Introduction](../coroutines/01-introduction.md)
4. **Advanced OOP** → [Enums and Sealed Classes](../oop/07-enums-sealed-classes.md)

## 📚 Additional Resources

- [Official Kotlin Collections Documentation](https://kotlinlang.org/docs/collections-overview.html)
- [Collection Operations](https://kotlinlang.org/docs/collection-operations.html)
- [Lambda Functions](https://kotlinlang.org/docs/lambdas.html)

## 🏆 Summary

- ✅ You understand what predicates are and how they work
- ✅ You can use predicates with collection functions like filter, any, all, none
- ✅ You can create custom predicates for complex conditions
- ✅ You know how to chain predicates for sophisticated filtering
- ✅ You're ready to apply predicates in real-world scenarios!

**Predicates are powerful tools for data filtering and validation. Master them for clean and expressive collection operations! 🎉**
