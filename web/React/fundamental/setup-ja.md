Title: Reactの開発環境を構築する

Priority: 10


ReactでWebアプリの開発を始めるには、 `npm` と `vite` を使用します。以前は `create-react-app` を使っていました。

[viteの公式サイト](https://vite.dev/)

## プロジェクトの作成

プロジェクトを作るには `npm create vite@latest` を使います。

まず、必要となるパッケージのインストールに同意します。

```
% npm create vite@latest
Need to install the following packages:
create-vite@6.0.1
Ok to proceed? (y)
```

プロジェクト名を入力します。

```
? Project name: › vite-project
```

どのフレームワークを使うかを選びます。今回はReactのプロジェクトを作りたいのでReactを選びます。

```
? Select a framework: › - Use arrow-keys. Return to submit.
    Vanilla
    Vue
❯   React
    Preact
    Lit
    Svelte
    Solid
    Qwik
    Angular
    Others
```

次に言語等を選びます。特に理由がない限り `TypeScript + SWC` を選びます。 `SWC` は `Speedy Web Compiler` の略のようです。 [公式サイト](https://swc.rs/)

```
? Select a variant: › - Use arrow-keys. Return to submit.
    TypeScript
❯   TypeScript + SWC
    JavaScript
    JavaScript + SWC
    React Router v7 ↗
```

Doneと表示されると成功です。プロジェクトができました。

```
Done. Now run:

  cd vite-project
  npm install
  npm run dev
```

プロジェクトのフォルダに移動して `npm install` を実行した後、 `npm run dev` で開発サーバーが起動します。

```
VITE v6.0.3  ready in 379 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

`localhost:5173` にブラウザでアクセスすると次のような画面が表示されます。


