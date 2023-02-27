Title: Jetpack ComposeアプリにNavHostを追加する

Navigationを使ってJetpack Composeを使用するアプリに画面遷移機能を追加するには、まずNavHostを追加します。

アプリにNavHostを追加するには、次の2ステップを行います。

- NavControllerを作る
- Scaffoldの中でNavHostを作る

## NavControllerを作る

アプリのルートとなるComposableの中で `NavController` を作ります。再composeの際に情報が失われると困るので、 `rememberNavController()` を使って作ります。

```
@Composable
fun MyApp() {
    ComposeAppTheme {
        val navController = rememberNavController()
        ...
    }
}
```

## Scaffoldの中でNavHostを作る

次に、 `Scaffold` の中でNavHostを作ります。各画面に対応するComposableには文字列で名前をつけていきます。今回は最初の1画面のみなので `main` にしておきます。

```
@Composable
fun MyApp() {
    ComposeAppTheme {
        val navController = rememberNavController()
        Scaffold(
            topBar = { MyTopAppBar() },
        ) {
            NavHost(navController = navController, startDestination = "main") {
                composable("main") {
                    MainScreen()
                }
            }
        }
    }
}
```

`NavHost` の `startDestination` で、最初にどの画面(Composable)が表示されるかを指定します。

`NavHost` の `{}` の中で、 `composable(画面名)` を画面の数だけ作り、その中でどのComposableを表示させるかを指定します。
