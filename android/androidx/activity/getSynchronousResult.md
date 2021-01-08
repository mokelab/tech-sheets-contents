ActivityResultContractでインテントを投げずに結果を返す

`ActivityResultContract` は結果のあるアクティビティを起動するのに使います。
しかしパラメータの中身によってはインテントを投げずに結果を返したほうがはやい場合もあるかもしれません（例えば不正なパラメータが渡されたなど）。

その場合、 `getSynchronousResult()` をオーバーライドすることでインテントを投げずに結果を返すことができます。

```
class NextActivityResultContract: ActivityResultContract<Int, String>() {
  override fun createIntent(context: Context, input: Int?): Intent { ... }
  override fun parseResult(resultCode: Int, intent: Intent?): String { ... }

  override fun getSynchronousResult(context: Context, input: Int?): SynchronousResult<String>? {
    if (input == 1) {
      // 画面遷移不要で結果を返しちゃえ
      return SynchronousResult("OK")
    }
    return null
  }
}
```

`null` を返すとインテントを作成して投げる処理が行われます。

## どんな場面で使う？

すいません、アプリ開発者が使う場面が浮かびませんでした。

なお、ライブラリでは `RequestPermission` や `RequestMultiplePermissions` で使われていました。すでに権限取得済みだったらインテントを投げる必要はないですね。

```
public static final class RequestPermission extends ActivityResultContract<String, Boolean> {

  @NonNull
  @Override
  public Intent createIntent(@NonNull Context context, @NonNull String input) { ... }

  @NonNull
  @Override
  public Boolean parseResult(int resultCode, @Nullable Intent intent) { ... }

  @Override
  public @Nullable SynchronousResult<Boolean> getSynchronousResult(
      @NonNull Context context, @Nullable String input) {
    if (input == null) {
      return new SynchronousResult<>(false);
    } else if (ContextCompat.checkSelfPermission(context, input)
         == PackageManager.PERMISSION_GRANTED) {
      return new SynchronousResult<>(true);
    } else {
      // proceed with permission request
      return null;
    }
  }
}
```


