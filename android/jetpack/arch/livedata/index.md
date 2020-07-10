LiveDataとは、アクティビティやフラグメントのライフサイクルを意識した上で、最新のデータを提供するための仕組みを提供してくれるものです。通常、 [ViewModel](https://tech.mokelab.com/android/jetpack/arch/viewmodel/index.html)とセットで使うので、dependenciesには次の項目を追加します。

```
implementation 'androidx.lifecycle:lifecycle-livedata-ktx:2.2.0'
```

 - [ViewModelにLiveDataを持たせる](./create.html)
 - [LiveDataを監視する](./observe.html)
 - [MutableLiveDataに値をセットする](./mutable_set.html) 


