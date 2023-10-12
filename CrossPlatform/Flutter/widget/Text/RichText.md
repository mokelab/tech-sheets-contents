Title: Flutter の RichText

Priority: 20

[公式ドキュメント：RichText class](https://api.flutter.dev/flutter/widgets/RichText-class.html)

Flutter の RichText を使うと、テキストの一部だけ色やサイズなどを変えることができます。

![RichText](RichText_01.jpg)

```
RichText(
    text: const TextSpan(
    text: "こんにちは、 ",
    style: TextStyle(color: Colors.black),
    children: [
        TextSpan(
        text: "モケラ",
        style: TextStyle(
            color: Colors.green, fontWeight: FontWeight.bold),
        ),
        TextSpan(text: "です♪")
    ],
    ),
)
```
