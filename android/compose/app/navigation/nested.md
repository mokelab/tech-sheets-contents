Title: Navigation Composeでグラフを入れ子にする

公式ドキュメントは[こちら](https://developer.android.com/jetpack/compose/navigation#nested-nav)

 `NavHost` の中で `composable()` の代わりに `navigation()` を使うと、グラフを入れ子にすることができます。

```
NavHost(navController, startDestination = "top") {
  navigation(route = "login", startDestination = "login/login") {
    composable("login/login") { ... }
    composable("login/reset_password") { ... }
  }
  navigation(route = "main", startDestination = "main/home") {
    composable("main/home") { ... }
  }
}
```

 `route` パラメータと `startDestination` を同じ値にするとエラーとなり、実行時にクラッシュします。
また、入れ子の中で追加する `composable()` のルートは全体で一意となる必要があります。重複した場合、どの設定が使われるかの保証はありません（多分。。。）

## 拡張関数で定義する

`NavGraphBuilder` に対し、拡張関数で定義する方法が公式ドキュメントで紹介されています。

```
// 引数は必要に応じて設定
fun NavGraphBuilder.userInfoGraph(navController: NavController, route: String) {
  navigation(route = route, startDestination = "${route}/top") {
    composable("${route}/top") { ... }
  }
}
```

定義した拡張関数を、 `NavHost` の中や他の `navigation()` の中で使います。

```
NavHost(navController, startDestination = "top") {
  userInfoGraph(navController, "user")
  ...
}
```

