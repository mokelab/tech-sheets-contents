Title: FlutterでPOSTリクエストを投げる

Priority: 20

FlutterでPOSTリクエストを投げるには、 http パッケージの `post()` を呼びます。

## パッケージのインポート

JSON文字列を送信する場合は `dart:convert` もインポートします。

```
import 'dart:convert';

import 'package:http/http.dart' as http;
```

## リクエストの送信

送信時のHTTPヘッダーは `Map<String, String>`で指定します。ボディ部分にJSON文字列を送信する場合は、 `json.encode()` を使用します。

ここでは例として `httpbin` にリクエストを投げてみることにします。

```
void _request() async {
  Uri url = Uri.parse("https://httpbin.org/post");
  Map<String, String> headers = {'content-type': 'application/json'};
  String body = json.encode({'name': 'moke'});

  http.Response resp = await http.post(url, headers: headers, body: body);
  if (resp.statusCode != 200) {
    setState(() {
      int statusCode = resp.statusCode;
      _content = "Failed to post $statusCode";
    });
    return;
  }
  setState(() {
    _content = resp.body;
  });
}
```




