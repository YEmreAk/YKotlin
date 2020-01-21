# 🚴‍♂️ Giriş \| Değişkenler

## 🏗️ Değişken Tanımlama

* 👨‍💻 `var` ile tanımlanırlar
* 💁‍♂️ Değişken tipinin belirtilmesine gerek yoktur
* 🤓 Yine de belirmek istersen `: String` eki ile belirtilir

```kotlin
var metin = "yemreak" // String metin = "yemreak"
var metin: String = "yemreak" // String metin = "yemraek"
```

## 🧱 Sabit Değerler

* 👮‍♂️ Sonradan değiştirilemezler
* 👨‍💻 `val` ile tanımlanırlar
* 💁‍♂️ Java için `final` deyimine denktir

```kotlin
val metin = "değişmem" // final String metin = "değişmem"

/*
Foo
bar
*/
val uzunMetin = """
                Foo
                Bar
                """.trimIndent()

/*
if(a > 1) {
    return a
}
*/               
val uzunGirintiliMetin = """if(a > 1) {
                         |    return a
                         |}""".trimMargin()
                         
// 0 sa true değilse false
val isEmpty: Boolean get() = size == 0
```

## 💠 Fonksiyonel

* 😱 Fonksiyon değişkenleri tanımlanabilir
* 💁‍♂️ Kotlin de her şeyin değişkeni tanımlanabilir \(neredeyse\)

```kotlin
var func: () -> Unit = {
    // Kardeş ben fonksiyonum
}

var func2: (Boolean) -> Unit = { bool ->
    // Kardeş ben parametreli fonksiyonum
}

val func2: (Boolean) -> Int = { bool ->
    // Kardeş ben bir integer döndürüyorum
    return 1
}
```

## 🏗️ Obje

```kotlin
object : Obje
object : CountDownTimer(1, 1){...}
object : Intent(...)
```

