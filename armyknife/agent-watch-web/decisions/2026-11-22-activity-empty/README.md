# 操作がないときの Activity

Merge や Close を一度も実行していない (または Clear finished で全部消した) と、PC のナビにも iPhone のナビゲーションにも Activity がなかった。1 件目を実行すると quota の上に急に現れ、どこで結果を見るのかを実行する前に知る手段がなかった。

## 案

- A: 操作がなくても Activity を出し、ラベルを薄く (#8b8b94) して数は出さない。開くと No recent activity. と Merge and Close results appear here. を出し、Clear finished は出さない。
- B: A と同じに出し、薄い 0 を添える。開いたときは A と同じ。

## 採用した案

A。PC はナビの quota の上、iPhone はナビゲーションの quota の上に置く。

## 理由

- 置き場所がいつも同じで、結果を見る所が先に分かる。
- 意味のない 0 が目に入らない。数が出たら何かあった、と読める。
- いつもある分、ナビの下が 1 行ぶん常に埋まることは受け入れる。

## app との違い

app の iPhone は今、44px のアイコンだけの ActivityButton をヘッダーに置いている (`mobile-navigation-actions.tsx`)。screens と [2026-11-20-phone-activity](../2026-11-20-phone-activity/README.md) はナビゲーションの quota の上に置いており、この案は screens に合わせた。
