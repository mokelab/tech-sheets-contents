Title: MUI の TextField コンポーネント

Priority: 10

MUI の TextField コンポーネントは、テキスト入力フィールドを簡単に作成するためのコンポーネントです。  

公式ドキュメント:[Text Field](https://mui.com/material-ui/react-text-field/)  

# 基本的な使い方  

```tsx
import TextField from "@mui/material/TextField"; // `@mui/material` からインポートします

const BasicTextField: React.FC = () => {
  return <TextField label="名前" variant="outlined" />; // タグを記述して使用します。
};

export default BasicTextField;
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/3c9ca83f-a6db-46ce-a739-8c0e3f582f39)  

上記の例では、`label`プロパティを使用してフィールドのラベルを「名前」に設定し、`variant`プロパティでフィールドのスタイルを`outlined`に設定しています。



