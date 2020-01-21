# 🏃‍♂️ Hızlı Notlar

## 🕐 Zaman Hesaplama

```kotlin
val time = measureTimeMillis {
    val one = doSomethingUsefulOne()
    val two = doSomethingUsefulTwo()
    println("The answer is ${one + two}")
}
println("Completed in $time ms")
```

## 📋 Hepsi

```kotlin
// TODO
fun calcTaxes(): BigDecimal = TODO("Waiting for feedback from accounting")

// Koşullu kullanım (Conditional expressions)
if (a > b) a else b

// Instance check
when (x) {
    is Foo -> // ...
    is Bar -> // ...
    else   -> // ...
}
(obj !is String)

// Range
for (x in 1..10 step 2) {}

// Collections
val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
  .filter { it.startsWith("a") }
  .sortedBy { it }
  .map { it.toUpperCase() }
  .forEach { println(it) }

("jane@example.com" !in emailsList)
  
// Filtreleme
list.filter { x -> x > 0 }

// Lazy
val p: String by lazy {
    // compute the string
}

// Extension functions
fun String.spaceToCamelCase() { /* ... */ }

// Null 
println(files?.size ?: "empty")
val mapped = value?.let { transformValue(it) } ?: defaultValue
val email = values["email"] ?: throw IllegalStateException("Email is missing!")

// Try-Catch
val email = values["email"] ?: throw IllegalStateException("Email is missing!")

fun transform(color: String): Int {
    return when (color) {
        "Red" -> 0
        "Green" -> 1
        "Blue" -> 2
        else -> throw IllegalArgumentException("Invalid color param value")
    }
}

fun test() {
    val result = try {
        count()
    } catch (e: ArithmeticException) {
        throw IllegalStateException(e)
    }

    // Working with result
}

fun transform(color: String): Int = when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentException("Invalid color param value")
}

// Java 7's try with resources
val stream = Files.newInputStream(Paths.get("/some/file.txt"))
stream.buffered().reader().use { reader ->
    println(reader.readText())
}

// Convenient form for a generic function that requires the generic type information

//  public final class Gson {
//     ...
//     public <T> T fromJson(JsonElement json, Class<T> classOfT) throws JsonSyntaxException {
//     ...


inline fun <reified T: Any> Gson.fromJson(json: JsonElement): T = this.fromJson(json, T::class.java)

// Swap var
var a = 1
var b = 2
a = b.also { b = a }


```

## Functions vs Properties

In some cases functions with no arguments might be interchangeable with read-only properties. Although the semantics are similar, there are some stylistic conventions on when to prefer one to another.

Prefer a property over a function when the underlying algorithm:

* does not throw
* is cheap to calculate \(or caсhed on the first run\)
* returns the same result over invocations if the object state hasn't changed

## Platform types

A public function/method returning an expression of a platform type must declare its Kotlin type explicitly:

```kotlin
fun apiCall(): String = MyJavaApi.getProperty("name")
```

Any property \(package-level or class-level\) initialised with an expression of a platform type must declare its Kotlin type explicitly:

```kotlin
class Person {
    val name: String = MyJavaApi.getProperty("name")
}
```

A local value initialized with an expression of a platform type may or may not have a type declaration:

```kotlin
fun main() {
    val name = MyJavaApi.getProperty("name")
    println(name)
}
```

