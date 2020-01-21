# ⭐ Özellikler \| Değişkenler

## ⚡ Statik

* 🦄 Sadece 1 kez tanımlanırlar
* 🌇 `companion object` içerisindeki tüm tanımlamalar `static` olarak ele alınır
* 🐣 Diğer sınıflardan `<class>.<static>` şeklinde erişilebilir

```kotlin
class Main {
    val metin0 = "hello"
    companion object {
        var metin1 = "yemreak" // static String metin = "yemreak"
        var metin2: String = "yemreak" // static String metin = "yemraek"
        val metin3 = "değişmem" // static final String metin = "değişmem"
    }
}

class New {
    var metin0 = Main.metin0 // Çalışmaz, metin0 static değil
    Main.metin2 = "Heey" // Metin 2 objesinin değeri değişir
    Main.metin3 = "Olmaz" // Val olduğu için değer atanmaz
} 
```

## 🕐 Tanımlanmamış

* 🙄 Henüz değeri atanmamış değerlerdir
* 🐞 Değerleri atanmadan kullanılırlarsa hata fırlatır

```kotlin
lateinit var sonrakiMetin

// ... 
var a = sonrakiMetin // Tanımlanmadan kullanıldı HATA!
sonrakiMetin = "yok"
var b = sonrakiMetin // Çalışır
```

## 🦥 Lazy \(Tembel\)

* 😴 Tüm değişkenler tanımlandıktan sonra tanımlanırlar

## 🐥 Nullable

* ✨ Kotlin üzerinde tüm değişkenler **null olmayacak** şekilde tanımlanır
* 🌌 Null olabilecek değerler `?` ile tanımlanır
* 👨‍💼 `!!` deyimi ile "Null olmadığından eminim" komutu verilir
* 👮‍♂️ `?.` deyimi ile "Null değilse çalıştır" komutu verilir
* 🧐 `?:` deyimi ile "Varsa ilki yoksa ikinci" komutu verilir

> ✨ Java'daki `NullPointerException` hatalarına odaklı bir çalışmadır

```kotlin
// ' ? ' değişkenin değerinin null da olabiliceğini ifade etmekte.
var sayi? = null

// '!!' değişkenin kesinlikle değerinin olacağını ifade etmekte.
var kesin!!             

// b null değilse b'nin uzunluğunu ata aksi halde -1 ata (Elvis Operator)
val a = b?.lenght ?: -1 

var metin1: String? = null
metin?. // Varsa kullan
metin!! // Olduğundan kesinlikle eminim

var func: (() -> Unit)? = null
func?.invoke() // Null değilse çalıştır

// Dsoya varsa sayısı yoksa boş yaz
println(files?.size ?: "empty")

// Hata fırlatmalı atamalar
val email = values["email"] ?: throw IllegalStateException("Email is missing!")
```

{% hint style="info" %}
📢 Sonradan tanımlanacak değişkenler için `?` değil `lateinit` kullanın
{% endhint %}

