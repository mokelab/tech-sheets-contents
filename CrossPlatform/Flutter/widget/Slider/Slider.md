Title: Flutter の Slider

[公式ドキュメント：Slider class](https://api.flutter.dev/flutter/material/Slider-class.html)

`Slider` は、ユーザーがドラッグして値を変更できるウィジェットです。音量や明るさの調整、色の選択など、さまざまな用途に使用できます。

![Slider](Slider_01.jpg)

```
double _currentSliderValue = 50;

@override
Widget build(BuildContext context) {
return Slider(
    value: _currentSliderValue,
    min: 0,
    max: 100,
    onChanged: (double value) {
        // 値が変更されたときの処理
    });
}
```

`Slider` を動かすためには、`onChanged` で `setState` を使って値を更新します。

![Slider](Slider_02.jpg)

```
double _currentSliderValue = 50;

@override
Widget build(BuildContext context) {
return Slider(
    value: _currentSliderValue,
    min: 0,
    max: 100,
    onChanged: (double value) {
        setState(() {
        _currentSliderValue = value;
        });
    });
}
```
