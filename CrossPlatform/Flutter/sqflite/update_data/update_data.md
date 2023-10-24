Title: Flutter の sqflite でデータを更新する

sqflite でデータを更新するには、 `Database.update()` を使用します。

```
Future<void> _updateAccount(
  Database db,
  int id,
  String name,
  int age,
) async {
  var values = <String, dynamic>{
    "name": name,
    "age": age,
  };
  await db.update(
    "account",
    values,
    where: "_id=?",
    whereArgs: [id],
  );
}
```

第 1 引数・第 2 引数は `insert()` と同様です。

どの行を更新するかの条件は、 `query()` と同様に `where` と `whereArgs` で指定します。
