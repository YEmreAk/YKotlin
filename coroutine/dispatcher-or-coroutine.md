---
description: Coroutine yönlendiricileri ile optimize işlemler yapma
---

# 🏹 Dispatcher \| Coroutine

## 🔮 Neden Kullanılır

* ✨ Optimize edilmiş thread yapısıdır
* 👮‍♂️ Main \(UI\), IO, Default thread yapıları ile arka plan işlemlerini yönetirsiniz
* 🦄 `newSingleThreadContext` ile tek örneği olan coroutine yapısı oluşturulur

## ⭐ Dispatcher Sınıfları

| 🧱 Main | 🔣 IO | 🎳 Default | 🌌 Unconfined |
| :--- | :--- | :--- | :--- |
| UI Thread işlemleri | Disk ve network işlemleri | CPU gerektiren işlemler | Main thread işlemleri |
| Fonksiyon çağırma | Database | Liste sıralama | Tanımlanmamıştır |
| View işlemleri | Dosya okuma & yazma | JSON parsing |  |
| LiveData işlemleri | Ağ işlemleri | DiffUtils |  |

## 👨‍💻 Kullanım Örneği

```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking<Unit> {
    launch { // context of the parent, main runBlocking coroutine
        println("main runBlocking      :\
         I'm working in thread ${Thread.currentThread().name}")
    }
    launch(Dispatchers.Unconfined) { // not confined -- will work with main thread
        println("Unconfined            :\
         I'm working in thread ${Thread.currentThread().name}")
    }
    launch(Dispatchers.Default) { // will get dispatched to DefaultDispatcher 
        println("Default               :\
         I'm working in thread ${Thread.currentThread().name}")
    }
    launch(newSingleThreadContext("MyOwnThread")) { // will get its own new thread
        println("newSingleThreadContext:\
         I'm working in thread ${Thread.currentThread().name}")
    }    
}

/*
Sırası değişken olabilir (?)
Unconfined            : I'm working in thread main
Default               : I'm working in thread DefaultDispatcher-worker-1
newSingleThreadContext: I'm working in thread MyOwnThread
main runBlocking      : I'm working in thread main (Her zaman en son çalışır)
*/
```

{% hint style="info" %}
‍🧙‍♂ Detaylı bilgi için:

* [👨‍💻 Dispatchers](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-dispatchers/)
* [📖 Dispatchers and thread](https://kotlinlang.org/docs/reference/coroutines/coroutine-context-and-dispatchers.html#dispatchers-and-threads)
* [📖 Improve app performance with Kotlin coroutines ~ Android](https://developer.android.com/kotlin/coroutines) 
* [📃 Coroutines on Android \(part I\): Getting the background](https://medium.com/androiddevelopers/coroutines-on-android-part-i-getting-the-background-3e0e54d20bb)

alanlarına bakabilirsin.
{% endhint %}

## 🚚 Thread Arasında Dolanma

* 🆔 `Context` değerleri ile thread değiştirilebilir
* 🚫 `runBlocking` context alarak çalışabilmekte

```kotlin
import kotlinx.coroutines.*

fun log(msg: String) = println("[${Thread.currentThread().name}] $msg")

fun main() {
    newSingleThreadContext("Ctx1").use { ctx1 ->
        newSingleThreadContext("Ctx2").use { ctx2 ->
            runBlocking(ctx1) {
                log("Started in ctx1")
                withContext(ctx2) {
                    log("Working in ctx2")
                }
                log("Back to ctx1")
            }
        }
    }    
}

/*
[Ctx1 @coroutine#1] Started in ctx1
[Ctx2 @coroutine#1] Working in ctx2
[Ctx1 @coroutine#1] Back to ctx1
*/
```

## 👨‍👨‍👦‍👦 İç İçe Coroutine

* **👨‍👦** İç coroutine işlemleri bitmeden ana coroutine tamamlanmaz
* 🧐 `GlobalScope` bağımsız olarak çalışır
* 🙄 İçinde bulunduğu thread bitse bile devam eder
* 🌇 `GlobalScope.launch {}` coroutine'i işi bitince sonlanır \(daemon\)

```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking<Unit> {
    // launch a coroutine to process some kind of incoming request
    val request = launch {
        // GlobalScope üzerinde coroutine tanımlama
        GlobalScope.launch {
            println("job1: I run in GlobalScope and execute independently!")
            delay(1000)
            println("job1: I am not affected by cancellation of the request")
        }
        // Run blocking context'ini miras alan coroutine tanımlama
        launch {
            delay(100)
            println("job2: I am a child of the request coroutine")
            delay(1000)
            println("job2: I will not execute this line if my parent request is cancelled")
        }
    }
    delay(500)
    request.cancel() // Coroutine objesini durdurma
    delay(1000) // delay a second to see what happens
    println("main: Who has survived request cancellation?")
}

/*
job1: I run in GlobalScope and execute independently!
job2: I am a child of the request coroutine
job1: I am not affected by cancellation of the request
main: Who has survived request cancellation?
*/
```

## ➕ Context ile Birleştirme

```kotlin
launch(Dispatchers.Default + CoroutineName("test")) {
    println("I'm working in thread ${Thread.currentThread().name}")
}
```

## 👷‍♂️ Coroutine

```kotlin
val inputStream: InputStream = InputStream()

fun usage() {
    GlobalScope.launch {
        readBuffered(inputStream)
    }
}

suspend fun readBuffered() -> Unit)
    = withContext(Dispatchers.IO) {
        while (inputStream.read(buffer) != -1) {
            // ...
        }
}
```

