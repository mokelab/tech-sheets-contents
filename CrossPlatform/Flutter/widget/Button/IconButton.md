Title: Flutter の IconButton

Flutter の IconButton を使うと、アイコンをボタン化できます。

ボタンが押されたら、onPressed 関数が呼び出されます。null の場合、ボタンは無効になり、タッチに反応しなくなります。

[公式ドキュメント：IconButton class](https://api.flutter.dev/flutter/material/IconButton-class.html)

![iconButton](iconButton_01.jpg)

```
IconButton(
  icon: const Icon(Icons.account_circle),
  onPressed: () {
    // ボタンが押された時の処理
  },
)
```
