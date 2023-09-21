Title: Flutter で ライトとダーク両方のテーマを設定する
Priority: 10

Flutter の`flex_color_scheme` を使うと、アプリのテーマを簡単に設定することができます。[公式ドキュメント](https://pub.dev/packages/flex_color_scheme)

## パッケージの追加

`dart pub add flex_color_scheme` または `flutter pub add flex_color_scheme`をします。

`MaterialApp`　の `theme` プロパティに `FlexThemeData.light` を、`darkTheme` プロパティに `FlexThemeData.dark` を割り当てます。

また、両方のテーマモードで `FlexThemeData` の `scheme` プロパティに `FlexScheme.mandyRed` を設定します。

そして、`themeMode` プロパティに `ThemeMode.system` を設定することで、端末で設定されているテーマモードを取得して、表示するテーマを切り替えます。

```dart
import 'package:flex_color_scheme/flex_color_scheme.dart';

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: FlexThemeData.light(scheme: FlexScheme.mandyRed),
      darkTheme: FlexThemeData.dark(scheme: FlexScheme.mandyRed),
      themeMode: ThemeMode.system,
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

```
