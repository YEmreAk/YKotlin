# 🌄 Scope \| Coroutine

## 🔮 Neden Kullanılmalıdır

* 💫 Yaşam döngüsü olan sınıflarda tercih edilir
* ☠ Activity öldüğünde coroutine işlemleri devam eder
* 🎳 Devam eden işlemler gereksiz bellek kullanırlar \(memory leak\)

## 🛑 Manuel Durdurma

```kotlin
class Activity {
    private val mainScope = MainScope()
    
    fun destroy() {
        mainScope.cancel()
    }
// to be continued ...
}
```

## 🏗️ Scope Tanımlama

* ✋ Activity sonlandığında coroutine işlemleri de sonlanır
* 💁‍♂️ Gereksiz işlemler otomatik önlenir
* ✨ `CoroutineScope by CoroutineScope(<dispathcer>)` miras alınır

```kotlin
class Activity : CoroutineScope by CoroutineScope(Dispatchers.Default) {
    fun doSomething() {
        // launch ten coroutines for a demo, each working for a different time
        repeat(10) { i ->
            launch {
                delay((i + 1) * 200L) // variable delay 200ms, 400ms, ... etc
                println("Coroutine $i is done")
            }
        }
    }
} // class Activity ends

val activity = Activity()
activity.doSomething() // run test function
println("Launched coroutines")
delay(500L) // delay for half a second
println("Destroying activity!")
activity.destroy() // cancels all coroutines
delay(1000) // visually confirm that they don't work

/*
Launched coroutines
Coroutine 0 is done
Coroutine 1 is done
Destroying activity!
*/
```

## 🧐 Kaynaklar

{% embed url="https://kotlinlang.org/docs/reference/coroutines/coroutine-context-and-dispatchers.html\#coroutine-scope" %}

