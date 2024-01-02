Title: RiverpodでStateNotifierを使って状態を扱う

Priority: 30

RiverpodのStateNotifierを使うと状態を扱うことができます。Androidで言うところのViewModelっぽいものを作るときに便利そうです。

## StateNotifierを継承したクラスを作る

例としてログイン画面の状態を扱う `LoginViewModel` を作ってみます。状態部分は `sealed class` にしてみます。

```
class LoginViewModel extends StateNotifier<UiState> {
  final AccountRepository accountRepository;

  LoginViewModel({
    required this.accountRepository,
  }) : super(const Idle());

  void login(String email, String password) async {
    state = const InProgress();
    try {
      final account = await accountRepository.login(email, password);
      state = Success(account: account);
    } catch (e) {
      state = Error(e: e);
    }
  }
}

// 状態を表すクラス
sealed class UiState {
  const UiState();
}

class Idle extends UiState {
  const Idle();
}

class InProgress extends UiState {
  const InProgress();
}

class Success extends UiState {
  final Account account;
  Success({required this.account});
}

class Error extends UiState {
  final Object e;
  Error({required this.e});
}
```

## StateNotifierProviderを作る

 `StateNotifierProvider` を使って、`LoginViewModel` の作り方を指示します。
 `WidgetRef` があるので依存するオブジェクトを `read()` で取得することもできます。

```
final _viewModelProvider = StateNotifierProvider<LoginViewModel, UiState>((ref) {
  final accountRepository = ref.read(accountRepositoryProvider);
  return LoginViewModel(
    accountRepository: accountRepository,
  );
});
```

## watchで状態を取得する

 `ConsumerWidget` の `build()` の中で `ref.watch()` を使うと状態を取得・監視することができます。
状態が変化したタイミングで再度 `build()` が実行されます。

```
class LoginScreen extends ConsumerWidget {
  @override
  void build(BuildContext context, WidgetRef ref) {
    final uiState = ref.watch(_viewModelProvider);
    return switch (uiState) {
    }
  }
}
```

## StateNotifierを取得する

 `ref.read(provider.notifier)` で、 `StateNotifier` を取得することができます。
状態更新のためのメソッドを呼びたいときに使います。

```
class LoginScreen extends ConsumerWidget {
  @override
  void build(BuildContext context, WidgetRef ref) {
    // 取得する
    final viewModel = ref.read(_viewModelProvider.notifier);
    ...
    ElevatedButton(onPressed: () {
      viewModel.login();
    }, child: const Text("Login"));
  }
}
```
