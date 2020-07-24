IndexedDBを開くには、 `indexedDB.open()` を使います。

```
const name = "myDatabase"
const version = 1
const r = indexedDB.open(name, version);
r.onupgradeneeded = (ev) => {
  const db = ev.target.result;
  // オブジェクトストアを作ったり、定義を変更したりする処理
};
r.onsuccess = (ev) => {
  const db = ev.target.result;
  // dbを使った処理
};
r.onerror = (ev) => {
  // 開けなかった
  console.log(ev);
}
```

第1引数にはデータベース名を指定し、第2引数にはデータベースのバージョンを指定します。
ブラウザ側で保存されているデータベースのバージョンと異なるバージョンが指定された際は、 `onupgradeneeded()` が呼ばれた後に
`onsuccess()` が呼ばれます。初回も呼ばれるので、 `onupgradeneeded()` の中でオブジェクトストアを作るようにしましょう。

