Title: ListItemを使って1行分のレイアウトを作る

Priority: 20

リストの1行分のレイアウトですが、マテリアルデザインの仕様にあっているものでよい場合は `ListItem` を使うと便利です。

## テキストのみ

View Systemでは `android.R.layout.simple_list_item_1` を使っていたケースでしょうか。

```
import androidx.compose.material3.ListItem

val names = (1..100).map { "モケラ $it 号" }

@Composable
fun MainScreen() {
  LazyColumn {
    items(names) { name ->
      ListItem(
        headlineContent = {
          Text(name)
        },
      )
    }
  }
}
```

表示は次のようになります。

![テキストのみ](./listItem1.png)
