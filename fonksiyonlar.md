# 💠 Fonksiyonlar

## 🔌 Fonksiyon Genişletmeleri

* ➕ Olmayan metotları sınıflara sonradan dahil edebilirsiniz
* 🐥 Metot yerine `get() =` yapısı ile property \(özellik\) de eklenebilir

```kotlin
// Metot genişletmeleri
fun Uri.inputStream(activity: Activity): InputStream {
    return activity.contentResolver.openInputStream(this)!!
}

val activity = Activity()
val mUri: Uri = new Uri()

// Kullanım
val inputStream = uri.inputStream(activity)
```

```kotlin
// Özellik genişletmeleri
val WifiP2pInfo.isConnected: Boolean
    get() = groupFormed

val WifiP2pInfo.isClient: Boolean
    get() = isConnected && !isGroupOwner

val WifiP2pInfo.isServer: Boolean
    get() = isConnected && isGroupOwner
    
val info: WifiP2pInfo = WifiP2pInfo()

// Kullanımlar
info.isConnected
info.isClient
info.isServer
```



