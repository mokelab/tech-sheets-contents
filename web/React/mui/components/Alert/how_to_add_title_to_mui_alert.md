Title: MUI の Alert コンポーネントにタイトルを追加する 
  
Priority: 60  

`MUI` の `Alert` コンポーネントにタイトルを追加するには、`AlertTitle` コンポーネントを使用します。  
`AlertTitle` は `Alert` 内に配置して、見出しとしてのタイトルを表示するために使用されます。  

# 実装方法

```tsx
import Alert from "@mui/material/Alert";
import AlertTitle from "@mui/material/AlertTitle";

export default function AlertTitleSample() {
  return (
    <Alert severity="success">
      <AlertTitle>Success</AlertTitle>
      This is a success Alert with an encouraging title.
    </Alert>
  );
}
```

![MUI_Alert_title実装例](https://github.com/user-attachments/assets/1e956eef-079d-4f6b-89d4-dd3392818e65)

## `AlertTitle` を 左よせにする方法

上記の例で、`AlertTitle`を左寄せで表示したい場合、`sx={{ textAlign: "left" }}` を設定します。  


```tsx
import Alert from "@mui/material/Alert";
import AlertTitle from "@mui/material/AlertTitle";

export default function AlertTitleSample() {
  return (
    <Alert severity="success">
      <AlertTitle sx={{ textAlign: "left" }}>Success</AlertTitle>
      This is a success Alert with an encouraging title.
    </Alert>
  );
}
```

![MUI_Alert_title実装例_左よせ](https://github.com/user-attachments/assets/25a6ae67-f5ee-4a00-8776-d16e977e446e)
