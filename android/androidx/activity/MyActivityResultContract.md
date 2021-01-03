ActivityResultContractを自作する

代表的な `ActivityResultContract` は `ActivityResultContracts` で定義されています。今回は自作してみましょう。

## 遷移先のアクティビティを作る

例として、ボタンをタップすると、 `setResult()` で結果を返すだけのアクティビティを作ります。結果の型は文字列ひとつにしておきます。

```
class NextActivity: AppCompatActivity(R.layout.next_activity) {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        findViewById<Button>(R.id.button).setOnClickListener {
            val data = Intent()
            data.putExtra("data", "RESULT!!")
            setResult(RESULT_OK, data)
            finish()
        }
    }
}
```

## ActivityResultContractを継承したクラスを作る

型引数の1つ目はアクティビティ起動時のパラメータで、2つ目は結果の型です。今回は使用していませんがInt型を受け取ることにします。

```
class NextActivityResultContract: ActivityResultContract<Int, String>() {
    override fun createIntent(context: Context, input: Int?): Intent {
        val resId = input ?: android.R.string.ok
        return Intent(context, NextActivity::class.java).apply {
            putExtra("resId", resId)
        }
    }

    override fun parseResult(resultCode: Int, intent: Intent?): String {
        if (resultCode != Activity.RESULT_OK) {
            return ""
        }
        return intent?.getStringExtra("data") ?: ""
    }
}
```

## 使ってみる

`ActivityResultContracts` で定義されているものと同じように使えます。

```
class MainActivity : AppCompatActivity() {

    private val launcher = registerForActivityResult(
        // 自作のActivityResultContractを使う
        NextActivityResultContract()
    ) { result ->  // resultはString型
        Toast.makeText(
            this,
            "result=${result}",
            Toast.LENGTH_SHORT
        ).show()
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<Button>(R.id.button)
            .setOnClickListener {
                // Int型のパラメータを渡す
                launcher.launch(android.R.string.copy)
            }
    }
}
```

