Title: MUI の Button Group を縦に表示する

Priority: 20  

Button Groupコンポーネントは、`orientation` プロパティを `vertical` に指定することで、Buttonコンポーネントを縦に並べることができます。  

```tsx
import Button from "@mui/material/Button";
import ButtonGroup from "@mui/material/ButtonGroup";

const buttons = [
  <Button key="one">One</Button>,
  <Button key="two">Two</Button>,
  <Button key="three">Three</Button>,
];

export default function GroupOrientation() {
  return <ButtonGroup orientation="vertical">{buttons}</ButtonGroup>; // `orientation` プロパティを `vertical` に指定する
}
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/86323baa-541b-4c51-a87f-178a4b233ac3)
