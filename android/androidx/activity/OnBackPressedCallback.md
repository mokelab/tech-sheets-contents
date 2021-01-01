OnBackPressedCallbackを使って戻るボタン時の処理を書く

端末の戻るボタン(バックボタン)が押された時になんらかの処理をさせたい場合、androidx.activityで提供されている `OnBackPressedDispatcher` と `OnBackPressedCallback` を使います。

```
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // addCallbackはktxで提供されている拡張関数
        onBackPressedDispatcher.addCallback {
            Toast.makeText(
                    this@MainActivity,
                    "Back pressed",
                    Toast.LENGTH_SHORT
            ).show()
            finish() // 自前で終了させる必要あり
        }
    }
}
```

`addCallback` で戻るボタンが押された時のコールバックを登録した場合、 `finish()` でアクティビティを終了させる処理があります。これを忘れると終了できないアプリが出来上がるので注意しましょう。

なお、フラグメントで使いたい場合は次のように親となるアクティビティをとってきてからコールバックをセットします。この時、LifecycleOwnerとして自分自身をセットしておきます。

```
class MainFragment: Fragment() {
    override fun onAttach(context: Context) {
        super.onAttach(context)
        requireActivity().onBackPressedDispatcher
            .addCallback(this) {
                Toast.makeText(
                    context,
                    "Back pressed",
                    Toast.LENGTH_SHORT
                ).show()
                // pop backstack
        }
    }
}
```

