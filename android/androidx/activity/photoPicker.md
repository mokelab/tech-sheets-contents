Title: PhotoPickerを使って写真選択機能を作る

Priority: 60

Androidで写真選択機能を作るにはPhotoPickerを使います。追加の権限も不要です。該当の `ActivityResultContracts` は `androidx.activity` に入っています。

```
import androidx.activity.result.PickVisualMediaRequest
import androidx.activity.result.contract.ActivityResultContracts.PickVisualMedia
import coil.compose.AsyncImage

@Composable
fun PhotoPickerScreen() {
    var imageUri by remember { mutableStateOf<Uri?>(null) }
    val launcher = rememberLauncherForActivityResult(
        PickVisualMedia()
    ) { uri ->
        imageUri = uri
    }
    Scaffold { contentPadding ->
        Column(
            modifier = Modifier.padding(contentPadding)
        ) {
            Button(onClick = {
                // PhotoPickerの起動
                launcher.launch(
                    PickVisualMediaRequest(PickVisualMedia.ImageOnly)
                )
            }) {
                Text("Pick photo")
            }
            if (imageUri != null) {
                AsyncImage(model = imageUri, contentDescription = "Image")
            }
        }
    }
}
```

表示には[Coil](https://coil-kt.github.io/coil/README-ja/) を使っています。
