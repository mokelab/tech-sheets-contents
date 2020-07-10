[先ほど](./create_viewmodel.html)作成したViewModelオブジェクトを取得するには、次のように `by viewModels()` を使います。 

```
class MainFragment : Fragment() {
    private val model: MainViewModel by viewModels()
}

```

_`viewModels()` 拡張関数はJava 8の機能を使用しているので、`build.gradle`のandroidブロックに次の記述を追加します。

```
android {
    .. 
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    kotlinOptions {
        jvmTarget = '1.8'
    }
}
```

