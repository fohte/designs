# 新しいセッションを裏で起動する

New session で Start を押すと、Start が Starting… になり、空いた所に Starting session… Waiting for it to appear in the session list. を出していた。待つ間に Inbox やほかのセッションへ移れても、作成中だと分かる表示はどこにもなかった。新しいセッションが一覧に現れると、どの画面にいてもその会話へ切り替わり、読んでいた会話や入力中の返信から引き離された。

決まっていたこと: + の画面に留まっていれば今どおり新しいセッションへ移る。離れたら移らず、Activity に作成中として出し、始まったら通知し、Activity の行と通知の両方から開ける。始められなかったら理由と Retry を出す。

## 案

作成中をどこに出すか:

- A: Merge と同じく、左下 (iPhone は下端) のトーストと Activity の先頭の行に Starting session を出す。ナビの Activity は実行中の青い数にする。
- B: トーストは出さず、ナビの Activity のすぐ上に作成中の行を出し続ける。iPhone は ☰ に青い印を付ける。

始まったときの通知:

- A: トーストが Session started と Open に変わり、5 秒で消える。
- B: トーストは出さず、ナビの Activity に緑の ✓ と数を付け、行に Open を出す。

Start を押した直後の + の画面:

- A: 今の画面のまま、Starting session… と You can leave this page. の 1 行を出す。入力欄はメッセージを残して薄くする。
- B: 送ったメッセージを会話の形で出し、その下に Starting Claude Code in … を出す。入力欄は空にして Reply once the session starts とだけ出す。

## 採用した案

作成中は A、通知は A、+ の画面は B。

- - の画面を離れると、Merge と同じトーストと Activity の先頭の行に Starting session、最初のメッセージの 1 行目、repo を出す。
- 始まったらトーストと行を Session started と Open に変え、トーストは 5 秒で消える。行は Clear finished まで残る。
- - の画面は、会話の部品 (PC は Conversation、iPhone は PhoneChat) で描く。最初のメッセージを自分の発言として出し、その下に会話の結果の 1 行と同じ部品で Starting Claude Code in … を出す。

## 理由

- 作成中と通知を Merge、Close、! コマンドと同じ見え方にすれば、新しく覚えることがない。トーストと Activity の部品に種類を足すだけで済む。
- B の通知 (緑の印) では、印に気付くまで始まったことが分からない。
- - の画面の B は、今の画面からの変更が A より大きく見えた。しかし普段の会話の部品をそのまま使えるので、新しい部品は作らずに済む。始まったあとの会話と同じ形なので、切り替わったときに画面が飛ばない。何を送ったかと、どこで始めているかも読める。
- A の + の画面では、送ったメッセージが入力欄に残り、まだ送れていないように見えた。
