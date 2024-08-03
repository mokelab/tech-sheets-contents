Title: MUI の TextField コンポーネント の種類

Priority: 20  

TextField には主に3つのバリアントがあります。  

# standard  

デフォルトのバリアントです。  
シンプルで基本的な入力フィールドに最適です。過度に強調する必要がない場合に適しています。  
フォーカス時に下線の色が変わり、アクティブな状態を示します。  

```tsx
<TextField />
// または
<TextField variant="standard" />
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/0cd669f4-2106-491d-9898-30a5126733b0)  

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/4cda556d-6901-48b5-954b-498abb1420ec)

# outlined  

入力フィールド全体が枠で囲まれたデザインです。  
フィールドを明確に区別し、視覚的に分かりやすくしたい場合に最適。複雑なフォームやカードデザインに適しています。  
エラーステートやフォーカス時に枠線の色が変わります。

```tsx
<TextField variant="outlined" />
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/3d8b34bc-c552-4162-a8a8-1152cc9c302e)  

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/6ab0a1aa-4961-4ab8-8283-af63e7672780)  

# filled  

入力フィールドの背景が塗りつぶされているデザインです。  
強調されたデザインと明確な視覚的フィードバックが必要な場合に最適。重要な入力フィールドやモダンなUIデザインに適しています。
フォーカス時に背景色が変わることで、アクティブな状態を示します。  

```tsx
<TextField variant="filled" />
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/6a0c9091-3904-4593-bde8-c0aed816682a)  

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/d2cbe814-1ab5-403b-8b90-19e8158fadba)



