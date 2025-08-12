Title: Jetpack ComposeでPDFを表示する

Priority: 10

※本記事はアルファ版ライブラリでの調査結果です

androidx.pdf:pdf-composeとandroidx.pdf:pdf-document-serviceを使ってJetpack ComposeでPDFが表示できます。

## ライブラリの追加

バージョン `1.0.0-alpha10` 以降を指定します。

```
// app/build.gradle.kts
dependencies {
  ...
  implementation("androidx.pdf:pdf-compose:1.0.0-alpha10")
  implementation("androidx.pdf:pdf-document-service:1.0.0-alpha10")  
}
```

## 表示対象PDFのUriを取得する

今回は `rememberLauncherForActivityResult` で取得するようにしてみます。

```
val launcher = rememberLauncherForActivityResult(
  ActivityResultContracts.OpenDocument()
) { uri ->
  if (uri == null) return@rememberLauncherForActivityResult
  // 続きは後ほど
}
```

## PDFをロードする


Uriが取得できたら次はロードします。 `suspend fun` なのでコルーチンスコープの中で実行します。

```
val context = LocalContext.current
val scope = rememberCoroutineScope()
var pdf by remember { mutableStateOf<PdfDocument?>(null) }

val launcher = rememberLauncherForActivityResult(
  ActivityResultContracts.OpenDocument()
) { uri ->
  if (uri == null) return@rememberLauncherForActivityResult

  val loader = SandboxedPdfLoader(context = context)
  // Load the PDF document from the URI
  scope.launch {
    pdf = loader.openDocument(uri = uri, password = null)
  }
}
```

## ロードしたPDFを表示する

表示には `PdfViewer()` コンポーザブルを使います。

```
if (pdf != null) {
    PdfViewer(
        pdfDocument = pdf,
        state = state,
    )
}
```


