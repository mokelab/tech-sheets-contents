[こちら](./create.html)で用意した `MutableLiveData` は、とても簡単に説明すると「監視可能なデータの入れ物」です。ここでは値を外からセットする方法を紹介します。

```
 val button = root.findViewById<Button>(android.R.id.button1)
 button.setOnClickListener {
    this.model.count.value = this.model.count.value!! + 1
 }
```

ボタンをタップするとカウントを増やす例です。`MutableLiveData` に値をセットするには `setValue()` を、セットされている値を取り出すには `getValue()` を使います。Kotlinの場合は上記の例のようにプロパティ構文が使えますが、初期値が設定されていない場合、 `getValue()` は `null` を返すので注意しましょう。

なお、 `setValue()` はメインスレッドでしか呼べません。 `AsyncTask` のようなワーカースレッドから呼ぶと、次のような例外が発生します。

```
java.lang.IllegalStateException: Cannot invoke setValue on a background thread
    at androidx.lifecycle.LiveData.assertMainThread(LiveData.java:461)
    at androidx.lifecycle.LiveData.setValue(LiveData.java:304)
```

ワーカースレッドから値をセットする場合は次のように `postValue()` を使います。

```
// AsyncTaskの中
override fun doInBackground(vararg params: Void?): Void? {
    model.count.postValue(model.count.value!! + 1)
    return null
}
```


