Title: MUI の Button Group コンポーネント

Priority: 10

MUI　の Button Groupコンポーネントは、複数のボタンを一つのグループとしてまとめることができます。見た目を統一するのに役立ちます。  

公式ドキュメント：[Button Group](https://mui.com/material-ui/react-button-group/)

# 基本的な使い方

```tsx
import Button from '@mui/material/Button';
import ButtonGroup from '@mui/material/ButtonGroup'; // `@mui/material` からインポートします

export default function BasicButtonGroup() {
  return (
    <ButtonGroup> // タグを記述して使用します。
      <Button>One</Button> // タグ内に、配置したい<Button>コンポーネントを記述します。
      <Button>Two</Button>
      <Button>Three</Button>
    </ButtonGroup>
  );
}
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/3759b40b-50dc-4c85-9c0e-4667976972fb)
