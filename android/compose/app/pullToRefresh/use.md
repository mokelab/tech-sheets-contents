Title: Jetpack Composeで引っ張って更新を実装する

Priority: 10

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

