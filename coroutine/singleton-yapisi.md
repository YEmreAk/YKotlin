# 🦄 Singleton Yapısı

## 👨‍💻 Sınıf Kodu

```kotlin
open class SingletonHolder<T, A>(creator: (A) -> T) {
    private var creator: ((A) -> T)? = creator
    @Volatile private var instance: T? = null

    fun getInstance(arg: A): T {
        val i = instance
        if (i != null) {
            return i
        }

        return synchronized(this) {
            val i2 = instance
            if (i2 != null) {
                i2
            } else {
                val created = creator!!(arg)
                instance = created
                creator = null
                created
            }
        }
    }
}
```

## 🔗 Faydalı Bağlantılar

{% embed url="https://stackoverflow.com/questions/45912619/using-room-as-singleton-in-kotlin" %}



