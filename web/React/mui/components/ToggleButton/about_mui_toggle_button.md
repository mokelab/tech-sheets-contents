Title: MUI の Toggle Button コンポーネント

Priority: 10

`Toggle Button` コンポーネントは、複数の選択肢の中から一つまたは複数を選択できるボタンです。  
これらのボタンは、クリックすることで選択状態がトグル（切り替え）される仕組みになっています。  
選択状態が変わると、ボタンの見た目や動作が変化するため、現在の選択状態が視覚的に分かりやすくなります。  

公式ドキュメント： [Toggle Button](https://mui.com/material-ui/react-toggle-button/)

# 基本的な使い方

```tsx
import React, { useState } from "react";
import ToggleButton from "@mui/material/ToggleButton";
import ToggleButtonGroup from "@mui/material/ToggleButtonGroup";

const ToggleButtonSumple: React.FC = () => {
  const [selected, setSelected] = useState<string | null>(null);

  const handleToggle = (
    event: React.MouseEvent<HTMLElement>,
    newSelection: string | null
  ) => {
    setSelected(newSelection);
  };

  return (
    <ToggleButtonGroup // ①
      value={selected}
      exclusive
      onChange={handleToggle}
      aria-label="custom styled toggle buttons"
    >
      <ToggleButton value="option1" aria-label="option 1"> // ②
        Option 1
      </ToggleButton>
      <ToggleButton value="option2" aria-label="option 2">
        Option 2
      </ToggleButton>
      <ToggleButton value="option3" aria-label="option 3">
        Option 3
      </ToggleButton>
    </ToggleButtonGroup>
  );
};

```

## ① ToggleButtonGroup

複数の `ToggleButton` をグループ化するために使用されます。

- `value`：現在選択されている値を設定します
- `exclusive`：`exclusive`プロパティを設定すると、単一選択モードになります（複数選択モードにする場合は省略します）
- `onChange`：選択が変更されたときに呼び出される関数を設定します
- `aria-label`：アクセシビリティのためのラベルを設定します

## ② ToggleButton

- `value`：各ボタンの識別子として機能します
- `aria-label`：アクセシビリティのためのラベルを設定します

![image](https://github.com/user-attachments/assets/d68c0690-da84-4bc1-b0f0-ab8e8605e319)  

![image](https://github.com/user-attachments/assets/d1d9801c-dbe2-47ed-9a99-1e372f56ae31)



