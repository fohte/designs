# draft の本文の読み方

Review タブでは、状況パネルの細い幅に Markdown の生テキストとプレビューが 2 列で並び、どちらも読みにくかった。PC では Edit / Preview のボタンを押しても何も変わらなかった。

## 案

- A: パネルの中で 1 列にし、Preview と Edit を切り替える。開いたときは Preview。
- B: パネルには本文の冒頭と Read full width だけを出し、押すと会話の列を置き換えて Markdown とプレビューを左右に並べる。
- C: ふだんは A、長い draft は全幅の入口から B の画面を開く。iPhone は A。
- D: C の形のまま、Preview で draft の種類ごとに読める形にする。
  - PR draft は frontmatter の title などを入力欄にし、その下に Markdown を出す。
  - issue は Title、Labels、Assignees、親と子の issue を欄に分け、その下に本文を出す。
  - レビューへの返信は、スレッドごとにファイルと行、コメントした行を目立たせた diff、レビュアーのコメント、返信の欄、Resolve を 1 枚にまとめる。

## 採用した案

D。

- 一番上の行にどの draft かを出し、PC は右端の ⛶ で全幅に開く。iPhone はもともと全画面なので ⛶ を置かない。
- frontmatter は Body の上の別の欄に分け、Preview でもその場で直せる入力欄にする。
- Edit は生のファイルをそのまま出す。

## 理由

- A から C は PR draft なら読めるが、レビューへの返信と issue の frontmatter は、生のファイルの形のままでは読みにくいという指摘を受けた。
- 種類ごとの形にすると、承認する前に確かめたいこと (どのスレッドに何と返すか、issue のラベルや担当) が本文と分かれて読める。
- frontmatter を Body の見出しの下に置くと本文の一部に見え、表示だけだと人が直せなかったので、欄を分けて入力欄にした。
