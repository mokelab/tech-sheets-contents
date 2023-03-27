Title: InheritedWidgetを使ってDIする

Priority: 10

Flutterの `InheritedWidget` はツリーの上側にいるウィジェットを定数時間で取得可能にするための特殊ウィジェットです。
今回はこれを使って `UserRepository` のようなオブジェクトを取得できるようにしてみます。

AndroidのJetpack Composeでは[CompositionLocal](https://developer.android.com/jetpack/compose/compositionlocal?hl=ja)という名称がついています。

## InheritedWidgetを継承したクラスを作る

今回はクラス名を `AppModule` にしてみます。

```
class AppModule extends InheritedWidget {
  final UserRepository userRepository;
  const AppModule(
      {required this.userRepository, required Widget child, super.key})
      : super(child: child);

  // 更新通知は不要
  @override
  bool updateShouldNotify(covariant InheritedWidget oldWidget) => false;
}
```

## 下位ウィジェットで取得する

今回欲しいのはデータの変更通知が必要ない `AppModule` なので、 `getElementForInheritedWidgetOfExactType()` で取得します。

```
class _MyHomePageState extends State<MyHomePage> {
  void _loginClicked() {
    // キャストが必要
    final module = context
      .getElementForInheritedWidgetOfExactType<AppModule>()
      ?.widget as AppModule;
    final repo = module.userRepository;
    final user = await repo.login();
  }
  ...
}
```

## main()で差し込む

 `runApp()` の引数に `AppModule()` を渡すようにします。差し込みたいオブジェクトはここで作ってしまいましょう。

```
void main() {
  runApp(
      AppModule(userRepository: DefaultUserRepository(), child: const MyApp()));
}
```

## of()を作る

`AppModule` に `of()` を追加して使いやすくします。

```
class AppModule extends InheritedWidget {
  final UserRepository userRepository;
  const AppModule(
      {required this.userRepository, required Widget child, super.key})
      : super(child: child);

  @override
  bool updateShouldNotify(covariant InheritedWidget oldWidget) => false;

  static AppModule of(BuildContext context) =>
      context.getElementForInheritedWidgetOfExactType<AppModule>()?.widget
          as AppModule;
}
```

この `of()` を使うとすっきり書けます。

```
class _MyHomePageState extends State<MyHomePage> {
  void _loginClicked() {
    final repo = AppModule.of(context).userRepository;
    final user = await repo.login();
  }
  ...
}
```

