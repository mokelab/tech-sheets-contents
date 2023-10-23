Title: Flutter の sqflite でデータを取得する

[データを追加](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/insert.html)したら、次は取得してみましょう。

やはり Android の `SQLiteDatabase` と使い方はほぼ同じです。

```
Future<List<Account>> _getAllAccount(
  Database db,
) async {
  List<Map> results = await db.query("account");
  // map to account list
  return results.map((Map m) {
    int id = m["_id"];
    String name = m["name"];
    int age = m["age"];
    return Account(id, name, age);
  }).toList();
}
```

テーブルからデータを取ってくる部分は `db.query("account")` です。

第 1 引数には対象となるテーブル名を指定します。

結果は `MapString`, `dynamic` のリストとして返ってきます。

各 `Map` は列名がキーとなっており、`「\_id` は先頭から何番目か」を取得したりする必要はありません。

## 検索条件を加える

上記の方法はテーブル内のデータを全部とってきてしまいます。

例えば「`\_id=1` のデータだけ取得したい」といった場合は、 `where` と `whereArgs` を指定します。

```
List<Map> results = await db!.query(
  "account",
  where: "_id=?",
  whereArgs: [1],
);
```

SQL インジェクションを防ぐため、 `where` の中では ? プレースホルダーを使用します。
