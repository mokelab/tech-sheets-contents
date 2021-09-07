Title: 文字列を表示する

Jetpack Composeで文字列を表示するには、 `Text` composable関数を使います。引数には表示したい文字列を指定します。

プロジェクトを作るとデフォルトで文字列を表示する関数が作られるので、特に説明は不要かと思います。

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello $name!")
}
```

## 文字列リソースを表示する

多言語対応のため、画面に表示する文字列は文字列リソースから取得するのが望ましいです。

Jetpack Composeでは `stringResource()` を使います。引数には `getString()` と同様に文字列リソースのIDを指定します。

```kotlin
@Composable
fun AppName() {
    Text(text = stringResource(id = R.string.app_name))
}
```

文字列リソースに `%1$s` のようなプレースホルダがある場合、これも `getString()` のときと同様に `stringResource()` に引数として渡すことで値をセットすることができます。

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = stringResource(id = R.string.hello, name))
}
```
