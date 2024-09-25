Title: Jetpack Composeで引っ張って更新を実装する

Priority: 10

[Material3のバージョン1.3.0](https://developer.android.com/jetpack/androidx/releases/compose-material3#1.3.0)で使い方が変わりました！

Jetpack Composeで引っ張って更新(PullToRefresh)を実装するには、以下の3ステップをやります。

- UiStateに更新中の状態を追加する
- LazyColumnを `PullToRefreshBox` で囲む
- refresh中の時の処理を書く

## 更新中の状態を追加する

リスト表示を実装する際、UiStateで表示内容となるリストを管理していると思います。これに更新中かどうかを表す状態を追加します。

```
class MyViewModel : ViewModel() {
  sealed interface UiState {
    data object Initial : UiState
    data object Loading : UiState
    data class Success(
      val data: List<String>,
      val isRefreshing: Boolean, // 追加する
    ) : UiState

    data class Error(val message: String) : UiState
  }

  private val _uiState = MutableStateFlow<UiState>(UiState.Initial)
  val uiState = _uiState.asStateFlow()
  ...
}
```

## LazyColumnを `PullToRefreshBox` で囲む

1.3.0から、LazyColumnを `PullToRefreshBox` で囲むだけでよくなりました。

```
PullToRefreshBox(
  isRefreshing = uiState.isRefreshing,
  onRefresh = {
    refresh() // 更新処理
  },
) {
  LazyColumn(
    modifier = Modifier
      .fillMaxWidth()
      .padding(innerPadding),
  ) {
    items(uiState.data) { item -> ... }
  }
}
```

## refresh中の時の処理を書く

 `isRefreshing` を一旦 `true` にしてから更新処理をViewModelに書いていきます。

```
fun refresh() {
  val currentState = _uiState.value
  if (currentState !is UiState.Success) return

  _uiState.value = currentState.copy(isRefreshing = true)
  viewModelScope.launch {
    try {
      val data = myRepository.fetch()
      _uiState.value = UiState.Success(
        data = data,
        isRefreshing = false,
      )
    } catch (e: CancellationException) {
      throw e
    } catch (e: Exception) {
      _uiState.value = UiState.Error(e.message ?: "Unknown error")
    }
  }
}
```


以下、どうしても1.3.0未満を使わないといけない方向け

Jetpack Composeで引っ張って更新(PullToRefresh)を実装するには、以下の4ステップをやります。

- stateを作る
- nestedScrollを設定する
- PullToRefreshContainerを配置する
- refresh中の時の処理を書く

## stateを作る

 `rememberPullToRefreshState()` を使います。

```
val pullToRefreshState = rememberPullToRefreshState()
```

## nestedScrollを設定する

Scaffoldに対しnestedScrollを設定します。

```
Scaffold(
  modifier = Modifier.nestedScroll(pullToRefreshState.nestedScrollConnection),
) { innerPadding -> }
```

## PullToRefreshContainerを配置する

読込中を表すコンポーザブルを配置します。Box + LazyColumnといった構成にします。

```
Box(modifier = Modifier.padding(innerPadding)) {
  LazyColumn(modifier = Modifier.fillMaxSize()) { ... }

  PullToRefreshContainer(
    state = pullToRefreshState,
    modifier = Modifier.align(Alignment.TopCenter),
  )
}
```

## refresh中の時の処理を書く

 `isRefreshing` を見て、 `LaunchedEffect` を使ってリフレッシュ処理を実行します。

```
if (pullToRefreshState.isRefreshing) {
  LaunchedEffect(Unit) {
    viewModel.refresh()
  }
}
```

## 完成形

```
@Composable
fun MainScreen(viewModel: MainViewModel) {
  val pullToRefreshState = rememberPullToRefreshState()

  Scaffold(
    modifier = Modifier.nestedScroll(pullToRefreshState.nestedScrollConnection),
  ) { innerPadding ->
    Box(modifier = Modifier.padding(innerPadding)) {
      LazyColumn(modifier = Modifier.fillMaxSize()) { ... }

      PullToRefreshContainer(
        state = pullToRefreshState,
        modifier = Modifier.align(Alignment.TopCenter),
      )
    }
  }

  if (pullToRefreshState.isRefreshing) {
    LaunchedEffect(Unit) {
      viewModel.refresh()
    }
  }
}
```
