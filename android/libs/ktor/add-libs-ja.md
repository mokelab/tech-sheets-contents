Title: AndroidアプリにKtorを追加する

Priority: 10

AndroidアプリにKtorを追加するには、app/build.gradle.ktsのdependenciesに次の2つを追加します。

```
dependencies {
  implementation("io.ktor:ktor-client-core:3.0.2")
  implementation("io.ktor:ktor-client-cio:3.0.0")
}
```

- ktor-client-core はKtorクライアントの基盤となるモジュールです。
- ktor-client-cio は、実際のHTTPリクエストの実行に利用するエンジンです。

また、AndroidManifest.xmlにINTERNETパーミッションも追加します。

```
<manifest>
    <uses-permission android:name="android.permission.INTERNET" />
    <application>
        ...
    </application>
</manifest>
```
