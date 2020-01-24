# 📂 Dosya İşlemleri

## 👨‍💻 Kişisel Kodlarım

```kotlin
/**
 * Verilen [fileUri] değerine sahip olan dosya için [InputStream] döndürür
 */
@Throws(FileNotFoundException::class)
fun getInputStream(activity: Activity, fileUri: Uri): InputStream {
    return activity.contentResolver.openInputStream(fileUri)!!
}

/**
 * Verilen [fileUri] değerine sahip olan dosya için [BufferedInputStream] döndürür
 */
@Throws(FileNotFoundException::class)
fun getBufferedInputStream(activity: Activity, fileUri: Uri): BufferedInputStream {
    return getInputStream(activity, fileUri).buffered(DEFAULT_BUFFER_SIZE)
}

/**
 * Verilen [fileUri] değerine sahip olan dosya için [OutputStream] döndürür
 */
@Throws(FileNotFoundException::class)
fun getOutputStream(activity: Activity, fileUri: Uri): OutputStream {
    return activity.contentResolver.openOutputStream(fileUri)!!
}

/**
 * Verilen [fileUri] değerine sahip olan dosya için [BufferedOutputStream] döndürür
 */
@Throws(FileNotFoundException::class)
fun getBufferedOutputStream(activity: Activity, fileUri: Uri): BufferedOutputStream {
    return getOutputStream(activity, fileUri).buffered(DEFAULT_BUFFER_SIZE)
}

/**
 * Verilen [fileUri] değerine sahip olan dosyayı [BUFFER] objesini kullanarak parça parça okur.
 * Her okuma işleminde [onBuffered] metodunu okunan [BUFFER] ile çağırır
 */
@Throws(FileNotFoundException::class)
fun readBuffered(
    activity: Activity,
    fileUri: Uri,
    onBuffered: (ByteArray) -> Unit
) {
    return readBuffered(getBufferedInputStream(activity, fileUri), onBuffered)
}

/**
 * Verilen [inputStream] objesini [BUFFER] objesi ile parça parça okuma. Her okuma işleminde
 * [onBuffered] metodunu okunan [BUFFER] ile çağırır
 */
fun readBuffered(
    inputStream: InputStream,
    onBuffered: (ByteArray) -> Unit
) {
    return readBuffered(inputStream.buffered(), onBuffered)
}


/**
 * Verilen [bufferedInputStream] objesini [BUFFER] objesi ile parça parça okuma. Her okuma işleminde
 * [onBuffered] metodunu okunan [BUFFER] ile çağırır
 */
fun readBuffered(
    bufferedInputStream: BufferedInputStream,
    onBuffered: (ByteArray) -> Unit
) {
    while (bufferedInputStream.read(BUFFER) != -1) {
        onBuffered(BUFFER)
    }
}
```

## 🔗 Faydalı Kaynaklar

* [💕 Kotlin IO](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/java.io.-input-stream/index.html)
* [👀 Reading File into ByteArray](https://stackoverflow.com/a/55416646/9770490)

