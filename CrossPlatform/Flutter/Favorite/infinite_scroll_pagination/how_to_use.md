Title: Flutterで追加読み込みしながらリスト表示する
Priority: 10

Flutterの `infinite_scroll_pagination` を使うと追加読み込みしながらリスト表示することができます。
[公式ドキュメント](https://pub.dev/packages/infinite_scroll_pagination)

## パッケージの追加

 `flutter pub add` します。
 
```
% flutter pub add infinite_scroll_pagination
```

## PagingControllerを作る

続きをとってくるのに使うキーを `DateTime` にして、 `Article` のリストをとってくる場合は次のようにします。

```
class _ArticleListScreenState extends State<ArticleListScreen> {
  final PagingController<DateTime, Article> _pagingController =
      PagingController(firstPageKey: DateTime.now());

  @override
  void dispose() {
    _pagingController.dispose();
    super.dispose();
  }
}
```      

## PageRequestListener部分を作る

キーを元にデータをとってくる部分を作ります。とってきたデータが一番最後かどうかでappendする際のメソッドを変更します。

```
class _ArticleListScreenState extends State<ArticleListScreen> {
  final PagingController<DateTime, Article> _pagingController =
      PagingController(firstPageKey: DateTime.now());

  @override
  void initState() {
    _pagingController.addPageRequestListener((pageKey) {
      _fetch(pageKey);
    });
    super.initState();
  }

  Future<void> _fetch(DateTime key) async {
    final module = Provider.of<AppModule>(context, listen: false);
    try {
      final loadedArticles = await module.articleRepository().getList(key);
      final hasNext = loadedArticles.isNotEmpty;
      if (hasNext) {
        _pagingController.appendPage(loadedArticles, loadedArticles.last.date);
      } else {
        _pagingController.appendLastPage(loadedArticles);
      }
    } catch (e) {
      _pagingController.error = e;
    }
  }
}
```

## PagedListViewを配置する

1行分のWidgetは　`builderDelegate` で指定します。

```
class _ArticleListScreenState extends State<ArticleListScreen> {
  final PagingController<DateTime, Article> _pagingController =
      PagingController(firstPageKey: DateTime.now());

  ...
  @override
  Widget build(BuildContext context) {
    return PagedListView<DateTime, Article>(
      pagingController: _pagingController,
      builderDelegate: PagedChildBuilderDelegate<Article>(
          itemBuilder: (context, article, index) {
        return ListTile(title: Text(article.subject));
      }),
    );
  }
}
```


