Title: How to use MUI

Priority: 20

# Install MUI in your React project

Please see below.  

[Build a React development environment](https://tech.mokelab.com/web/React/fundamental/setup-en.html)  

[Introduction of MUI](./introduction-en.html)  

If you already have a project with MUI, you can skip this step.  

Import and use the component

Below is an example of using the Button component.  

```tsx
import React from 'react';
import Button from '@mui/material/Button'; // 1: import 

const App: React.FC = () => {
  return (
    <div>
      <Button variant="contained" color="primary"> // 2: use 
        Button! // 3: content
      </Button>
    </div>
  );
}

export default App;
```

1. Import the `Button` component from `@mui/material/Button`.
  
2. `variant="contained"` sets the style of the button. Other options are `contained`, `text`, and `outlined`. `color="primary"` sets the color of the button. Other options are `secondary` and `inherit`.
  
3. You set the text that appears on the `Button` by putting the text between tags.

