Title: MUI の Alert コンポーネントのバリエーション  
  
Priority: 40  

`MUI` の `Alert` コンポーネントは、異なる状況やコンテンツに応じてさまざまなスタイルとバリエーションを持っています。  

# 基本的な使い方  

```tsx
import Alert from "@mui/material/Alert";
import Stack from "@mui/material/Stack";

export default function VariantsAlerts() {
  return (
    <Stack sx={{ width: "100%" }} spacing={2}>
      <Alert variant="filled" severity="success">
        This is a filled success Alert.
      </Alert>
      <Alert variant="filled" severity="info">
        This is a filled info Alert.
      </Alert>
      <Alert variant="filled" severity="warning">
        This is a filled warning Alert.
      </Alert>
      <Alert variant="filled" severity="error">
        This is a filled error Alert.
      </Alert>
    </Stack>
  );
}
```

![image](https://github.com/user-attachments/assets/21ade508-a111-48e9-a42b-890fa223d901)

