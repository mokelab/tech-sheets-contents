Title: Comppsableが表示されたタイミングでコルーチンを起動する(LaunchedEffect)

Composableは関数なので、次のように表示のタイミングで処理（副作用）を書きたくなります。

```
@Composable
fun TopScreen(id: String) {
  // サーバーからデータ取得するでー
  val user = getUser(id)
  
  Text(user.name)
}
```

しかしComposable関数は状態の変化などで何度も呼ばれます。またコルーチンスコープ外なのでsuspend関数も呼べません。

Composableが表示されたタイミングで処理を実行したい場合は、 `LaunchedEffect` を使います。

```
@Composable
fun LaunchedEffectScreen(
    back: () -> Unit,
) {
    var counter by remember { mutableStateOf(0) }

    LaunchedEffect(Unit) {
        while (true) {
            delay(1000)
            ++counter
        }
    }

    // HasBackScaffoldは自作のComposable
    HasBackScaffold(
        title = stringResource(id = R.string.effect_launched_effect),
        back = back,
    ) { paddingValues ->
        Text(
            "Count=${counter}",
            modifier = Modifier.padding(paddingValues)
        )
    }
}
```
 `LaunchedEffect` の引数にはキーとなるオブジェクトを指定します。再Composeのタイミングでキーの値が変化した際、実行しているコルーチンを中断し再起動してくれます。
 
 
