Title: Hiltを使ってViewModelに依存性を注入(DI)する

Priority: 10

本記事はJetpack Composeを使うアプリにおいて、Hiltを使ってViiewModelに依存性を注入(DI)する方法を解説します。
Viewシステム(レイアウトXML/フラグメント)の場合は使用するライブラリ等が一部異なるので注意してください。

公式ドキュメントは[こちら](https://developer.android.com/jetpack/compose/libraries?hl=ja#hilt)です。本記事執筆時はやや記事が足りないので本記事を活用してください。

## ライブラリを追加する

まず、プロジェクトのルートにある `build.gradle` でライブラリを追加します。

```gradle
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    ...
    dependencies {
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
        classpath 'com.google.dagger:hilt-android-gradle-plugin:2.36' // これを追加
    }
}
```

次に、 `app/build.gradle` にもライブラリを追加します。プラグインも追加します（kotlin-kaptはおそらくKSPに置き換えられるので、置き換え後に本記事を見た方は @mokelabまでお知らせください)。

```gradle
plugins {
    ...
    // この２つを追加
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}

dependencies {
    ...
    implementation "com.google.dagger:hilt-android:2.36"
    kapt "com.google.dagger:hilt-android-compiler:2.36"
    // Jetpack Compose用のライブラリ
    implementation 'androidx.hilt:hilt-navigation-compose:1.0.0-alpha03'
}
```

## アプリケーションクラスを作る

Hiltを使うには `@HiltAndroidApp` のついたアプリケーションクラスを作る必要があります。

```kotlin
@HiltAndroidApp
class ComposeApplication: Application()
```

AndroidManifest.xmlにも登録します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <application
        ...
        android:name=".ComposeApplication">
        <activity>
        ... 
        </activity>
    </application>
</manifest>
```

## コンストラクタを修正する

今回はToDoを扱う `ToDoRepository` を用意し、必要とする場面では `ToDoRepositoryImpl` が使われるようにしてみます。

```kotlin
interface ToDoRepository {
   ...
}

// @Inject constructorにする
class ToDoRepositoryImpl @Inject constructor(): ToDoRepository {
}
```

コンストラクタに `@Inject constructor()` をつけます。これがないとHiltはインスタンスを作ってくれません。

## モジュールを作る

Hiltでは、「このインターフェースのオブジェクトがほしいと言われたら、このインスタンスを渡してね」という対応を作ってあげる必要があります。

インターフェースと実装クラスを繋げるには、 `@Binds` を使います。リポジトリオブジェクトは一つでいいので `@Singleton` もつけます。

```kotlin
@Module
@InstallIn(SingletonComponent::class)
abstract class MainModule {
    @Binds
    @Singleton
    abstract fun bindToDoRepository(impl: ToDoRepositoryImpl): ToDoRepository
}
```

すごく不思議なメソッド定義ですが、「そういうもの」として定義してください。

## アクティビティの修正

アクティビティには `@AndroidEntryPoint` をつけます。

```kotlin
@AndroidEntryPoint
class MainActivity : ComponentActivity() {
    ...
}
```

## ViewModelの修正

ゴールはViewModelに必要なオブジェクトをDIすることなので、ViewModelも修正します。 `@HiltViewModel` をつけ、
コンストラクタは `@Inject constructor()` にします。そして必要となるオブジェクトをコンストラクタの引数として受け取ります。

```kotlin
@HiltViewModel
class MainViewModel @Inject constructor(
    private val repo: ToDoRepository
): ViewModel() {
    ...
}
```

## NavHostの修正

ようやくJetpack Compose特有の話題がでてきました。ViewModelオブジェクトを取得しているNavHostの部分を修正します。

```kotlin
NavHost(navController = navController, startDestination = "main") {
    composable("main") {
        // hiltViewModel() を使う
        val viewModel: MainViewModel = hiltViewModel()
        MainScreen(viewModel) {
            navController.navigate("second")
        }
    }
}
```
　
これで、ViewModelが必要とするオブジェクトをHiltが注入した上でViewModelオブジェクトを作ってくれるようになります。



