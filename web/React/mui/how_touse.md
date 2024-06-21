Title: MUIの使い方
Priority: 20

## ReactプロジェクトにMUIをインストールする

それぞれ以下を参照。  

[Reactの開発環境を構築する](https://tech.mokelab.com/web/React/fundamental/setup.html)  
[MUIの導入]  

すでにMUI導入済みのプロジェクトがある場合は、このステップは飛ばして構いません。  

## コンポーネントをインポートして使用する

以下はButtonコンポーネントを使用する例です。  

```tsx
import React from 'react';
import Button from '@mui/material/Button'; // 1:ここでコンポーネントをインポートしています

const App: React.FC = () => {
  return (
    <div>
      <Button variant="contained" color="primary"> // 2:ここでコンポーネントを使用しています
        ボタンだよ！ // 3:ここでButtonに表示されるテキストを設定しています
      </Button>
    </div>
  );
}

export default App;
```

1. `@mui/material/Button`から`Button`コンポーネントをインポートしています。
2. `variant="contained"`はボタンのスタイルを設定しています。`contained`の他にも`text`や`outlined`などがあります。`color="primary"`はボタンの色を設定しています。他にも`secondary`や`inherit`などがあります。
3. 開始タグと終了タグの間にテキストを入れることで、`Button`に表示されるテキストを設定しています。
