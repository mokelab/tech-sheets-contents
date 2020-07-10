LiveData オブジェクトは通常 `ViewModel` に持たせて使用します。ここでは例として、カウントを保持する `LiveData` を持たせてみます。

```
class MainViewModel : ViewModel() {
    val count: MutableLiveData<Int> by lazy {
        MutableLiveData(0)
    }
}
```

外部から値を変更したい場合は `MutableLiveData` を使用します。

