Title: Goでzipファイルを作る

Priority: 10

標準の `archive/zip` パッケージを使うとGoでzipファイルが作れます。

## 保存先を作る

まず保存先となるファイルを作ります。 

```
file, err := os.Create("test.zip")
if err != nil {
	panic(err)
}
defer file.Close()
```

## zip.Writerを作る

 `zip.NewWriter()`で作ります。 `io.Writer` があればいいので、Web APIの場合は `http.ResponseWriter` を渡せばよいです。
 
```
w := zip.NewWriter(file)
defer w.Close()
```

## ファイルを追加する

 `Create()` でzipに含めるファイルを追加します。フォルダにいれる場合は次のように `/` で区切っておきます。

```
entry1, err := w.Create("test/test1.txt")
if err != nil {
	panic(err)
}
entry1.Write([]byte("test1 file"))
```

`entry1` は単なる `io.Writer` なのでそのまま `Write()` したり、 `io.Copy()` で書き込んだりすればOKです。

## ヘッダ付きファイルを追加する

 `Create()` で追加したファイルにはヘッダ情報がないのでファイル作成日が `00-00-1980` になったりします。 
 `CreateHeader()` を使うとヘッダ情報付きでファイルを追加できます。
 
``` 
entry2, err := w.CreateHeader(&zip.FileHeader{
	Name:     "test/test2.txt",
	Method:   zip.Deflate,
	Modified: time.Now(),
})
if err != nil {
	panic(err)
}
entry2.Write([]byte("test2 file"))
```

## 全体

こんな感じになります

```
package main

import (
	"archive/zip"
	"fmt"
	"os"
	"time"
)

func main() {
	file, err := os.Create("test.zip")
	if err != nil {
		panic(err)
	}
	defer file.Close()

	w := zip.NewWriter(file)
	defer w.Close()

	entry1, err := w.Create("test/test1.txt")
	if err != nil {
		panic(err)
	}
	entry1.Write([]byte("test1 file"))

	entry2, err := w.CreateHeader(&zip.FileHeader{
		Name:     "test/test2.txt",
		Method:   zip.Deflate,
		Modified: time.Now(),
	})
	if err != nil {
		panic(err)
	}
	entry2.Write([]byte("test2 file"))

	fmt.Printf("Done!\n")
}
```
