[Entity](./entity.html)と[DAO](./dao.html)を作ったら、最後に `RoomDatabase` を作ります。これは、1つのデータベースファイルにどのEntity（＝テーブル）を含めるかを指定し、DAOインスタンスを提供する役割をもちます。

```
@Database(entities = [Article::class], version = 1)
abstract class ArticleDB: RoomDatabase() {
    abstract fun articleDAO(): ArticleDAO
}
```

_`RoomDatabase` を継承した抽象クラスにします。 `@Database` で、どのEntityが含まれるかと、データベースのバージョンを指定します。

メソッドで、 `DAO` を返すメソッドを定義します。Roomはこれらの情報から、データベース作成時の処理と、DAOインスタンスを返すメソッドを生成します。



