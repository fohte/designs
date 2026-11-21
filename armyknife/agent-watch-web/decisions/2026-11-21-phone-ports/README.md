# PC にしかなかった画面の iPhone 版

PC と iPhone の画面は 1 対 1 で描く。screens には、iPhone 版のない PC の画面が残っていた。メッセージの種類 (MessageKinds)、返答を待つカード (Cards)、確認ダイアログ (Dialogs)、Merge がキューに入ったとき (ActionQueued)、別のセッションに移ったあとの結果 (ActionAway)、エンジンを変えてモデルが既定に戻ったとき (NewSessionModelSwitch) の 6 つ。

## 変えたこと

- 6 つの PC の画面の右に、それぞれの iPhone 版 (`screens/` の PhoneMessageKinds、PhoneCards、PhoneDialogs、PhoneActionQueued、PhoneActionAway、PhoneNewSessionModelSwitch) を足した。状態は PC と同じで、iPhone の部品と寸法 (本文 15px、押せるところは高さ 44px か 48px、ダイアログは下からのシート) に合わせただけ。
- 状態を並べた PC の画面 (MessageKinds、Cards、Dialogs) は、同じ状態を幅 390px で縦に並べた 1 枚にした。
- ConfirmDialog の sheet に、modal と panel にあった code (コミットのハッシュ) と details (作業ディレクトリとコマンド) を足した。iPhone の Merge の確認と ! コマンドの確認に使う。

## 案を出さなかった理由

既にある iPhone の部品と寸法をそのまま当てはめただけで、選ぶことがなかった。そのため案は出しておらず、比べるための canvas も作っていないので `project/` は残していない。
