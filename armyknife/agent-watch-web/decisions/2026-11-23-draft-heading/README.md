# 何の draft かの見出し

状況パネルの Review タブには見出しがなく、開いている draft が issue へのコメント、PR draft、PR のレビューへの返信、ただの draft (a ai draft) のどれで、どこに出るのかが本文を読むまで分からなかった。

## 案

- A: 見出しに種類 (Issue comment / PR draft / Review replies / Draft) と対象を出す。対象は種類ごとに、issue の番号とタイトル、repo · ブランチと PR タイトル、PR の番号と返信するスレッドの数にする。PR draft だけは PR タイトルを見出しで直せる。
- 今のまま見出しを出さない。

## 採用した案

A。

## 理由

- 何の draft で、承認するとどこに出るのかが、開いてすぐ分かる。
- 表示には、draft ごとの種類と対象をサーバーから受け取る必要がある。
