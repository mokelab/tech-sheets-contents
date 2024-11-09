Title: Setup Kotlin Multiplatform

Priority: 10

To create an app with Kotlin Multiplatform, prepare the followings. 
[Official document](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-setup.html)

- Android Studio
- XCode(for iOS app)
- Fleet(or Android Studio)

If you use macOS、 `kdoctor` command is useful. 

```
brew install kdoctor
```

`kdoctor` command tells you your setup state.

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

You may be ready when `Your operation system is ready for Kotlin Multiplatform Mobile Development!` is displayed.

