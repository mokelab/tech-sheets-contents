Title: Hiltを使ってViewModelに依存性を注入(DI)する

Priority: 10

本記事はJetpack Composeを使うアプリにおいて、Hiltを使ってViiewModelに依存性を注入(DI)する方法を解説します。
Viewシステム(レイアウトXML/フラグメント)の場合は使用するライブラリ等が一部異なるので注意してください。

公式ドキュメントは[こちら](https://developer.android.com/jetpack/compose/libraries?hl=ja#hilt)です。本記事執筆時はやや記事が足りないので本記事を活用してください。

## ライブラリを追加する

まず、プロジェクトのルートにある `build.gradle` でライブラリを追加します。

```gradle
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    ...
    dependencies {
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
        classpath 'com.google.dagger:hilt-android-gradle-plugin:2.36' // これを追加
    }
}
```

次に、 `app/build.gradle` にもライブラリを追加します。プラグインも追加します（kotlin-kaptはおそらくKSPに置き換えられるので、置き換え後に本記事を見た方は @mokelabまでお知らせください)。

```gradle
plugins {
    ...
    // この２つを追加
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}

dependencies {
    ...
    implementation "com.google.dagger:hilt-android:2.36"
    kapt "com.google.dagger:hilt-android-compiler:2.36"
    // Jetpack Compose用のライブラリ
    implementation 'androidx.hilt:hilt-navigation-compose:1.0.0-alpha03'
}
```

## アプリケーションクラスを作る

Hiltを使うには `@HiltAndroidApp` のついたアプリケーションクラスを作る必要があります。

```kotlin
@HiltAndroidApp
class ComposeApplication: Application()
```

AndroidManifest.xmlにも登録します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <application
        ...
        android:name=".ComposeApplication">
        <activity>
        ... 
        </activity>
    </application>
</manifest>
```






