Title: Navigation Composeでパラメータを渡す

Priority: 60

Navigation Composeで画面遷移時にパラメータを渡すには、ルートのパスパラメータとして渡します。
`Parcelable` のようなオブジェクトは渡せないので注意しましょう。

パラメータはルート中で `{}` を使って表します。

```
composable("users/{userId}") { entry ->
  val userId = entry.arguments?.getString("userId")
  ...
}
```

## ViewModelで直接受け取る

ViewModelに `SavedStateHandle` をプロパティとして追加すると、パラメータを直接受け取ることもできます。

```
@HiltViewModel
class UserDetailViewModel @Inject constructor(
  private val savedStateHandle: SavedStateHandle,
) : ViewModel() {
  private val userId = savedStateHandle.get<String>("id") ?: ""
}
```

## String以外で受け取る

　`arguments` でこのパラメータはこの型だよーという情報を与えると、String以外で受け取ることもできます。

```
composable(
  "users/{userId}",
  arguments = listOf(
    navArgument("userId") {
      type = NavType.LongType
    }
  )
) { entry ->
  val userId = entry.arguments?.getLong("userId")
  ...
}
```

