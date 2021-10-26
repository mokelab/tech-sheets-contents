Title: Jetpack ComposeでFlowを状態として扱う

Priority: 20

Flowは非同期でデータが流れてくるモノです。Jetpack ComposeではこのFlowを状態として扱うことができます。 
最新のデータが取得できた際、UIの必要な部分を再composeしてくれます。

[LiveData](./livedata.html)の時とは異なり、追加のライブラリは必要ありません。

## ViewModelにFlowを返すものを追加する

今回は `StateFlow` を使い、ボタンを押した回数をFlowで返すようにしてみます。さらにカウントアップのためのメソッドも用意してみます。

```kotlin
class MainViewModel: ViewModel() {
    private val _counter = MutableStateFlow(0)
    val counter: StateFlow<Int> = _counter

    fun add() {
        _counter.value = _counter.value + 1
    }
}
```

## ComposableでFlowを状態として扱う

ViewModelに入っているFlowを状態として扱うには、 `collectAsState()` を呼びます。拡張関数として定義されているので追加のimportが必要です。

```kotlin
@Composable
fun MainScreen(
    viewModel: MainViewModel,
) {
    val counter = viewModel.counter.collectAsState()

    Column {
        // nullを返すことはないので気軽に使える
        Text("${counter.value}")
        Button(onClick = {
            viewModel.add()
        }) {
            Text("Add")
        }
    }
}
```

これで、ViewModelを使ってカウントアップする処理が実現できました。
