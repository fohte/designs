# Inbox の To-do later の区分をなくす

待ちの to-do が全部畳んであるセッションは、Needs action から外し、そのすぐ下の To-do later の 1 行の区分にまとめていた (2026-11-21-todo-collapse)。ユーザーから「1 行になってしまっているのは期待していない。To-do later という枠組みはつくらなくていい。running なら running に出せばいい」と指摘があった。

案を並べずに、指摘のとおりに直した。canvas はない。

## 採用した形

- To-do later の区分をなくす。
- 待ちの to-do が全部畳んであるセッションは、今までどおり Needs action とその数から外す。
- そのセッションは、畳んだ to-do がないものとして区分を決める。動いていれば In progress、Later に回していれば Later、終わっていれば Done に出す。
- PC は行のプレビューに To-do · later を出す。iPhone は In progress の行に 1 to-do later のように件数を添える。

## 理由

- 区分を 1 つ増やすと、セッションの今の状態 (動いている、終わった) が Inbox から読めなくなる。
- 畳んだ to-do は後で確かめるものなので、Needs action に戻す理由はない。行の印で見つけられれば足りる。
