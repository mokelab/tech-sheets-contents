Title: MUI の Alert コンポーネントの色を変更する

Priority: 70  

`MUI` の `Alert` コンポーネントでは、`sx` プロップを使うと色を変更することができます。  

```tsx
import Alert from "@mui/material/Alert";

function ColorAlert() {
  return (
    <Alert
      severity="info"
      sx={{ backgroundColor: "lightblue", color: "darkblue" }}
    >
      This is a custom alert!
    </Alert>
  );
}

export default ColorAlert;
```

![MUI_Alert_色を変更する](https://github.com/user-attachments/assets/028ebdbf-33b6-408a-93ce-28091fb929d0)
