まずは `Entity` となるクラスを作ります。Roomはこの情報を元にテーブルを作ります。

```
@Entity
data class Article(
    @PrimaryKey(autoGenerate = true) val id: Int,
    val title: String,
    val content: String)
```

まず、クラスに対し `@Entity` をつけます。次にフィールドを定義していきます。各フィールドがテーブルの列になります。 `@PrimaryKey` をつけると、その列は主キーになり、 `autoGenerate = true` をつけると `AUTOINCREMENT` になります。

上の例のようにフィールドをnon-nullにすると、テーブルでは `NOT NULL` 制約が付与されます。NULLを許可したい場合は、次のようにnullableにします。

```
// content列はNULLを許可する
@Entity
data class Article(
    @PrimaryKey(autoGenerate = true) val id: Int,
    val title: String,
    val content: String?)
```

既存のテーブルをRoomで操作できるようにする場合は注意しましょう。

