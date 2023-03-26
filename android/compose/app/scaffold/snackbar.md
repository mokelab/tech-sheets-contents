Title: Jetpack ComposeでSnackbarを表示する

Priority: 40

Jetpack ComposeでSnackbarを表示するには `Scaffold` と `snackbarHost` を使います。

```
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MainScreen() {
  val hostState = remember { SnackbarHostState() }
  val scope = rememberCoroutineScope()

  Scaffold(
    snackbarHost = { SnackbarHost(hostState) }
  ) { paddingValues ->
    Column(modifier = Modifier.padding(paddingValues)) {
      Button(onClick = {
        scope.launch {
          hostState.showSnackbar("Message")
        }
      }) {
        Text("Snack bar")
      }
    }
  }
}
```

実際にSnackbarを表示するには `snackbarHostState.showSnackbar()` を呼びます。 `suspend fun` になっているのでコルーチンスコープの中で実行します。

```
Button(onClick = {
  scope.launch {
    hostState.showSnackbar("Message")
  }
}) {
  Text("Snack bar")
}
```

実行結果はこんな感じです。

