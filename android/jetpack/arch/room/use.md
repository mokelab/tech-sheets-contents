[Entity](./entity.html)と[DAO](./dao.html)と[Database](./database.html)ができたら、準備は完了です。最後にデータベース操作を実装しましょう。

まず、 `Database` と `DAO` 置き場となるViewModelを作りましょう。Databaseを作る際に `ApplicationContext` が必要となるので、 `AndroidViewModel` を継承させておきます。

```
class MyViewModel(application: Application):
        AndroidViewModel(application) {
    val db = Room.databaseBuilder(application, ArticleDB::class.java, "article-db").build()
    val dao = db.articleDAO()
}
```

_`RoomDatabase`を作るには、 `Room.databaseBuilder().build()` を使います。第2引数には定義した `RoomDatabase` クラスを指定し、第3引数にはデータベースファイル名を指定します。

次に、このViewModelを `Fragment` で取得しましょう。`RoomDatabase` オブジェクトはアプリで複数生成すべきではないので、 `Activity` に紐づけたViewModelで取得します。

```
class MyFragment: Fragment(R.layout.fragment_my) {
    private val viewModel: MyViewModel by activityViewModels()
}
```

データの追加はDAOで定義したメソッドを呼ぶだけです。UIスレッドで呼ぶと例外が発生するので、ワーカースレッドで実行されるようにします。ViewModelにある`viewModelScope`を使うとよいでしょう。

```
class MyViewModel(application: Application):
        AndroidViewModel(application) {
    fun insert() {
        viewModelScope.launch {
            withContext(Dispatchers.IO) {
                val title = "記事タイトル"
                val content = "記事本文"
                val article = Article(0, title, content)
                viewModel.dao.insert(article)
            }
        }
    }
}
```

データの取得もDAOで定義したメソッドを呼ぶだけです。 `LiveData`を返す場合は `observe` しておくと、自動で最新のデータが取得できます。

```
// this is Fragment
this.viewModel.dao.getAll().observe(viewLifecycleOwner, Observer {
    adapter.submitList(it)
    adapter.notifyDataSetChanged()
})
```

