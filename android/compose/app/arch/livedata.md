Title: Jetpack ComposeでLiveDataを状態として扱う

Priority: 10

LiveDataは監視可能なデータのいれものです。Jetpack ComposeではこのLiveDataを状態として扱うことができます。
最新のデータが取得できた際、UIの必要な部分を再composeしてくれます。

## ライブラリを追加する

Jetpack ComposeでLiveDataを使うには、 `runtime-livedata` を追加します。

```gradle
dependencies {
    implementation "androidx.compose.runtime:runtime-livedata:$compose_version"
}
```

## ViewModelにLiveDataを追加する

今回はボタンを押した数をいれておくLiveDataを用意してみます。さらにカウントアップのためのメソッドも用意してみます。

```kotlin
class MainViewModel: ViewModel() {
    // 初期値は0としました
    private val _counter = MutableLiveData(0)
    val counter: LiveData<Int> = _counter

    fun add() {
        _counter.value = _counter.value!! + 1
    }
}
```

## ComposableでLiveDataを状態として扱う

ViewModelに入っているLiveDataを状態として扱うには、 `observeAsState()` を呼びます。拡張関数として定義されているので追加のimportが必要です。

```kotlin
@Composable
fun MainScreen(
    viewModel: MainViewModel,
) {
    // 状態として取得
    val counter = viewModel.counter.observeAsState()

    Column {
        counter.value?.let { count ->
            Text("$count")
        }
        Button(onClick = {
            viewModel.add()
        }) {
            Text("Add")
        }
    }
}
```

これで、ViewModelを使ってカウントアップする処理が実現できました。





