※本記事はAndroid JetpackのNavigationが無い時代に書かれたものです。Navigationを使う場合、Fragmentの貼り付け方などが異なるため、別の記事を参照してください（記事を書いたらここにリンク貼ります。。。）

----

まずは1画面のアプリでFragmentを使ってみましょう。次の手順でFragmentを貼り付けてみます。

 - Fragment用のレイアウトXMLを作る
 - Fragmentを継承したクラスを作る
 - Activity用のレイアウトXMLをFrameLayoutのみにする
 - ActivityのonCreate()で、指定した位置にFragmentを貼り付ける

では、順にみていきましょう。

## Fragment用のレイアウトXMLを作る

Fragment用のレイアウトXMLを用意します。ファイル名をfragment_xxxx.xmlのようにしておくと「あ、これはFragment用のレイアウトか」と認識できて便利ですね。

```
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    >
    <TextView
        android:text="@string/hello_world"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</RelativeLayout>
```

## Fragmentを継承したクラスを作る

次に、Activityのときと同様にFragmentを継承したクラスを作ります。このとき、最低限必要なメソッドはonCreateView()メソッドです。

onCreateView()メソッドは引数としてLayoutInflaterとViewGroupが渡されます(SavedInstanceStateも渡されますが、ここでは省略)。この2つを用いて次のようにViewを生成し、returnします。inflate()メソッドの引数でこれ以外を指定する（例えば第3引数にtrueを渡すなど）と実行時にエラーとなるので注意しましょう。

```
public class FirstFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_title, container, false);
    }
}
```

## Activity用のレイアウトXMLをFrameLayoutのみにする

Activity用のレイアウトは、Fragmentを貼り付けるための箱だけにします。idをつけるのを忘れないように。

```
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/container">
</FrameLayout>
```

## ActivityのonCreate()で、指定した位置にFragmentを貼り付ける

ActivityのonCreate()で、setContentView()でActivity用のレイアウトXMLを適用した後、先ほど定義したFragmentを指定した位置に貼り付ける処理を記述します。

```
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        if (savedInstanceState == null) {
            FragmentManager manager = getSupportFragmentManager();
            FragmentTransaction transaction = manager.beginTransaction();

            transaction.add(R.id.container, new FirstFragment());

            transaction.commit();
        }
    }
}
```

savedInstanceStateがnullのときのみ、貼り付け処理を行っているのは、Activity再生成時に再度貼り付け処理が行われるのを防ぐためです。super.onCreate(savedInstanceState)内で貼り付けられたFragmentの状態などが復元されます。

Fragmentの貼り付けはFragmentManagerオブジェクト経由で行います。support-v4(AppCompatActivity)を使用する場合はgetSupportFragmentManager()で取得します。

実際の貼り付け処理はFragmentTransactionを用いて行います。Activityに貼り付けたレイアウトの指定したidにFragmentを追加する場合は、add()メソッドを使用します。第1引数は貼り付ける位置です。複数のFragmentを一度に貼り付ける場合は、add()メソッドを複数回呼びます。

add()を呼び終えたら、FragmentTransactionオブジェクトのcommit()を呼びます。これで、画面全体にFragmentを貼ることができました。

※見た目はActivityにレイアウトを直接指定したときと同じなのでスクリーンショット省略

