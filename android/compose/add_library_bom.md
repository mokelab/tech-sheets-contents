Title: Jetpack Composeのライブラリ(BOM)を追加する

Priority: 10

Jetpack Composeは日々開発がすすんでいるため、適当にライブラリのバージョンを指定していくと動作しないことがあります。

動作確認がとれている組み合わせはBOM(Bill of Materials)として用意されています。公式ドキュメントは[こちら](https://developer.android.com/jetpack/compose/bom/bom)

やることは以下の2つです。

- BOMを追加する
- 各ライブラリからバージョン部分を抜く

## BOMを追加する

`androidx.compose:compose-bom` を追加します。

```
// build.gradle.kts
val composeBom = platform("androidx.compose:compose-bom:2023.01.00")
implementation(composeBom)
testImplementation(composeBom)
androidTestImplementation(composeBom)
```

## 各ライブラリからバージョン部分を抜く

どのバージョンを使うかはBOMにかかれているので、各ライブラリからバージョン部分を抜きます。

```
// build.gradle.kts
implementation("androidx.compose.ui:ui")
implementation("androidx.compose.ui:ui-tooling-preview")
implementation("androidx.compose.material3:material3")

androidTestImplementation("androidx.compose.ui:ui-test-junit4")
debugImplementation("androidx.compose.ui:ui-tooling")
debugImplementation("androidx.compose.ui:ui-test-manifest")
```

最終的にbuild.gradle.ktsのdependencies部分は次のようになります。

```
dependencies {
  // BOMを追加する
  // testImplementation とかにも追加するのを忘れないよう
  val composeBom = platform("androidx.compose:compose-bom:2023.01.00")
  implementation(composeBom)
  testImplementation(composeBom)
  androidTestImplementation(composeBom)

  // バージョン部分は抜く
  implementation("androidx.compose.ui:ui")
  implementation("androidx.compose.ui:ui-tooling-preview")
  implementation("androidx.compose.material3:material3")

  androidTestImplementation("androidx.compose.ui:ui-test-junit4")
  debugImplementation("androidx.compose.ui:ui-tooling")
  debugImplementation("androidx.compose.ui:ui-test-manifest")
}
```
