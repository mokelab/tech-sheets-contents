Title: Flutter の sqflite でデータベースを開く

`sqflite` を使ってデータベースを開くには、 `openDatabase()` を使用します。

```
import 'package:sqflite/sqflite.dart';

Database? db;

void main() async {
  db = await openDatabase(
    "my_db.db",
    version: 1,
    onCreate: (database, version) async {
      await database.execute('''create table account(
          _id integer primary key autoincrement,
          name text,
          age int)''');
    },
  );
}
```

第 1 引数にはデータベースのファイル名を指定します。

`version` パラメータにはデータベースのバージョンを指定します。

`onCreate` パラメータでは、データベースが新しく作られた時と、バージョンが変化したときに行う処理を記述します。

今回は account テーブルをここで作成しています。
