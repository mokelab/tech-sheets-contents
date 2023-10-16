Title: FlutterのOutlinedButton

Priority: 40

[公式ドキュメント：OutlinedButton class](https://api.flutter.dev/flutter/material/OutlinedButton-class.html)

 `OutlinedButton` は、基本的には枠線が描かれた TextButton です。重要だけどアプリのメインではないアクションなど、中程度の強調のボタンに使います。

![OutlinedButton](OutlineButton_01.jpg)

```
OutlinedButton(
  child: const Text("OutlinedButton"),
  onPressed: () {
    // ボタンが押されたときの処理
  },
)
```
