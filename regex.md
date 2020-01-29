---
description: Kotlin ile regular expression (regex) kullanımı
---

# 💎 RegEx

## 🧱 Temel Kullanım

* 👨‍🔬 Regex test işlemleri için [Regex101](https://regex101.com/) sitesini kullanabilirsiniz
* 💠 Tüm regex metotlarına [`Regex`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/index.html) ile erişebilirsiniz
* ⚙️ Kotlin Regex ayarlarına [`RegexOption`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex-option/index.html) ile erişebilirsiniz

## ⭐ Basit Kullanım

```kotlin
// . ile tüm karakterler alınır
"""<pre>.*</pre>""".toRegex(RegexOption.DOT_MATCHES_ALL)
regex.find(response)?.value?.let { // İlk bulunanı döndürür
    // Bulunan metin `it`
}
```

## 🍱 Gruplama

```kotlin
val text = "Hello Alice. Hello Bob. Hello Eve."
val regex = Regex("Hello (.*?)[.]")
val matches = regex.findAll(text)
val names = matches.map { it.groupValues[1] }.joinToString()
println(names) // Alice, Bob, Eve
```

## 🔗 Faydalı Bağlantılar

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/index.html" %}

