Title: MUI の Rating コンポーネント

Priority: 10

Rating コンポーネントは、ユーザーが星の数で評価を入力できる UI コンポーネントです。  

公式ドキュメント：[Rating](https://mui.com/material-ui/react-rating/)

# Rating コンポーネントの使い方

```tsx
// 必要なコンポーネントをインポートします
import * as React from "react";
import Box from "@mui/material/Box";
import Rating from "@mui/material/Rating";
import Typography from "@mui/material/Typography";

export default function BasicRating() {
  const [value, setValue] = React.useState<number | null>(2); // useState フックを使って value を管理します。この値は Rating コンポーネントで選択された評価値を保持します

  return (
    <Box
      sx={{
        "& > legend": { mt: 2 },
      }}
    >
      <Typography component="legend">Controlled</Typography>
      <Rating // タグを記述して使用します
        name="simple-controlled" // Rating コンポーネントの名前を設定します
        value={value} // 現在の評価値を指定します
        onChange={(event, newValue) => { // ユーザーが評価を変更したときに呼び出され、新しい評価値を状態に設定します
          setValue(newValue);
        }}
      />
      <Typography component="legend">Read only</Typography>
      <Rating name="read-only" value={value} readOnly /> // 評価を表示するだけで変更できない状態にします

      <Typography component="legend">Disabled</Typography>
      <Rating name="disabled" value={value} disabled /> // 評価コンポーネントを無効にします

      <Typography component="legend">No rating given</Typography>
      <Rating name="no-value" value={null} /> // 未評価の状態を表します
    </Box>
  );
}
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/d15980e9-cd4a-47ad-b197-026b3581680f)
