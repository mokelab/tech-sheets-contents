Title: Jetpack Composeでコンポーザブルをタップ可能にする

Priority: 80

View Systemでは `setOnClickListener()` を使うとViewをタップ時になにか処理をさせることができました。

Jetpack Composeで任意のコンポーザブルをタップ可能にするには、 `modifier` パラメータで `clickable` を使います。

例として画像をタップ可能にしてみます。

```
Image(
  painter = painterResource(R.drawable.moke),
  contentDescription = "Moke",
  modifier = Modifier.clickable {
    // タップ時の処理
    println("Clicked!")
  }
)
```
