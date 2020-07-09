Activityによる遷移では、端末の戻るボタンで１つ前の画面に戻ることができました。Fragmentでは、BackStackという仕組みを利用して、端末の戻るボタンで1つ前の画面に戻れるようにできます。

やり方は簡単です。Fragmentのreplace時、FragmentTransactionオブジェクトのaddToBackStack()メソッドを呼ぶだけです。このメソッドは、今のFragmentの状況（どのidにどのFragmentが貼り付けられているか）をBackStackと呼ばれるスタックに積みます。このBackStackに状態が積まれているとき、端末の戻るボタンを押すと、1つ前の状態、つまり１つ前の画面に戻れる　という仕組みです。

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
            transaction.addToBackStack("");
            transaction.replace(R.id.container, NextFragment.newInstance("myName"));

            transaction.commit();
        }
    });
    return root;
}
```

