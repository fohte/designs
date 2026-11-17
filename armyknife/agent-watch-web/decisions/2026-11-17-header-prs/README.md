# 会話のヘッダーの PR の出し方

desktop のヘッダーは右上に #番号 PR を並べるだけで、タイトル、repo、状態、CI が出ず、どれが今の branch の PR か分からない。merged / closed も同じ見た目で残り、phone のヘッダーには PR が出ない。

## 案

- current: 今の実装。#番号 PR を並べる。
- A: cwd の branch の PR だけを、状態の色、番号、タイトル、CI で出す。ほかの PR は別の +1 のボタンから This branch / Opened elsewhere / Merged に分けた一覧で見る。
- B: ヘッダーには open / draft の branch の PR だけを短く出し、すべての PR は右のパネルの Pull requests に並べる。
- C: ヘッダーの下に 1 行の帯を足し、open の PR を役割の名前つきで全部並べる。
- D: A からタイトルを外し、ほかの PR の数 (+1) を同じボタンに入れる。

## 採用した案

D。ヘッダーの PR は状態の色の点、番号、状態 (Open など) だけを出し、ボタン全体が A と同じ一覧を開く。ほかの PR がなくても ▾ を出し、全部 merged なら薄い ✓ Merged +1 にする。phone はタイトルの下に同じボタン (44px) を置き、押すと同じ一覧のシートを出す。

- CI は文字にせず、点の色だけで出す。実行中は GitHub に合わせて黄 (#fbbf24)、passed は緑。

## 理由

- A はタイトルでヘッダーの右側が広くなり、+N が PR と別のボタンに見えて分かりにくい。
- B は別の repo の PR が open でも、パネルを開くまで見えない。
- C は PR がある間、会話の高さが 36px (phone は open の PR ごとに 44px と、merged があればもう 44px) 減る。
- D はヘッダーの右側が A より狭く、PR の操作の場所が 1 つにまとまる。PR のタイトルは一覧を開くまで見えない。
