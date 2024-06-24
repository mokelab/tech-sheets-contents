Title: MUI の Button コンポーネント

Priority: 10

MUI の Button コンポーネントは、アプリケーション内でアクションをトリガーするための基本的かつ重要な要素です。  
多機能でカスタマイズ可能であり、異なる状況やスタイルに適したボタンを簡単に作成できます。  

公式ドキュメント：[Button](https://mui.com/material-ui/react-button/)  

# 基本的な使い方  

`Button` コンポーネントは、`@mui/material` からインポートして使用します。  

```tsx
import Button from "@mui/material/Button"; // `@mui/material` からインポートします

export function ButtonComponent() {
  return (
    <Button variant="contained" color="primary"> // タグを記述して使用します。
      MUIのボタン
    </Button>
  );
}
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/450b1a41-bdcc-494d-935f-106661804cbb)
