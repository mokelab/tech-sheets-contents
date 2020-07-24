IndexedDBのオブジェクトストアからデータを削除するには、 `delete()` を使用します。

```
const tr = db.transaction([storeName]);
const store = tr.objectStore(storeName);

const request = store.delete('id1122');

request.onsuccess = () => {
    // 削除に成功したときの処理
}
request.onerror = (err) => {
    // 削除に失敗したときの処理
};
```

削除にはキーが必要なので注意しましょう。
