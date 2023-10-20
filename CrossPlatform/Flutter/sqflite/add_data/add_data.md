Title: Flutter の sqflite でデータを追加する

[こちら](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/open.html)でデータベースを用意したら、早速テーブルにデータを追加してみましょう。

こちらも Android の `SQLiteDatabase` とほぼ同じだったりします。

```
Future<void> _insertAccount(
  Database db,
  String name,
  int age,
) async {
  final values = <String, dynamic>{
    "name": name,
    "age": age,
  };
  await db.insert(
    "account",
    values,
  );
}
```

実際にデータを追加しているのは `db.insert()` の部分です。

第 1 引数にはテーブル名を記述し、第 2 引数でどの列にどの値をセットするかを指定します。
