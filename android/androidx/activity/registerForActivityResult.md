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

## Can only use lower 16 bits for requestCode で落ちる場合

`launch()` を呼んだときに `java.lang.IllegalArgumentException: Can only use lower 16 bits for requestCode` で落ちることがあります。
これは `appcompat` が依存関係として持ってくる `androidx.fragment` が古い時に発生します。

手元で確認したところ、 `androidx.appcompat:1.2.0` は `androidx.fragment:fragment:1.1.0` を持ってきていました。

`androidx.fragment` の最新版を明示的に追加することで解決できます。

```
dependencies {
    implementation 'androidx.fragment:fragment-ktx:1.3.0-rc01'
}
```

`FragmentActivity` でのリクエストコードの扱いが変わったのが原因のようです。以前は、どのフラグメントに結果を伝えるかの情報を含めるため、使用可能なリクエストコードは16bit以内でした。新方式の導入により、この制限がなくなっている反面、古い `androidx.fragment` を使うと16bitチェックが入ってしまい、ほぼ確実にクラッシュしてしまいます。
