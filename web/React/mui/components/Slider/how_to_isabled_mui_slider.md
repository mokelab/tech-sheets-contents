Title: MUI の Slider コンポーネントを無効にする

Priority: 20  

MUI の `Slider` コンポーネントを無効にするには、`disabled` プロパティを使用します。  
このプロパティを `true` に設定すると、スライダーが無効になり、ユーザーは操作できなくなります。  

```tsx
<Slider
  aria-label="Volume"
  value={value}
  onChange={handleChange}
  disabled={true} // ここでスライダーを無効にしています
/>
```

![image](https://github.com/user-attachments/assets/30e16549-7882-4def-a9b0-b7ce30f082ab)
