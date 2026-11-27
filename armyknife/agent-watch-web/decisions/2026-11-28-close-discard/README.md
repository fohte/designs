# Close が止まったときに変更を捨てて worktree を消す

Close は、コミットしていない変更か merge していないブランチがあると、何も消さずに止まる。選べるのは Close and keep worktree、Retry、Details (Activity では Open in terminal) だけで、変更を捨てて worktree ごと消すにはターミナルで消すしかなかった。赤い Discard changes and close… を足し、押すと消す前の確認を出す。

## 案

ボタンの置き場所 (ページ「選択肢の置き場所」):

- A: 今のボタンの下に、赤い枠の Discard changes and close… を幅いっぱいの 4 つ目のボタンとして足す。トースト、会話の行、Activity の行で同じ並び。
- B: ボタンの並びの最後に ⋯ を置き、開いたメニューに Discard changes and close… を入れる。iPhone は下から出るシート。
- C: トーストは今のままにし、Activity の行の一番下にだけ赤い枠のボタンを置く。

この 3 案はすべて退けた。ボタンの大きさがばらばらで、一番下に幅いっぱいの枠だけのボタンを置く形が Cancel に見えたため。描き直した案 (ページ「ボタンの並び」) は、どれもボタンの高さを PC 26px、iPhone 44px に揃え、赤い塗りは確認の最後の 1 押しだけに使う:

- A: Close anyway の見出しの下に、白い Keep worktree と赤い枠と文字の Discard changes… (ゴミ箱付き) を同じ幅で並べ、Retry と Details はその下。2 列 2 段の同じ大きさのボタン。
- B: Close and keep worktree の右端に ▾ を付けた分割ボタンにし、▾ のメニューに Discard changes and close… を入れる。
- C: 同じ幅のボタンを縦に積み、2 段目に Discard changes and close… を赤い文字とゴミ箱で置く。3 段目に Retry と Details。

消す前の確認 (ページ「消す前の確認」)。どの案も Uncommitted changes (M / A / D / ?? とパス) と Commits not on main (短い sha と件名) に分ける:

- A: 全部を並べ、長いときは枠の中でスクロールする。赤いボタンを押すだけ。
- B: 区分ごとに 5 件まで出し、残りは Show 9 more で開く。赤いボタンを押すだけ。
- C: B のリストに加え、ブランチ名を打つと赤いボタンが押せる。

## 採用した案

ボタンの並びは描き直した A、消す前の確認は B。

トースト、会話の行、Activity の行で同じ並びにし、Activity では Details の位置に Open in terminal を置く。会話の行には Details を新しく足す。

## 理由

- 4 つのボタンの大きさが揃い、Discard changes… が閉じ方の 2 択の片方に見えるので、Cancel に見えない。開かなくても見つかる。
- 件数が先に目に入り、5 件までなら全部見える。押したあとに中身が変わっていれば何も消さずに止めるので、確認は押すだけで足りる。
