IndexedDBのオブジェクトストアにデータを追加するには、 `add()` や `put()` を使います。 `add()` の場合、
オブジェクトストアにすでに同じキーのオブジェクトがあった場合はエラーとなり、 `put()` の場合は更新となります（なければ作成）

```
const tr = db.transaction([storeName], "readwrite");
const store = tr.objectStore(storeName);

const request = store.put(value);
// add()の場合、キー重複時はエラーになる
// const request = store.add(value);

tr.oncomplete = () => {
    // データの追加更新にすべて成功した場合の処理
};
tr.onerror = (err) => {
    // なにか失敗したときの処理
};
```

トランザクションになっているので、データの追加更新はまとめて行うことができます。
