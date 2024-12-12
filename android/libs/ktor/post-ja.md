Title: KtorでPOSTリクエストを投げる

Priority: 30

KtorでPOSTリクエストを投げるには、 `HttpClient` の `post()` を使います。送信するボディ部分は `setBody()` で指定します。

```
viewModelScope.launch {
    try {
        val resp = httpClient.post(Url("https://httpbin.org/post")) {
            setBody(JSONObject().put("name", "moke").toString())
        }
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
