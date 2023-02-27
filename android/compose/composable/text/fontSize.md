Title: Text Composeで文字サイズを変更する

Text Composableで文字の表示サイズを変更するには、 `fontSize` パラメータをsp単位で指定します。

```kotlin
@Composable
fun Greeting(name: String) {
    Row {
        Text(text = "ねぇ")
        Text(text = "$name!", fontSize = 25.sp)
    }
}
```

プレビューは次のようになります。

![プレビュー](./fontSize1.png)

## .spとは？

`25.sp` は普通のプログラミングだとあまり見かけない表現です。中身を見てみましょう。

```kotlin
val Int.sp: TextUnit get() = pack(UNIT_TYPE_SP, this.toFloat())
```

Int型の拡張プロパティとして定義されています。 `pack()` の中身はJetpack Composeライブラリで定義されたLong値への変換なので中身を追わないようにします。。

