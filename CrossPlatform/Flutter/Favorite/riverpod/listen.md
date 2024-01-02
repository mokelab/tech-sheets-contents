Title: Riverpodで状態が変わったら何か処理をする

Priority: 40

RiverpodのStateNotifierの状態が変わったタイミングで何か処理をしたい場合（例えばエラー時にSnackbarを表示する等）は、
 `ref.listenManual()` を使います。 `initState()` のタイミングで設定するので、 `ConsumerStatefulWidget` を使います。

## ConsumerStatefulWidgetを作る

 `StatefulWidget` の代わりに `ConsumerStatefulWidget` を継承したクラスを作ります。
 `createState()` の戻り値の型が `ConsumerState<ConsumerStatefulWidget>` になっている点に注意しましょう。

```
class _LoginScreen extends ConsumerStatefulWidget {
  const _LoginScreen();

  @override
  ConsumerState<ConsumerStatefulWidget> createState() => _LoginScreenState();
}
```

## ConsumerStateを作る

 `State<T>` の代わりに `consumerState` を継承したクラスを作ります。

```
class _LoginScreenState extends ConsumerState<_LoginScreen> {
  @override
  Widget build(BuildContext context) {
    // refが使える
  }
}
```

## initStateでlistenManualを呼ぶ

状態が変わったタイミングでラムダ式の中身が呼ばれます。画面遷移等をしたい場合は `WidgetsBinding.instance.addPostFrameCallback()` を使います。

```
ProviderSubscription? _subscription;

@override
void initState() {
  super.initState();
  _subscription = ref.listenManual(
    viewModelProvider,
    (previous, next) {
      switch (next) { ... }
    }
  );
}
```

## listenManual直後に中身を実行する

「画面が表示されたタイミングで処理させたい」みたいな場合は、 `fireImmediately: true` を引数に追加します。

```
ProviderSubscription? _subscription;

@override
void initState() {
  super.initState();
  _subscription = ref.listenManual(
    viewModelProvider,
    (previous, next) {
      switch (next) { ... }
    },
    fireImmediately: true, // これを追加
  );
}
```
