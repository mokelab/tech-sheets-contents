Title: Jetpack Composeで画面遷移させる

Jetpack Composeで画面遷移させるには、 [NavHostを追加する](./navHost.html) の回で作成した `NavController` を使います。

まず、遷移先となる `SecondScreen` を作ります。

```kotlin
@Composable
fun SecondScreen() {
    Text("2nd Screen!!")
}
```

そして `NavHost` の `{}` の中に追加します。今回は画面名を `second` にしてみます。

```
NavHost(navController = navController, startDestination = "main") {
    composable("main") {
        MainScreen()
    }
    // ここを追加
    composable("second") {
        SecondScreen()
    }
}
```


ボタンタップ時に画面遷移させてみたいので、 `MainScreen` にボタンを追加します。

```kotlin
@Composable
fun MainScreen() {
    Column {
        Text("Hello")
        Button(onClick = {
            /* later */
        }) {
            Text("Next")
        }
    }
}
```

ボタンタップ時に `NavController` の `navigate()` が呼ばれるようにします。 `MainScreen` の引数に `NavController` を追加し、 `onClick` の中で呼びます。
引数には遷移先となる画面名を指定します。

```kotlin
@Composable
fun MainScreen(navController: NavController) {
    Column {
        Text("Hello")
        Button(onClick = {
            navController.navigate("second")
        }) {
            Text("Next")
        }
    }
}
```

`NavHost` の部分も修正します。全体では次のようになります。

```kotlin
@Composable
fun MyApp() {
    ComposeAppTheme {
        val navController = rememberNavController()
        Scaffold(
            topBar = { MyTopAppBar() },
        ) {
            NavHost(navController = navController, startDestination = "main") {
                composable("main") {
                    // 引数としてnavControllerを渡す
                    MainScreen(navController = navController)
                }
                composable("second") {
                    SecondScreen()
                }
            }
        }
    }
}
```

これでボタンをタップすると `SecondScreen` に遷移し、端末のバックボタンで `MainScreen` に戻ってきます。

## 抽象化する

ここまで紹介した方法だと、 `NavController` が各画面に直接渡されます。これだとテスト時にやりづらくなるので、各画面はラムダ式を受け取るようにして抽象化を行います（[公式ドキュメント](https://developer.android.com/jetpack/compose/navigation?hl=ja#testing)）

```kotlin
@Composable
fun MainScreen(toSecond: () -> Unit) {
    Column {
        Text("Hello")
        Button(onClick = {
            toSecond()
        }) {
            Text("Next")
        }
    }
}
```

`NavHost` の部分は次のようになります。

```kotlin
@Composable
fun MyApp() {
    ComposeAppTheme {
        val navController = rememberNavController()
        Scaffold(
            topBar = { MyTopAppBar() },
        ) {
            NavHost(navController = navController, startDestination = "main") {
                composable("main") {
                    MainScreen {
                        navController.navigate("second")
                    }
                }
                composable("second") {
                    SecondScreen()
                }
            }
        }
    }
}
```
