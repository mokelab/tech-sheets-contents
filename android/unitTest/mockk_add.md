Title: MockKを追加する

Priority: 100

MockKはKotlinでモックオブジェクトを作ってくれるライブラリです。Unit Testを書くときにとても役立ちます ([公式ドキュメント](https://mockk.io/))。

MockKをAndroidのUnit Test用に追加するには、 `app/build.gradle.kts` の `dependencies` に追加します。

```
dependencies {
  ...
  testImplementation(libs.mockk)
}
```

```
// libs.versions.toml
[versions]
mockk = "1.13.1"

[libraries]
mockk = { group = "io.mockk", name = "mockk", version.ref = "mockk" }
```

