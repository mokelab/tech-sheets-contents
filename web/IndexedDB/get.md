IndexedDBのオブジェクトストアからデータを取得するには、 `get()` や `getAll()` を使用します。

```
const tr = db.transaction([storeName]);
const store = tr.objectStore(storeName);
// 全件取得
const request = store.getAll();
// キー指定で1件取得
// const request = store.get("id001");

request.onsuccess = (ev) => {
    // get()の場合はオブジェクトそのものが入っている
    // getAll()の場合は配列
    const items = ev.target.result;
};
request.onerror = (err) => {
    // 取得に失敗したときの処理
};
```

`getAll()` の場合は配列として、 `get()` の場合はオブジェクトが結果として返ってきます。
