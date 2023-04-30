Title: Reactで開発時と本番時で設定を変える

Priority: 110

 `create-react-app` で作ったReactアプリは、 `.env` ファイルで環境変数を取り込むことができます。
これを使って開発時( `npm start` )と本番時( `npm run build` )で設定を変えたりできます。

## .envファイルを作る

プロジェクトのルートに `.env.development` と `.env.production` を作ります。変数名は `REACT_APP_` プレフィックスが必要なので注意しましょう（[公式ドキュメント](https://create-react-app.dev/docs/adding-custom-environment-variables/))

```
# development
REACT_APP_BASE_URL="http://localhost:9000"
```

```
# production 
REACT_APP_BASE_URL="https://api.example.com"
```

## アプリ内で参照する

 `process.env.変数名` で参照できます。
 
```
<a
  className="App-link"
  href="https://reactjs.org"
  target="_blank"
  rel="noopener noreferrer"
>
  Learn React {process.env.REACT_APP_BASE_URL}
</a>
```




