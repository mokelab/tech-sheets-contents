ViewModelに入っているLiveDataには最新のデータが入っています。これをUIに反映させるために監視しましょう。

監視するには、 `observe()` を呼びます。ここでは、カウント値が変化したら `TextView` にその値を表示するようにしてみます。

```
override fun onActivityCreated(savedInstanceState: Bundle?) {
    super.onActivityCreated(savedInstanceState)

    this.model.count.observe(viewLifecycleOwner, Observer { newCount ->
        this.countText.text = "$newCount"
    })
}
```

_`observe()` の第1引数にはライフサイクルオーナーを指定します。フラグメントで使用する場合は、Viewの破棄のタイミングで監視を終える必要があるため、 `viewLifecycleOwner` を指定します。通常、何かを監視する場合、不要になった時点で監視を終了する必要があります。 `LiveData` は引数としてライフサイクルオーナーを受け取ることで、監視の終了を自動で行ってくれます。

