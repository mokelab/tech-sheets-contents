Title: KtorでGETリクエストを投げる

Priority: 20

KtorでGETリクエストを投げるには `HttpClient` の `get()` を使います。 `suspend` 関数になっているのでコルーチンスコープの中で実行します。

```
viewModelScope.launch {
    try {
        val resp = httpClient.get(Url("https://httpbin.org/get"))
        if (resp.status.value != 200) {
            return@launch
        }
        _respTest.value = resp.body()
    } catch (e: CancellationException) {
        throw e
    } catch (e: Exception) {
        println(e)
    }
}
```

HTTPステータスコードは `status` プロパティに入っています。ボディ部分は `body()` で文字列として取得できます。
