Title: MockKを使ってメソッドの結果を指定する

Priority: 110

 `every { } `を使うと、指定したモックオブジェクトのメソッドが呼ばれた際の結果を指定することができます。

こんなインターフェースがあったとします。

```
interface AccountRepository {
  /**
   * サポートしているアカウント種別をリストで返す
   */
  fun listAccountTypes(): List<String>
}
```

MockKを使って、 `listAccountTypes()` の結果を指定してみます。

```
@Test
fun testLogin() {
  // モックオブジェクトを作る
  val repo = mockk<AccountRepository>()

  // every { } を使って結果を指定する
  every { repo.listAccountTypes() } returns listOf("Google", "X")

  // repoを使うオブジェクトを作る
  val viewModel = LoginViewModel(repo)

  // viewModelのメソッドを呼ぶ。内部で listAccountTypes() が呼ばれることになっている
  viewModel.login()

  // 結果のアサーション
}
```
