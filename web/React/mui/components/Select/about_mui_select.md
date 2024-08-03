Title: MUI の Select コンポーネント

Priority: 10

MUI の `Select` コンポーネントは、ユーザーがドロップダウンリストからオプションを選択できるUIコンポーネントです。  

公式ドキュメント：[Select](https://mui.com/material-ui/react-select/)  

# 基本的な使い方

```tsx
import * as React from "react";
import MenuItem from "@mui/material/MenuItem";
import Select, { SelectChangeEvent } from "@mui/material/Select"; // 必要なコンポーネントをインポートします

export default function BasicSelect() {
  const [character, setCharacter] = React.useState(""); // Reactのフックを使用して、ステート変数`character`を初期化します

  const handleChange = (event: SelectChangeEvent) => { //  セレクトボックスの値が変更されたときに呼び出されるイベントハンドラー関数です
    setCharacter(event.target.value as string);
  };

  return (
    <Select // セレクトボックスそのものを表します
      labelId="demo-simple-select-label"
      id="demo-simple-select"
      value={character}
      label="Character"
      onChange={handleChange}
    >
      <MenuItem value={10}>moke</MenuItem> // セレクトボックス内の個々の選択肢を表します
      <MenuItem value={20}>piyo</MenuItem>
      <MenuItem value={30}>maro</MenuItem>
    </Select>
  );
}
```

![image](https://github.com/user-attachments/assets/a2058aec-b2dd-41d6-bffc-daae140e137e)
