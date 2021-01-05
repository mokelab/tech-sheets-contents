ActivityResultLauncherを使って権限を取得する

`registerForActivityResult()` で作る `ActivityResultLauncher` ですが、これを使ってRuntime permission(実行時の権限)を取得することができます。

```
class MainActivity : AppCompatActivity() {

    private val launcher = registerForActivityResult(
        ActivityResultContracts.RequestPermission()
    ) { granted ->
        if (granted) {
            startCamera()
        } else {
            Toast.makeText(
                    this,
                    "Cannot use Camera",
                    Toast.LENGTH_SHORT
            ).show()
        }
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<Button>(R.id.button)
            .setOnClickListener {
                launcher.launch(Manifest.permission.CAMERA)
            }
    }
    ...
}
```

使用する `ActivityResultContract` は `ActivityResultContracts.RequestPermission()` です。 起動時の引数にはどの権限を取得するかを指定します。ここではカメラの権限を取得しています。

ちなみに、AndroidManifestに `<uses-permission android:name="android.permission.CAMERA"/>` がないとダイアログすら出ないので忘れずにつけておきましょう。

## お作法にしたがって権限を取得する

上記の例はいきなり権限の取得を行っていますが、ユーザーがすでに許可していた場合や拒否していた場合も考慮する必要があります。

```
private fun checkCameraPermission() {
    val permission = Manifest.permission.CAMERA
    when {
        ContextCompat.checkSelfPermission(
                this, permission
        ) == PackageManager.PERMISSION_GRANTED -> {
            startCamera()
        }
        shouldShowRequestPermissionRationale(permission) -> {
            showCannotUseDialog()
        }
        else -> {
            launcher.launch(permission)
        }
    }
}
```
