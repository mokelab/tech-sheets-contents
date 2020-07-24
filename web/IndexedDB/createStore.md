IndexedDBにオブジェクトストア（テーブルみたいなもの）を作るには、 `db.createObjectStore()` を使います。
データベースのバージョンに変化があったときのみ実行されるようにしましょう。

```
r.onupgradeneeded = (ev) => {
  const db = ev.target.result;
  // オブジェクトストアを作ったり、定義を変更したりする処理
  db.createObjectStore("myStore", { keyPath: "id" });
};
```

第1引数にはストア名を指定し、第2引数にはキーとなるフィールド名を指定したりします。
