Activityでダイアログを出そうとすると、実は大変でした。

 - ActivityのshowDialog()を呼ぶ
 - すると、onCreateDialog()が呼ばれるので、そこでダイアログを生成する
 - ダイアログはキャッシュされるので、一工夫必要

Fragmentを使ったアプリ開発では、ダイアログは画面遷移のように扱えるようになりました。次の手順で呼び出します。

 - DialogFragmentを継承したクラスを作る
 - onCreateDialog()を実装する
 - 呼び出し側でDialogFragmentオブジェクトを作り、show()を呼ぶ

では、順にみていきましょう

## DialogFragmentを継承したクラスを作る

まずはFragmentと同様に、DialogFragmentを継承したクラスを作ります。ここでは単純にメッセージを表示するだけのMessageDialogFragmentを作ってみます。

```java
public class MessageDialogFragment extends DialogFragment {
    public static MessageDialogFragment newInstance() {
        MessageDialogFragment fragment = new MessageDialogFragment();

        Bundle args = new Bundle();
        fragment.setArguments(args);

        return fragment;
    }
}
```

## onCreateDialog()を実装する

DialogFragmentでは、onCreateDialog()を実装します。このメソッドでは、Dialogオブジェクトを生成しreturnします。AlertDialog.Builderを使ってメッセージを出すだけのDialogを生成してみます。

```java
@NonNull
@Override
public Dialog onCreateDialog(Bundle savedInstanceState) {
    Activity activity = getActivity();
    if (activity == null) {
        return super.onCreateDialog(savedInstanceState);
    }

    AlertDialog.Builder builder = new AlertDialog.Builder(activity);
    builder.setMessage("やほー");
    builder.setPositiveButton(android.R.string.ok, null);
    return builder.create();
}
```

MessageDialogFragment全体は次のようになります。

```java
public class MessageDialogFragment extends DialogFragment {
    public static MessageDialogFragment newInstance() {
        MessageDialogFragment fragment = new MessageDialogFragment();

        Bundle args = new Bundle();
        fragment.setArguments(args);

        return fragment;
    }
    @NonNull
    @Override
    public Dialog onCreateDialog(Bundle savedInstanceState) {
        Activity activity = getActivity();
        if (activity == null) {
            return super.onCreateDialog(savedInstanceState);
        }

        AlertDialog.Builder builder = new AlertDialog.Builder(activity);
        builder.setMessage("やほー");
        builder.setPositiveButton(android.R.string.ok, null);
        return builder.create();
    }
}
```

## 呼び出し側でDialogFragmentオブジェクトを作り、show()を呼ぶ

ダイアログの表示はDialogFragmentオブジェクトのshow()で行います。

```java
@Nullable
@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View root = inflater.inflate(R.layout.fragment_title, container, false);
    View button = root.findViewById(R.id.button_next);
    button.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            MessageDialogFragment dialog = MessageDialogFragment.newInstance();
            dialog.show(getFragmentManager(), "");
        }
    });
    return root;
}
```

実際にボタンをタップすると、次のようにダイアログが表示されます。

![実行結果](./dialog.webp width=463 height=824)

