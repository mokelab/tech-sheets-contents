Title: Jetpack Composeで結果のあるアクティビティを起動する

Priority: 30

View System版では結果のあるアクティビティを起動するには `registerForActivityResult()` を使いました。

Jetpack Composeでは `rememberLauncherForActivityResult()` を使います。
公式ドキュメントは[こちら](https://developer.android.com/jetpack/compose/libraries?hl=ja#activity_result)

```
@Composable
fun MainScreen() {
  var uri by remember { mutableStateOf<Uri?>(null) }
  val launcher = rememberLauncherForActivityResult(GetContent()) {
    uri = it
  }
  Column {
    Button(onClick = {
      launcher.launch("image/*")
    }) {
      Text("Pick Content")
    }
    if (uri != null) {
      Text("uri=${uri}")
    }
  }
}
```

