Title: Flutter で SQLite

ここでは、Flutter で SQLite データベースを扱う方法を紹介します。

例として、次のようなアカウント情報を扱うことにします。ID は自動採番されるものとします。

```
class Account {
  final int id;
  final String name;
  final int age;

  Account(this.id, this.name, this.age);
}
```

デモプロジェクトは[こちら](https://github.com/mokelab/flutter_demo_sqflite)にあります。

- [データベースを開く](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/open.html)
- [データを追加する](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/insert.html)
- [データを取得する](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/query.html)
- [データを更新する](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/update.html)
- [データを削除する](https://tech.mokelab.com/CrossPlatform/Flutter/sqflite/delete.html)
