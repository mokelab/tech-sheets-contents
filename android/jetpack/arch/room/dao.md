[Entity](./entity.html)の定義ができたら、次はDAOを作ります。DAOとはデータにアクセスするためのオブジェクトです。

```
@Dao
interface ArticleDAO {
    @Insert
    fun insert(article: Article)

    @Query("SELECT * from article WHERE id=:id")
    fun getById(id: Int): Article

    @Query("SELECT * from article ORDER BY id desc")
    fun getAll(): LiveData<List<Article>>

    @Update
    fun update(article: Article)

    @Delete
    fun delete(article: Article)
}
```

インターフェースに対し、 `@DAO` をつけます。Roomはこれを見て適切なコードを生成します。データの追加を行うメソッドには `@Insert` を、更新を行うメソッドには `@Update` を、削除を行うメソッドには `@Delete` をつけます。

データの取得を行うメソッドには `@Query` をつけ、引数部分にSELECT文を記述します。 `getById()` のように、メソッドに引数がある場合、SELECT文の中でその引数を `:引数名` で使用することができます。

データ取得メソッドの場合、戻り値の型を [LiveData](https://tech.mokelab.com/android/jetpack/arch/livedata/index.html) にすると、Roomによってデータベースの監視機能が提供されます。行の追加といったデータベースに変更が入ると、自動で検索が実行され、セットしている `Observer` に結果が通知されます。



