Activityでは、`startActivityForResult()`で次のActivityを呼び出すと、後で結果を取得することができました。Fragmentでは次のように実装することで、呼び出し元に結果を伝えることができます。

 - 呼び出されるFragmentオブジェクトのsetTargetFragment()で、呼び出し元のFragmentオブジェクトをセットする
 - 呼び出された側で結果を伝える場面で、getTargetFragment()で、呼び出し元のFragmentオブジェクトを取得する
 - Intentに結果を詰め、呼び出し元のFragmentオブジェクトのonActivityResult()を呼ぶ
 - 呼び出し元で`onActivityResult()`を実装し、結果を受け取ったときの処理を記述する

やや長いですが、順にみていきましょう。

## 呼び出されるFragmentオブジェクトのsetTargetFragment()で、呼び出し元のFragmentオブジェクトをセットする

setTargetFragment()メソッドで、呼び出し元のFragmentオブジェクトとリクエストコードをセットできます。リクエストコードは結果を伝えるときに使用します。

Fragmentオブジェクトを作る際にまとめてセットできるよう、newInstance()メソッドで次のように実装するとよいでしょう。

```
public static NextFragment newInstance(Fragment target, int requestCode) {
    NextFragment fragment = new NextFragment();
    fragment.setTargetFragment(target, requestCode);
    
    Bundle args = new Bundle();
    fragment.setArguments(args);
    
    return fragment;
}
```

## 呼び出された側で結果を伝える場面で、getTargetFragment()で、呼び出し元のFragmentオブジェクトを取得する

setTargetFragment()でセットされた呼び出し元のFragmentオブジェクトはgetTargetFragment()で取得できます。リクエストコードはgetTargetRequestCode()で取得できます。

## Intentに結果を詰め、呼び出し元のFragmentオブジェクトのonActivityResult()を呼ぶ

入力内容などの結果はIntentオブジェクトを生成し、それに詰めます。単純に成功/キャンセルだけであればonActivityResult()の第2引数だけで表現できます。

例えば、保存ボタンを押すとEditTextの内容を結果として伝えるには次のようなコードになります。

```
// 引数は入力された文字列とします
void submit(String inputText) {
    Fragment target = getTargetFragment();
    if (target == null) { return; }
    
    Intent data = new Intent();
    data.putExtra(Intent.EXTRA_TEXT, inputText);
    target.onActivityResult(getTargetRequestCode(), Activity.RESULT_OK, data);
}
```

## 呼び出し元ではonActivityResult()を実装し、結果を受け取ったときの処理を記述する

呼び出し側のFragmentでonActivityResult()が呼ばれるので、呼び出し側でこのメソッドを実装します。

```
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    switch (requestCode) {
    case REQUEST_INPUT_NAME:
        if (resultCode != Activity.RESULT_OK) { return; }
        
        String name = data.getStringExtra(Intent.EXTRA_TEXT);
        Log.v("FirstFragment", "入力された名前は" + name);
        return;
    }
    super.onActivityResult(requestCode, resultCode, data);
}
```

DialogFragmentはFragmentを継承しているので、この一連の手続きはDialogFragmentでも同様に使えます。これにより、ダイアログと呼び出し元の結合度が下がり、再利用性が高まります。

## onActivityResult()を呼ぶのは邪道では？

Fragmentからの結果なのに`onActivityResult()`を呼ぶのは邪道なのでは？と感じる方もいるでしょう。実は`setTargetFragment`のJavadocに答えが書いてあります(v25で確認)。

```
/**
 * Optional target for this fragment.  This may be used, for example,
 * if this fragment is being started by another, and when done wants to
 * give a result back to the first.  The target set here is retained
 * across instances via {@link FragmentManager#putFragment
 * FragmentManager.putFragment()}.
 *
 * @param fragment The fragment that is the target of this one.
 * @param requestCode Optional request code, for convenience if you
 * are going to call back with {@link #onActivityResult(int, int, Intent)}.
 */
public void setTargetFragment(Fragment fragment, int requestCode) {
    mTarget = fragment;
    mTargetRequestCode = requestCode;
}
```

「onActivityResultでコールバックするなら、requestCodeを使うと便利だよ」と書いてあります。

