---
description: >-
  Coroutine yapısı, ne işe yarar, nedir, neden kullanılır ve temel kullanım
  örnekleri nelerdir
---

# 🚴‍♂️ Giriş \| Coroutine

## 🔮 Ne İşe Yarar

* 🕊️ Thread işlemlerini kolaylaştıran bir hafif yapıdır
* 👷‍♂️ `Coroutine` ile inline thread kullanabilirsin
* ✨ Otomatik olarak optimize edilirler

{% hint style="warning" %}
📢 Kullanabilmek için Kotlin Coroutine desteğini [buradan](https://github.com/kotlin/kotlinx.coroutines/blob/master/README.md#using-in-your-projects) projene eklemen lazım 
{% endhint %}

## 🧱 Temel Kullanım

* 🧐 `GlobalScope` bağımsız olarak çalışır
* 🙄 İçinde bulunduğu thread bitse bile devam eder
* 🌇 `GlobalScope.launch {}` coroutine'i işi bitince sonlanır \(daemon\)
* 👪 `repeat` ile birden fazla tekrarlanabilir

```kotlin
import kotlinx.coroutines.*

fun main() { 
    GlobalScope.launch { // Arka planda yeni bir işlem (coroutine) başlatır
        delay(1000L)
        println("World!")
    }
    println("Hello,") // Ana thread üzerinde çalışır
    runBlocking {     // Bu alandaki işlemler de ana thread'i engeller
        delay(2000L)  // ... 2s gecikmeden sonra JVM çalışmaya devam eder
    } 
}

// Unit döndüren bir coroutine tanımlama (yukarıdaki ile aynıdır)
fun main() = runBlocking<Unit> { 
    GlobalScope.launch { 
        delay(1000L)
        println("World!")
    }
    println("Hello,")
    delay(2000L)
}

// Tekrarlı kullanım ypaısı
fun main() = runBlocking<Unit> { 
    GlobalScope.launch { 
        delay(1000L)
        println("World!")
    }
    repead(3) {
        println("Hello,")
        delay(2000L)
    }
}
```

## 🏗️ İş Oluşturma

```kotlin
val job = GlobalScope.launch { // Coroutine oluşturma (thread oluşturma gibi)
    delay(1000L)
    println("World!")
}
println("Hello,")
job.join() // Coroutine bitene kadar bekleme (thread.join() gibi)
```

## 💠 Suspend Metotlar

* 🚫 Coroutine içeren metotlar `suspent` anahtarı ile belirtilir
* 💫 `async` içerisinde kullanılarak asenkron çalışabilirler
* 🛑 `await` metodu ile çalışmasını tamamlaması beklenebilir
* 🙄 `GlobalScope.async {}` yapısı ile diğer diller gibi çalışabilir ama tavsiye edilmez

```kotlin
fun main() = runBlocking<Unit> {
    val time1 = measureTimeMillis { // 2017ms
        val one1 = doSomethingUsefulOne()
        val two1 = doSomethingUsefulTwo()
        println("The answer is ${one + two}")
    }
    println("Completed in $time ms")

    val time2 = measureTimeMillis { // 1017ms <- Async çalıştığı için daha hızlı
        val one2 = async { doSomethingUsefulOne() }
        val two2 = async { doSomethingUsefulTwo() }
        println("The answer is ${one.await() + two.await()}")
    }
    println("Completed in $time ms")
    
    val time3 = measureTimeMillis{ // 1017ms <- Async çalışır
        one2.await() + two2.await() 
    }
}

suspend fun concurrentSum(): Int = coroutineScope {
    val one = async { doSomethingUsefulOne() }
    val two = async { doSomethingUsefulTwo() }
    one.await() + two.await()
}

suspend fun doSomethingUsefulOne(): Int {
    delay(1000L) // pretend we are doing something useful here
    return 13
}

suspend fun doSomethingUsefulTwo(): Int {
    delay(1000L) // pretend we are doing something useful here, too
    return 29
}
```

{% hint style="info" %}
‍🧙‍♂ Detaylı bilgi için[ Composing Suspending Functions](https://kotlinlang.org/docs/reference/coroutines/composing-suspending-functions.html#composing-suspending-functions) alanına bakabilirsin.
{% endhint %}

