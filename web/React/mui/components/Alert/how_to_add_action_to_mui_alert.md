Title: MUI の MUI の Alert コンポーネントにアクションを追加する

Priority: 50

`MUI` の `Alert` コンポーネントのには `action` プロパティがあり、ここにアクションを追加することができます。  
このアクションには、ボタンなどの他のインタラクティブな要素を含めることができます。  

# 基本的な使い方

```tsx
import { useState } from "react";
import Alert from "@mui/material/Alert";
import IconButton from "@mui/material/IconButton";
import CloseIcon from "@mui/icons-material/Close";
import Box from "@mui/material/Box";

export default function ActionAlerts() {
  const [open, setOpen] = useState(true); // 各アラートの表示状態を管理します。

  return (
    <Box>
      {open && (
        <Alert
          action={ 
            <IconButton 
              size="small"
              onClick={() => {
                setOpen(false);
              }}
            >
              <CloseIcon fontSize="inherit" /> // 閉じるボタンを追加
            </IconButton>
          }
          onClose={() => { // 閉じるアクションを設定
            setOpen(false);
          }}
        >
          This Alert displays the default close icon.
        </Alert>
      )}
    </Box>
  );
}
```

▼ × ボタンをクリックすると `Alert` がクローズされます
![Alert_action_参考画像](https://github.com/user-attachments/assets/c16859a2-2818-40c7-b7b8-5dab2958b7b7)
