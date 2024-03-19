Title: Jetpack Composeでランタイムパーミッションを取得する

Priority: 40

Jetpack Composeでランタイムパーミッションを取得するには `rememberLauncherForActivityResult` と `ActivityResultContracts.RequestPermission()` をセットで使います。

```
@Composable
fun PermissionScreen() {
  val request = rememberLauncherForActivityResult(
    ActivityResultContracts.RequestPermission()
  ) { isGranted ->
    if (isGranted) {
      // 権限もらえた！
    } else {
      // だめだった！
    }
  }
  Scaffold { contentPadding ->
    Column(
      modifier = Modifier.padding(contentPadding),
    ) {
      Button(onClick = {
        // ダイアログ表示
        request.launch(android.Manifest.permission.POST_NOTIFICATIONS)
      }) {
        Text("権限をもらう")
      }
    }
  }
}
```
