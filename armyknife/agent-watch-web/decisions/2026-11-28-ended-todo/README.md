# 終わったセッションの to-do

tmux の pane を閉じてセッションが終わっても、答えていない to-do があるセッションは Inbox の Needs action に残り、動いているセッションの to-do と見分けがつかなかった。会話の to-do カードは Mark done / Reject だけで、Inbox から外す手段もなかった。

## 退けた案

最初は「終わったセッションを Inbox に残し、終わったことを示して Withdraw (取り下げる) で外す」前提で 3 つの問いを描いたが、どれも採らなかった。終わったセッションはそもそも Inbox に出すべきではない、という答えだったため。

Inbox の行での見分け方:

- A: タイトルの横に灰色の Ended を付け、ポインターを乗せると Withdraw を出す (iPhone は左スワイプで Later と Withdraw)。
- B: Needs action の下に Ended sessions の区分を作り、Withdraw all でまとめて取り下げる。
- C: 種類のアイコンを灰色にしてプレビューに Ended 14:32 と出し、Withdraw は会話の中だけに置く。

会話の to-do カード:

- A: 見出しに Session ended と添え、Mark done / Reject の右に Withdraw を置く。
- B: カードに「再開するまで答えは届かない」と書き、Withdraw を主のボタンにする。
- C: カードは今のままにし、This session has ended の帯の Resume の横に Withdraw to-do を置く。

Close の確認:

- A: 本文の下に Withdraws 1 to-do and 1 proposal. の 1 行を足す。
- B: 取り下げる to-do と proposal をタイトルで並べる。

## 案

終わったセッションは Inbox に出さない (未回答の to-do や proposal があっても出さない) と決めたうえで、残った to-do と proposal の扱い:

- A: 終わったときに、未回答の to-do と proposal を自動で取り下げる。
- B: pending のまま残し、Recent の行の印と会話のカードからだけ答える。答えるとセッションを再開して届ける。

## 採用した案

A。pane が閉じたとき、サーバーが未回答の to-do と proposal を取り下げる。

- 会話のカードは To-do · withdrawn · session ended 14:32 (proposal は Proposal · withdrawn · …) の見出しとタイトルだけになり、ボタンはない。
- トーストも Activity も出さない。
- 終わったセッションの会話はナビの Recent (✓ の行) と ⌘K から開く。Resume しても取り下げは戻らない。
- Close の確認には取り下げの件数も一覧も足さない。Proposal の本文から the proposal stays unchosen を外す。

## 理由

- 終わったセッションに待ちが残らないので、片付ける操作が要らない。
- カードを見れば、なぜ取り下げたかが分かる。
- B は pane が落ちても依頼を失わないが、行が Recent から押し出されるとほぼ気づけず、答えるたびにセッションが再開する。
