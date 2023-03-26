Title: Jetpack Composeでタップ可能なアイコンを表示する

Priority: 10

Jetpack Composeでタップ可能なアイコンを表示するには、Image + clickableではなく `IconButton` を使います。

```
@Composable
fun MainScreen() {
  Column {
    IconButton(onClick = {
      println("Clicked!")
    }) {
      Icon(imageVector = Icons.Default.Add, contentDescription = "Add")
    }
  }
}
```

 `IconButton` のコンテンツ部分には `Icon` を使います。標準アイコンでよければ `Icons.Default.アイコン名` が使えます。
 
Material IconsからSVG(Vector Resource)をとってきた場合は `painter` で指定します。

```
@Composable
fun MainScreen() {
  Column {
    IconButton(onClick = {
      println("Clicked!")
    }) {   
      // painterで指定する
      Icon(
        painter = painterResource(R.drawable.baseline_add_24),
        contentDescription = "Add"
      )
    }
  }
}
```
