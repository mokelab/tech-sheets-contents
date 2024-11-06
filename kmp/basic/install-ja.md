Title: Kotlin Multiplatform開発環境の準備

Priority: 10

Kotlin Multiplatformでアプリを作るには、以下の3点を用意します。Androidのみでよい場合、Android Studioにプラグインを追加するだけでも開発できます。
[公式ドキュメント](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-setup.html)

- Android Studio
- XCode(iOS向けのアプリを作りたい場合)
- Fleet(Android Studioでも代用可)

もしmacを使っている場合、 `flutter doctor` コマンドに似た `kdoctor` コマンドが用意されているのでインストールしておくと便利かもしれません。

```
brew install kdoctor
```

`kdoctor` コマンドを実行すると次のように開発環境のインストール状況を教えてくれます。

```
% kdoctor
Environment diagnose (to see all details, use -v option):
[✓] Operation System
[✓] Java
[!] Android Studio
  ! Android Studio (AI-241.18034.62.2412.12266719)
    Location: /Applications/Android Studio.app
    Bundled Java: openjdk 17.0.11 2024-04-16
    Kotlin Plugin: 241.18034.62.2412.12266719-AS
    Kotlin Multiplatform Mobile Plugin: not installed
    Install Kotlin Multiplatform Mobile plugin - https://plugins.jetbrains.com/plugin/14936-kotlin-multiplatform-mobile
[✓] Xcode
[!] CocoaPods
  ! CocoaPods configuration is not required, but highly recommended for full-fledged development
  ✖ CocoaPods requires your terminal to be using UTF-8 encoding.
    Consider adding the following to ~/.zprofile
    export LC_ALL=en_US.UTF-8

Conclusion:
  ✓ Your operation system is ready for Kotlin Multiplatform Mobile Development!
```

Conclusionに `Your operation system is ready for Kotlin Multiplatform Mobile Development!` が表示されれば、開発環境の準備は大丈夫だと思われます。

