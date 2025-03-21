Title:ステート（States）の概要  
Priority: 10

## ステート（States） （状態）
ステート（状態）は、コンポーネントやUI要素がどのようなインタラクション状態にあるかを示します。

### ステートの基本原則
#### アクセシビリティの確保
各ステートには、視認性を高めるための2つの視覚的指標が備わっています。
#### ステートの組み合わせ
選択やホバーなど、複数のステートを同時に適用することができます。
#### 一貫した適用
すべてのコンポーネントにおいて、ステートを統一的に適用することが重要です。

### 各ステートの詳細

#### ① 有効（Enabled）
 - インタラクティブな要素であることを示す。
 - ボタンの場合、コンテナーとテキストのコントラストが強くなる。  

#### ② 無効（Disabled）
 - 操作できない要素であることを示す。  
 - ボタンの場合、灰色のコンテナー上に低コントラストの灰色のテキストが表示される。  

#### ③ ホバー（Hover）
 - ユーザーが要素の上にカーソルを置いた状態を示す。  
 - ボタンの場合、カーソルがボタン上にあることが視覚的に分かるように変化する。  

#### ④ フォーカス（Focused）
 - キーボードや音声入力などで要素が選択された状態を示す。  
 - ボタンの場合、コンテナーとテキストのコントラストが強調される。  

#### ⑤ 押された（Pressed）
 - ユーザーがボタンをタップまたはクリックしたことを示す。  
 - ボタンの場合、押されたことが分かるようにコンテナーとテキストのコントラストが変化する。  

#### ⑥ ドラッグ（Dragged）
 - ユーザーが要素を押して移動させている状態を示す。  
 - チップなどのコンポーネントをドラッグすると、その状態が視覚的に表示される。  
