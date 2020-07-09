Activityであれば、Intentオブジェクトを作り、startActivity()で画面遷移できました。Fragmentでは、最初の貼り付けと同様にFragmentManagerとFragmentTransactionを用います。

FragmentのレイアウトXMLは次のようなものとします。ボタンが1つ。

```xml
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    >
    <Button
        android:id="@+id/button_next"
        android:text="@string/next_page"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</RelativeLayout>
```

このボタンをタップすると、NextFragmentに遷移するには次のように記述します。

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

            transaction.replace(R.id.container, new NextFragment());

            transaction.commit();
        }
    });
    return root;
}
```

FragmentクラスにはgetFragmentManager()メソッドがあるので、これでFragmentManagerオブジェクトを取得します。後はActivityのonCreate()メソッドで貼り付けたのと同様です。画面遷移の場合は、すでに張り付けられているFragmentを置き換えすることになるので、replace()メソッドを使用します。間違えてadd()を呼ぶと、今表示中の画面と次の画面が重なって表示されてしまいます。


