まずは画面に対応したViewModelクラスを作成します。

```
class MainViewModel : ViewModel() {
    val count: MutableLiveData<Int> by lazy {
        MutableLiveData(0)
    }
}
```

一般的には `LiveData` をメンバーとして持たせます。 `LiveData` の具体的な使い方は [こちら](https://tech.mokelab.com/android/jetpack/arch/livedata/index.html)を参照してください。

