Title: MUI の Card コンポーネント の大きさを変更する

Priority: 20  

Card コンポーネントは、主に以下の方法でサイズを変更できます。  

1. sxプロパティを使用する
2. インラインスタイルを使用する

## sxプロパティを使用する  

MUI v5以降では、sxプロパティを使用してスタイルを直接指定することができます。  

```tsx
import { Card, CardContent, CardHeader, Typography } from "@mui/material";

function SxStyledCard() {
  return (
    <Card sx={{ width: 300, height: 400 }}>
      <CardHeader title="タイトル"></CardHeader>
      <CardContent>
        <Typography variant="body2" color="text.secondary">
          ここに内容が入ります。
        </Typography>
      </CardContent>
    </Card>
  );
}

export default SxStyledCard;
```
![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/f73f497e-41b4-4ae9-9477-1cd0eb68a8c2)


## インラインスタイルを使用する  

Reactの標準的なインラインスタイルを使用して、スタイルを指定することも可能です。  

```tsx
import { Card, CardContent, CardHeader, Typography } from "@mui/material";

function InlineStyledCard() {
  return (
    <Card style={{ width: 300, height: 200 }}>
      <CardHeader title="タイトル"></CardHeader>
      <CardContent>
        <Typography variant="body2" color="text.secondary">
          ここに内容が入ります。
        </Typography>
      </CardContent>
    </Card>
  );
}

export default InlineStyledCard;
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/4d76ba54-673e-4dbf-abc6-cbe5febc96ad)
