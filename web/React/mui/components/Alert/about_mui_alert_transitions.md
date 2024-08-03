Title: MUI の Alert コンポーネントのトランジション  
  
Priority: 30  

`MUI` の `Alert` コンポーネントにトランジションを追加することで、表示および非表示時のアニメーションを設定することができます。  

# 基本的な使い方

トランジションを簡単に追加するために `Collapse` コンポーネントや `Slide` コンポーネントを使用することができます。  

## `Collapse` コンポーネントを使用した例

```tsx
import * as React from 'react';
import Alert from '@mui/material/Alert';
import Collapse from '@mui/material/Collapse';
import Button from '@mui/material/Button';
import Stack from '@mui/material/Stack';

export default function TransitionAlert() {
  const [open, setOpen] = React.useState(true);

  return (
    <Stack sx={{ width: '100%' }} spacing={2}>
      <Button
        variant="outlined"
        onClick={() => setOpen(!open)}
      >
        Toggle Alert
      </Button>
      <Collapse in={open}>
        <Alert severity="error">This is an error alert — check it out!</Alert>
      </Collapse>
    </Stack>
  );
}

```

## `Slide` コンポーネントを使用した例  

```tsx
import * as React from 'react';
import Alert from '@mui/material/Alert';
import Slide from '@mui/material/Slide';
import Button from '@mui/material/Button';
import Stack from '@mui/material/Stack';
import { TransitionProps } from '@mui/material/transitions';

const duration = 500; // トランジションの持続時間を500msに設定

const CustomSlide = (props: TransitionProps) => {
  return <Slide {...props} timeout={duration} />;
};

export default function CustomSlideAlert() {
  const [open, setOpen] = React.useState(true);

  return (
    <Stack sx={{ width: '100%' }} spacing={2}>
      <Button
        variant="outlined"
        onClick={() => setOpen(!open)}
      >
        Toggle Alert
      </Button>
      <CustomSlide direction="up" in={open} mountOnEnter unmountOnExit>
        <Alert severity="error">This is an error alert — check it out!</Alert>
      </CustomSlide>
    </Stack>
  );
}
```
