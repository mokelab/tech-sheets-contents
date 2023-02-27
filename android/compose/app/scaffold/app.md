Title: アプリでScaffold Composableを使ってみる

[Googleのサンプル](https://github.com/android/compose-samples/blob/main/JetNews/app/src/main/java/com/example/jetnews/ui/JetnewsApp.kt)を参考に、
アプリで `Scaffold` を使ってみます。

## MyAppを作る

アプリ全体の設定を担当する `MyApp` Composableを作ります。

```kotlin
@Composable
fun MyApp() {
    ComposeAppTheme {
        Scaffold {
            MainScreen()
        }
    }
}
```

この中で `Scaffold` を呼びます。コンテンツ部分にはメイン画面を表す `MainScreen` を表示することにします。

## MyAppを使う

`MyApp` はアクティビティの `setContent` で使います。

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApp()
        }
    }
}
```


