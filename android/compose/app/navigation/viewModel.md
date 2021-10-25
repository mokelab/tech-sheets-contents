Title: Jetpack Composeで各画面にViewModelを追加する

Android Architecture Componentで登場したViewModelはJetpack Composeでも用意されています。

ViewModelとは、

- 画面(Screen)に関するデータの保持と操作を担当
- 画面回転といったconfiguration changeが生じてもインスタンスは保持される

という性質をもったオブジェクトです。

## ライブラリを追加する

アプリでViewModelを使うには、 `lifecycle-viewmodel-compose` を追加する必要があります。

```gradle
dependencies {
    ...
    implementation "androidx.lifecycle:lifecycle-viewmodel-compose:2.4.0-rc01"
}
```

## ViewModelを継承したクラスを作る

Viewシステムの時と同様に `ViewModel` を継承したクラスを作ります。今回は `MainScreen` 用のViewModelとして `MainViewModel` を作ります。

```kotlin
class MainViewModel: ViewModel() {
}
```

## ViewModelをパラメータとして受け取る

画面のルートとなるComposableで、ViewModelをパラメータとして受け取るようにします。

```kotlin
@Composable
fun MainScreen(
    viewModel: MainViewModel, //　追加した
    toSecond: () -> Unit,
) {
    ...
}
```

## NavHostの中でインスタンスを取得する

ViewModelのインスタンスは `NavHost` の中で `viewModel()` を使って取得します。
Navigation Composeを使って画面遷移を実現している場合、今どの画面にいるかを表す `navBackStackEntry` に関連づけられてViewModelが作られるようになります。

```kotlin
NavHost(navController = navController, startDestination = "main") {
    composable("main") {
        // ViewModelインスタンスの取得
        val viewModel: MainViewModel = viewModel()
        // そしてComposable関数のパラメータとして渡す
        MainScreen(viewModel) {
            navController.navigate("second")
        }
    }
    composable("second") {
        SecondScreen()
    }
}
```
