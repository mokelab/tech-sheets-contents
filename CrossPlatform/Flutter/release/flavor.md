Title: FlutterでProduct Flavorを使う

Priority: 100

Androidアプリではビルド時に設定などを変更できるProduct Flavorという仕組みがあります。この仕組みはFlutterでも用意されています。

公式ドキュメントは[こちら](https://docs.flutter.dev/deployment/flavors)

## Androidの設定

Android側はネイティブアプリと同様にProduct Flavorを作るだけです。 `android/app/build.gradle` にProduct Flavorを追加します。

```
android {
  ...
  flavorDimensions "default"

  productFlavors {
    stg {
      dimension "default"
      applicationIdSuffix ".stg"
    }
    production {
      dimension "default"
    }
  }
}
```

## iOSの設定

iOS側はconfigurationとschemeの追加で実現します。

まず、 `ios/Runner.xcworkspace` をXCodeで開きます。

Runner -> ProjectのRunner -> infoのConfigurationsで、Debug/Release/ProfileのConfigurationをそれぞれDuplicateで作ります。
名称は `Debug-stg` や `Debug-production` のように `-flavor名` にしておきます。

次にSchemeを追加します。XCode上部の Runner > デバイス名　の部分のRunnerをクリック -> Edit Scheme -> Duplicate Scheme で複製します。
名前は `stg` や　`production` のようにflavor名にします。Flutterがこのflavor名を使ってSchemeを決定するので `Runner-stg` みたいにすると動きません。

Schemeを複製したら、左側にあるBuild/Run/Test/Profile/Analyze/Archiveで使用するBuild ConfigurationをFlavor用に複製したConfigurationに変更します。

これでFlavorができました。あとはAndroidのFlavorと同様にstgビルドの時は別のBundle IdentifierとなるようConfigurationを設定します。

Runner -> TargetsのRunner -> Build Settings -> Product Bundle Identifier で、 `Debug-stg/Profile-stg/Release-stg` の時は別のBundle Identifierを
設定します。

## Flavorを使ったビルド

最後にFlavorを使ったビルドです。 `--flavor flavor名` を追加するだけです。

```
# stgビルドで実行
% flutter run --flavor stg

# productionビルドでapp bundleを作る
% flutter build appbundle --flavor production
```

