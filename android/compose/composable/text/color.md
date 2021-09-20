Title: Text Composableで文字列の色を変更する

Text Composableで文字列の色を変更するには、 `color` パラメータに `Color` オブジェクトを渡します。 `androidx.compose.ui.graphics` パッケージにある `Color` なので注意しましょう。

```kotlin
@Composable
fun Greeting(name: String) {
    Row {
        Text(text = "こんばんは!")
        Text(text = "$name!",
            color = Color(0xFF00FF00))
    }
}
```

プレビューは次のようになります。

![プレビュー](./color1.png)

## リソースの値を使う

リソースで定義している色を指定したい場合は、 `colorResource()` を使います。

```kotlin
@Composable
fun Greeting(name: String) {
    Row {
        Text(text = "こんばんは!")
        Text(text = "$name!",
            color = colorResource(id = android.R.color.holo_green_dark))
    }
}
```
