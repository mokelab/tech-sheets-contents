Title: Jetpack Composeで高さを指定する

Composableの高さを指定したサイズにするには、 `modifier` パラメータに `Modifier.height()` を渡します。単位はdp単位です。

```kotlin
@Composable
fun Greeting2(name: String) {
    Column {
        Text(text = "こんにちは", 
            modifier = Modifier.height(40.dp))
        Text(text = "$name!")
    }
}
```

プレビューは次のようになります。「こんにちは」の部分の高さが40dpとなり、余白が生じているのが確認できます。

![プレビュー](./height1.png)
