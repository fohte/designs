# Done 以外のセッションを閉じる

Close は Done のセッションにしか出なかった。答えられない Proposal で待っているものなど、Done 以外のセッションは tmux から閉じるしかなかった。

## 案

- A: Done 以外にも、Done と同じ場所 (PC のヘッダー、スマホのメニュー) に Close を出す。押すと Merge の確認と同じ中央のダイアログで確かめる。スマホは下からのシート。
- B: A と同じ場所に Close を出す。確認は押した場所に出す (ヘッダーの下のポップオーバー、Inbox の行の中、メニューの中)。
- C: Done 以外の Close は PC のヘッダーの新しい ⋯ メニューと、スマホのメニューの一番下に、赤い Close session… として置く。確認は A のダイアログ。

どの案も、パレットに Close this session を足す。Inbox の Close all とパレットの Close all done は Done だけを閉じるまま。

## 採用した案

C と A を合わせる。

- Done は今まで通り、PC のヘッダーとスマホのメニューの Close で、確認なしで閉じる。
- Done 以外 (Working、Question、Proposal、Approve、Review、Plan、Error、Later、待機中) は、PC のヘッダーの ⋯ の中と、スマホのメニューの一番下に離して置いた赤い Close session… から閉じる。
- 確認は Merge と同じ中央のダイアログで、スマホは下からのシート。Inbox の e も同じダイアログを出し、↵ で閉じ、Esc でやめる。パレットの Close this session も同じ。
- 確認の文言は状態で変える。見出しで何が失われるかを言い、確定のボタンは Working だけ Stop and close、ほかは Close session。
- 確認ダイアログは共通部品 ConfirmDialog にした。Merge、! コマンド、vibe mode の確認も同じ部品を使う。

## 理由

- Done の Close だけが目立つままになり、押し間違えで作業中のセッションを止めにくい。
- 赤字で離して置くので、ほかと違う操作だと分かる。
- どこから閉じても同じ確認になり、Merge の確認と同じ形なので確認だと一目で分かる。
- B は確認の形が 3 通りになり、パレットから閉じるときは置く場所がない。行の中は狭く、文言を短くするしかない。
