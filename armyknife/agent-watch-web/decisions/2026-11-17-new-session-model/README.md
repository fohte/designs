# New session でモデルと reasoning effort を選ぶ

watch-web の New session では engine と worktree は選べるが、モデルと reasoning effort は選べず、profile の既定値のまま起動していた。launcher はモデルと effort を受け取れるので、web からも選べるようにする。選べるモデルは engine ごとに、effort の段階はモデルごとに違う。

## 案

- 今: engine と worktree だけ選べる。モデルと effort は profile の既定値のまま。
- A: engine の横に、モデルと effort のチップを 1 つずつ並べる。
- B: モデルと effort を 1 つのチップにまとめ、開くと両方を選べる。
- C: engine とモデルを 1 つの選択にまとめ、effort も同じメニューで選ぶ。

## 採用した案

B。engine の右に、モデルと effort をまとめたチップを 1 つ置く。何も選んでいないときは、profile の既定値 (例: atlas-5 · high) を薄い文字で出し、default の印を付ける。開くと、その engine のモデルの一覧と、選んだモデルで使える effort の段階が出る。一覧の Default には、何に解決されるかを右に出す。engine を切り替えて、選んだモデルが新しい engine にないときは default に戻し、そのことを 1 行で知らせて Undo を出す。effort はそのモデルで使えるなら残し、使えなければそのモデルの default に戻す。コマンドパレットでは OPTIONS に Model · effort の行を置き、開くと同じように選べる。

例のモデル名はすべて架空。engine ごとのモデルの一覧をどこから取るかは実装で決める。

## 理由

- 今: モデルや effort を変えたいときに、web からは変えられない。
- A: チップが 4 つになり、スマホでは 2 行に折り返す。
- B: 入力欄の下のチップは 1 つ増えるだけで、モデルを選ぶと effort が使える段階だけに変わるので組み合わせを間違えない。
- C: メニューが長くなり、engine だけ変えたいときもモデルの並ぶメニューを開くことになる。
