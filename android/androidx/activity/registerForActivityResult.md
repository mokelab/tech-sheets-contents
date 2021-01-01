registerForActivityResultを使って結果のあるアクティビティを起動する

結果のあるアクティビティを起動する`startActivityForResult()` と、結果を受け取る `onActivityResult()` はAPI Level 1から存在する歴史あるAPIですが、

- 起動した場所と結果を受け取る場所が離れてしまう
- onActivityResult()の中で条件分岐が必要

といった使いにくさもありました。

イマドキな方法（MADな方法?)では、 `registerForActivityResult` を使います。引数には扱うインテントの種類となる `ActivityResultContract` を渡します。代表的な暗黙的インテントに対応する `ActivityResultContract` はライブラリで定義されています。

```
class MainActivity : AppCompatActivity() {

    private val launcher = registerForActivityResult(
        ActivityResultContracts.GetContent()
    ) { uri ->
        // 外部アプリで選択された後に実行される
        // キャンセルされたらnullが入っていたりする
        Toast.makeText(this, "url=${uri}", Toast.LENGTH_SHORT).show()
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<Button>(R.id.button).setOnClickListener {
            // 引数の型もContractで決まる
            launcher.launch("image/*")
        }
    }
}
```

`registerForActivityResult()` でインテントを投げるためのオブジェクトを作り、必要となる場面で `launch()` を呼びます。インテントにデータを詰め忘れるといった問題も解消できていい感じ。



