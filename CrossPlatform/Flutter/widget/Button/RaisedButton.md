Title: FlutterのRaisedButton

Priority: 1000

## 注意

本Widgetは廃止され、代わりに[ElevatedButton](./ElevatedButton.html)を使うようになりました。

## 旧記事

RaisedButtonは、高さ(elevation)の設定されたボタンです。大事なアクションの決定をさせるときなどに使用しましょう。

![Button](./raisedbutton.png width=236 height=144)

```
RaisedButton(
  child: Text("OK"),
  onPressed: () { print('ok'); },
),
```
