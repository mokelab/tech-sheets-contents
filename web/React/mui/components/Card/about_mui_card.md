Title: MUI の Card コンポーネント

Priority: 10  

MUI の Card は、コンテンツを視覚的に分離するためのコンポーネントです。  
メディア、テキスト、アクションボタンなどを含むことができます。  

主に以下のような用途に使用されます。  

- コンテンツのグループ化
- ユーザーに情報をわかりやすく伝えるためのレイアウト
- ダッシュボードやプロファイルページなどの情報のまとめ

公式ドキュメント：[Card](https://mui.com/material-ui/react-card/)  

## 基本的な使い方

```tsx
import {
  Card,
  CardContent,
  CardActions,
  Typography,
  Button,
  CardHeader,
} from "@mui/material"; // 必要なコンポーネントをインポートします

function SimpleCard() {
  return (
    <Card> // タグを記述して使用します
      <CardHeader title="タイトル" />  // カードのタイトルやサブタイトルを表示するサブコンポーネント
      <CardContent>  // カードの主要なコンテンツを表示するサブコンポーネント
        <Typography variant="body2" color="text.secondary">
          ここに内容が入ります。
        </Typography>
      </CardContent>
      <CardActions>  // カードのアクション（Buttonなど）を配置するサブコンポーネント
        <Button size="small">button</Button>
      </CardActions>
    </Card>
  );
}

export default SimpleCard;
```

## 主なサブコンポーネント  

Card コンポーネントには、いくつかのサブコンポーネントがあり、それぞれ特定の役割を果たします。

- `CardHeader`：カードのタイトルやサブタイトルを表示するために使用されます。`<CardHeader title="タイトル" /> `のように記述します。
- `CardContent`：カードの主要なコンテンツを表示するために使用されます。
- `CardActions`：カードのアクション（Buttonなど）を配置するために使用されます。
- `CardMedia`：画像やビデオなどのメディアを表示するために使用されます。

