Activityで画面遷移を行う際、IntentオブジェクトにputExtra()でパラメータを渡すことができました。Fragmentでは、次の手順でパラメータを渡すことができます。

 - 呼び出される側でnewInstance()メソッドを定義し、setArguments()でパラメータをセットする
 - 次の画面のFragmentオブジェクトをnewInstance()メソッドで作成する
 - 呼び出された側で、getArguments()でセットされたパラメータを取り出す

では、順にみていきましょう。

## 呼び出される側でnewInstance()メソッドを定義し、setArguments()でパラメータをセットする

これはFragmentを使うときのデザインパターンのようなものですが、Fragmentクラスを定義する際、インスタンスを生成するstaticメソッドを定義するようにします。もしパラメータがある場合は、このstaticメソッドの引数で渡せるようにします。

```java
public class NextFragment extends Fragment {
    private static final String ARGS_NAME = "name";

    public static NextFragment newInstance(String name) {
        NextFragment fragment = new NextFragment();
        
        Bundle args = new Bundle();
        args.putString(ARGS_NAME, name);
        fragment.setArguments(args);
        
        return fragment;
    }
}
```

newInstance()メソッドでは、自分自身のインスタンスを作成した後、パラメータの入れ物となるBundleオブジェクトを生成します。このBundleオブジェクトにkey-value形式で値をセットし、setArguments()メソッドでパラメータとして設定します。

newInstance()メソッドを用意しないと、呼び出し側が適切にBundleオブジェクトを生成し、setArguments()を呼ぶという責任を負うことになり、バグの温床となります（セットし忘れなど）。なので、パラメータが無いときも引数なしnewInstance()メソッドを定義し、それ経由でインスタンスを生成するコーディングをおすすめします。

## 次の画面のFragmentオブジェクトをnewInstance()メソッドで作成する

[画面遷移](./transition.html)では直接Fragmentオブジェクトをnewで生成していましたが、これを先ほど定義したnewInstance()メソッドで作成するよう修正します。

```java
@Nullable
@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View root = inflater.inflate(R.layout.fragment_title, container, false);
    View button = root.findViewById(R.id.button_next);
    button.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            FragmentManager manager = getFragmentManager();
            FragmentTransaction transaction = manager.beginTransaction();

            // 普通は引数は画面で入力されたメッセージをいれるのかな？
            transaction.replace(R.id.container, NextFragment.newInstance("myName"));

            transaction.commit();
        }
    });
    return root;
}
```

## 呼び出された側で、getArguments()でセットされたパラメータを取り出す

setArguments()でセットされたBundleオブジェクトはFragment内でgetArguments()メソッドで取り出せます。FragmentのonCreate()メソッド内で取り出すようにするとよいでしょう。

```java
private String mName;

@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Bundle args = getArguments();
    mName = args.getString(ARGS_NAME);
}
```

NextFragmentの全体は次のようになります(onCreateView()は省略)

```java
public class NextFragment extends Fragment {
    private static final String ARGS_NAME = "name";

    public static NextFragment newInstance(String name) {
        NextFragment fragment = new NextFragment();

        Bundle args = new Bundle();
        args.putString(ARGS_NAME, name);
        fragment.setArguments(args);

        return fragment;
    }

    private String mName;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        Bundle args = getArguments();
        mName = args.getString(ARGS_NAME);
    }
}
```

## コラム：引数ありコンストラクタや、setter()ではなぜだめなのか

ここまで読んできて、「こんな面倒なことをせず、引数ありコンストラクタやsetter()を定義したほうが早いのでは？」と思った方もいると思います。なぜ、だめなのでしょうか。

Fragmentインスタンスは、中断などで破棄され、再開時にFragmentManagerによって再度生成されます。このとき、リフレクションで引数なしコンストラクタが呼ばれることになっています。なので、もし引数ありコンストラクタを定義すると、引数なしのデフォルトコンストラクタは無くなってしまうため、再生成時にエラーとなってしまいます。

また、再生成はコンストラクタしか呼ばれないため、setter()でセットしたフィールドの値は初期値に戻ってしまいます。setArguments()で渡されたBundleオブジェクトはFragmentオブジェクト再生成時に復元され、裏でsetArguments()で再度セットされるようになっています。

このような理由から、パラメータを渡す方法として引数ありコンストラクタやsetter()は利用できないのです。

