Title: ペインレイアウト（Pane layouts）  

Priority: 10

## ペインレイアウト（Pane layouts）
ウィンドウサイズに応じたペインレイアウトの選択、ペインの拡張とサイズ変更、ペインの適応方法、そしてXR環境での空間パネルについて説明します。  

### ペインレイアウトの選択
#### レイアウトの基本
 - ペインレイアウトは1〜3つのペインで構成されます。
 - 適切なペインの数はウィンドウサイズと製品の特性によって決まります。
 - ペインの種類：
   - 固定ペイン：幅が固定される
   - 柔軟ペイン：利用可能なスペースに応じて拡縮する

#### 推奨されるペイン数
| ウィンドウサイズ | 推奨ペイン数 | その他の選択肢 |
| ---- | ---- | ---- |
| コンパクト<br>(Compact) | 1 | -- |
| ミディアム<br>(Medium) | 1 | 2 |
| エクスパンデッド<br>(Expanded) | 2 | 1 |
| ラージ<br>(Large) | 2 | 1 |
| エクストララージ<br>(Extra-large) | 2 | 1, 3 |


### ペインレイアウトの種類
#### 単一ペインレイアウト
 - 1つの柔軟ペインのみを使用。
 - すべてのウィンドウサイズに対応可能だが、コンパクトやミディアムウィンドウに推奨。

#### 二分割ペインレイアウト
1. スプリットペインレイアウト
   - 2つの柔軟ペインを使用。
   - 折りたたみデバイスや動的レイアウトに最適。
   - ナビゲーションレールがある場合、左右のペインが適切に分割される。
2. 固定・柔軟ペインレイアウト
   - 1つの固定ペインと1つの柔軟ペインを使用。  
   - 主にエクスパンデッド・ラージ・エクストララージウィンドウで利用。  
   - 固定ペインはリスト表示やサイドシートなどに適用。  

#### 三分割ペインレイアウト
 - エクストララージウィンドウサイズでのみ推奨。
 - 3つ目のペインは標準のサイドシートとして使用。
 - 3つ以上のペインは推奨されない。

### ペインの拡張とサイズ変更
#### ペインのリサイズ方法
 - ドラッグハンドルを使用して、ペインを拡大・縮小・折りたたむことが可能。
 - スプリットペインレイアウトでは、両ペインの幅を自由に調整可能。
 - 固定・柔軟ペインレイアウトでは、固定ペインを完全に折りたたんで1ペインレイアウトに変更可能。

#### 推奨されるカスタム幅
 - 360dp
 - 412dp
 - スプリットペイン（中央揃え）

#### リサイズの保持
1. 永続的なリサイズ
   - ユーザーが調整したペイン幅を記憶。
   - アプリを閉じても、またウィンドウサイズを変更しても維持。
2. 一時的なリサイズ
   - ペインのサイズはアプリやペインを閉じるとリセット。
   - 補助的なペインレイアウトに適用。

### ペインの適応方法
ウィンドウサイズや向きの変化に応じて、ペインは以下の方法で適応します。

#### 表示・非表示
 - ウィンドウサイズに応じて、ペインが表示・非表示を切り替え。

#### 浮遊
 - ペインが他のコンテンツの上に表示される（モーダルウィンドウのような動作）。

#### 再配置（リフロー）
 - 縦画面ではサポートペインがメインペインの下に移動するなど、レイアウトを調整。

### 空間パネル（XRデバイス対応）
 - XRデバイスでは、ペインを空間パネル（Spatial Panels）として表示可能。
 - 背景と区別するため、明確な枠組み（コンテナ）を持たせることが推奨される。

### まとめ
 - ペインレイアウトはウィンドウサイズに応じて選択。
 - 固定ペインと柔軟ペインを組み合わせ、適応性を高める。
 - ペインのリサイズは永続的または一時的に調整可能。
 - ウィンドウサイズの変化に応じて、ペインは表示・非表示、浮遊、再配置のいずれかで適応。
 - XRデバイスでは、空間パネルを活用することで、より柔軟なレイアウトが可能。  

このように、ペインレイアウトはウィンドウサイズに適した表示方法を選択し、ユーザーエクスペリエンスを最適化することが重要です。
