Title: MUI の Alert コンポーネントの重要度  

Priority: 20  


MUI の `Alert` コンポーネントは、 `severity` プロパティで重要度を設定することができます。 　
成功（デフォルト）、情報、警告、エラーという4つの値があり、それぞれに対応したアイコンと色の組み合わせがあります。  

```tsx
import Alert from "@mui/material/Alert";
import Stack from "@mui/material/Stack";

export default function TestSeverityAlert() {
  return (
    <Stack sx={{ width: "100%" }} spacing={2}>
      <Alert severity="success">This is a success Alert.</Alert>
      <Alert severity="info">This is an info Alert.</Alert>
      <Alert severity="warning">This is a warning Alert.</Alert>
      <Alert severity="error">This is an error Alert.</Alert>
    </Stack>
  );
}
```

![image](https://github.com/user-attachments/assets/913686b0-29da-40be-afa5-f21abe18e448)  
