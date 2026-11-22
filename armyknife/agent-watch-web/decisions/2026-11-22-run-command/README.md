# Run command の進み具合と結果

メッセージの `a agent ...` などの ! コマンドで Run command を押すと、確認ダイアログが Running command… のまま閉じず、終わるまでほかの操作ができなかった。Merge と Close はダイアログを閉じて裏で実行し、トースト、Activity、会話の最後の 1 行で結果を出しており、これに種類を足して揃える。

文言とアイコンは 3 案で同じ。

- 実行中: Running command (会話の行は Running command…)
- 成功: Ran command。トーストは自動で消える
- 失敗: Command failed · exit 1 (会話の行は Command failed (exit 1))
- 時間切れ: Command timed out と Stopped after 30 s.

## 案

- A: トーストの 2 行目はコマンド。失敗と時間切れは Retry と Details を置き、Activity の行に stderr の最後の数行を出す。
- B: トーストの 2 行目はセッションのタイトル。失敗と時間切れは Details だけを置く。Activity の行は A と同じ。
- C: トーストの 2 行目はコマンド。失敗と時間切れのトーストと Activity の行は Show output だけを置く。押すとそのセッションの会話で、サーバーが送った結果のメッセージ (終了コードと stdout / stderr) までスクロールして枠で示す。会話の最後の行にはボタンを置かない。

## 採用した案

C。PC のトーストは画面の左下 (left 16px、bottom 16px) に置く。

## 理由

- API を変えずに出せる。`commands/execute` が返すのは `exitCode`、`succeeded`、`timedOut` だけで、出力はサーバー (`bang_commands.rs` の `command_result_message`) がセッションへ結果のメッセージとして送っている。C はそのメッセージを指すだけでよい。
- 見せる出力が、エージェントが読んだものと同じになる。出力の置き場所が会話の 1 か所に決まる。
- トーストから Retry で同じコマンドをもう一度実行する道を作らない。やり直すときは、メッセージのボタンをもう一度押す。
- 出力を見ると今の画面から会話へ移ることと、Activity では出力を読めないことは受け入れる。
