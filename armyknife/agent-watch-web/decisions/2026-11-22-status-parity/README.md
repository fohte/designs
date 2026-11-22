# Session status の PC と iPhone の見た目

Session status の各タブ (Running、Tasks、Tree、Review、Decisions、Web UI) が、PC と iPhone で違う形になっていた。同じものは同じ部品・同じ見た目にする。案を並べる canvas は作らず、screens を直接そろえた。

## 決めたこと

- タブバーを `StatusTabs`、各タブの中身を `StatusBody` の部品にし、PC の `StatusPanel` と iPhone の `PhoneStatusPanel` の両方が読み込む。`size=desktop|phone` で切り替える。
- Tree: PC の 3 行 (題名 / role とタスク / リポジトリ) に寄せる。iPhone の 2 行ではタスク名がリポジトリ名に押されて途切れていた。
- Tasks: 終わったタスクも、進行中と同じ 2 行にする。
- Decisions: iPhone の形 (OK と Change… を横 2 列、送り先はボタンの下) に寄せる。
- Review: iPhone の形 (項目名は上、Edit と Preview の切り替え、Save と Finish review は横 2 列) に寄せる。PC で編集と表示を左右に並べる形はやめる。Preview を選んだ状態も PC と iPhone で並べる。
- Running と Web UI: Output ボタンの枠と、新しいタブで開くアイコンをそろえる。

## 残した違い

- 文字の大きさ (PC 13px、iPhone 15px): iPhone アプリ全体の大きさに合わせる。
- ボタンの高さ (PC 30px、iPhone 44px) とタブの間隔: 指で押すため。
- iPhone のタブバーは横にスクロールする: 画面の幅が足りないため。
- ⛶ (全幅で開く) は PC だけ: iPhone のタブはもともと画面の幅いっぱいのため。
- キー操作の表示は PC だけ: iPhone にはキーボードがないため。
- 閉じ方: PC は ×、iPhone は見出しの戻るボタン。iPhone では別のページとして開くため。
