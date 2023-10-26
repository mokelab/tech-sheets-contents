TItle:Flutter の sqflite でデータを削除する

`sqflite`でデータを削除するには、 `Database.delete()` を使用します。

```
Future<void> _deleteAccount(
  Database db,
  Account account,
) async {
  await db.delete(
    "account",
    where: "_id=?",
    whereArgs: [account.id],
  );
}
```

第 1 引数には削除対象のデータが入っているテーブル名を指定します。

`where` と `whereArgs` はデータの検索や更新時と同様です。

この 2 つを忘れるとテーブル内のデータが全部削除されてしまうので注意しましょう。
