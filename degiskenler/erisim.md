# 🐣 Erişim \| Değişkenler

## 🐣 Get Set Kavramları

* 🌌 Get set olmadan direkt olarak kullanabilirsiniz
* ‍🧙‍♂ Kotlin, onu sizin için halletmekte
* ⭐ Değişkenlere özel get set metotları tanımlanabilir

```kotlin
val arrayAdapter = ArrayAdapter<String>(
    wifiDirectActivity,
    R.layout.activity_wifi_direct,
    deviceNameList
)
wifiDirectActivity.lvPeer.adapter = arrayAdapter


// 0 sa true değilse false
val isEmpty: Boolean get() = size == 0
```

