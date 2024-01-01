Title: Riverpodで下位ウィジェットから値を取得できるようにする(Provider)

Priority: 20

Riverpodを使うと下位ウィジェットから指定した値（オブジェクト）を取得することができます。リポジトリ等をとってこれるようにすると便利です。

## Providerを作る

 `Provider<T>` でオブジェクトの作り方を指定します。

```
final accountRepositoryProvider = Provider<AccountRepository>((ref) {
  return AccountRepository();
});
```

## ProviderScopeを追加する

 `ProviderScope` を使ってスコープを指定します。リポジトリのようなアプリ全体でひとつだけあればいいようなオブジェクトであれば `runApp()` の位置で指定するとよいでしょう。

```
void main() {
  runApp(
    const ProviderScope(
      child: MyApp(),
    ),
  );
}
```

## ConsumerWidgetを継承する

オブジェクトを使いたいウィジェットを　`StatelessWidget` から `ConsumerWidget` に変更します。 `build()` の引数に `WidgetRef` も追加します。

```
class MainScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // refを使うコード
  }
}
```

## refからオブジェクトを取得する

 `ref.read()` を使って `Provider` で提供しているオブジェクトが取得できます。型情報があるので型安全に取得できます。

```
@override
Widget build(BuildContext context, WidgetRef ref) {
  final accountRepository = ref.read(accountRepositoryProvider);
}
```
