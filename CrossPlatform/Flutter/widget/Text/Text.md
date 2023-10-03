Title: Flutter の Text

Priority: 10

Text は、単一のスタイルで文字列を表示します。テキストを表示するときに使用しましょう。

[公式ドキュメント](https://api.flutter.dev/flutter/widgets/Text-class.html)

```

Text(
  'Hello, $_name ',
  style: const TextStyle(fontWeight: FontWeight.bold),
)

```

テキストのスタイルは TextStyle()内に記述します。
