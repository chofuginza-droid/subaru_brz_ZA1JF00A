# ZA1JF00A 定義の一覧

Author: S.S  2026-09-27

データ番地は ECU アドレスです。チェックサムは `subarudbw` のままにした。マップではないので、この表には入れていません。

確認できた表は、EcuFlash で軸と数値がマップとして見えたものです。`ZA1JF00A.xml` には、確認できた表だけを残しました。断定できない表は定義ファイルから外しました。

## 確認できた

| 表 | データ番地 | 軸 | 見えた内容 |
| --- | --- | --- | --- |
| Primary Open Loop Fueling | `117064` | 負荷 `116fd0` 14点、回転 `117008` 23点 | 負荷 0.15〜1.40、回転 800〜7400。低負荷 14.70、高負荷は 11.6〜13.7 |
| Base Timing A | `1162c0` | 負荷 `11622c` 14点、回転 `116264` 23点 | 負荷が上がると進角が減る。低回転・高負荷は約 -18 度 |
| Base Timing B | `116498` | 負荷 `116404` 14点、回転 `11643c` 23点 | A と同じ形で、高負荷側の進角が少し大きい |
| Rev Limit (Fuel Cut) | `10cc7c` | 2点 | On Above 7400、Off Below 7200 |
| Speed Limiting A Sport/Sport Sharp | `13c344` | 2点 | 表示 109 / 115 mph（中の値 175 / 185） |
| Speed Limiting B Sport/Sport Sharp | `13c350` | 2点 | 上と同じ |
| Speed Limiting A Intelligent | `13c35c` | 2点 | 上と同じ |
| Speed Limiting B Intelligent | `13c368` | 2点 | 上と同じ |
| MAF Sensor Scaling | `11e31c` | 電圧 `11e244` 54点 | 0.90V で 0.85g/s から 5.00V で 279.23g/s まで単調増加 |
| MAF Compensation (IAT) | `104e0c` | 温度 `104dcc` 6点、空気量 `104de4` 10点 | 冷間はプラス補正、高温はマイナス補正 |
| Timing Compensation (IAT) | `115274` | 温度 `115234` 16点 | -40℃で 0 度、高温側で最大約 -8 度 |
| MAF Correction After Start (Neutral) | `11ad98` | 水温 `11ad4c` 11点、モード `11ad78` 8点 | モード1・2は冷間 40 g/s から高温 6 g/s。モード3以降は 8 g/s から 4 g/s |
| MAF Correction After Start (In Gear) | `11ae94` | 水温 `11ae48` 11点、モード `11ae74` 8点 | モード1の冷間だけ 35 g/s。それ以外はニュートラルに近い |
| Injector Latency | `112398` | 電圧 `112378` 5点、吸気圧 `11238c` 3点 | 6.5V で 3.24ms、16.5V で 0.49ms。吸気圧 -19.34 / 0 / 19.34 psi の3段は同じ |
| Cranking Fuel IPW Compensation (MAP) | `10d3c4` | 吸気圧 `10d39c` 10点 | 3.56psi で -75.8%、14.70psi で 0%。間はほぼ一定の刻み |
| Coolant Temp Sensor Scaling | `11df4c` | 電圧 `11dedc` 28点 | 0.45V で 248°F（120℃）から 4.67V で -40°F。電圧が上がると温度が下がる |
| Timing Compensation Per Cylinder A | `116cec` | 回転 `116c94` 16点、負荷 `116cd4` 6点 | 負荷 0.30 と 0.50 は 0 度。0.70 以上は 2400rpm 付近から最大 -3.87 度 |
| Timing Compensation Per Cylinder B | `116da4` | 回転 `116d4c` 16点、負荷 `116d8c` 6点 | A と同じ軸で、補正の並びも A と同じ |
| Timing Compensation Per Cylinder C | `116e5c` | 回転 `116e04` 16点、負荷 `116e44` 6点 | 全面 0 度 |
| Timing Compensation Per Cylinder D | `116f14` | 回転 `116ebc` 16点、負荷 `116efc` 6点 | 全面 0 度 |
| Requested Torque B (Accelerator Pedal) | `13cd38` | ペダル `13cc9c` 16点、回転 `13ccdc` 23点 | ペダル 0% は 0。100% では 800rpm で 148.9、高回転側は 200 前後まで増える |
| Requested Torque A (Accelerator Pedal) | `103a18` | ペダル `103990` 16点、回転 `1039d0` 18点 | ペダル 0,10,…,100%。回転 800〜7600。800rpm・100% は 250、7600rpm・100% は 171 |
| Per Injector Pulse Width Compensation A〜H | `111620` から 8枚 | 噴射時間 `1115cc` 9点、回転 `1115f0` 12点 | A は 1〜17ms、回転 800〜7200。全面 -50.00。中の数は 64。共通定義 `32BITBASE.xml` の `InjectorPulseWidthCompensation` の式は `toexpr="(x*.78125)-100"`。128 が 0% なので、64 は -50 と出る。この式の範囲外。式は変えず -50 のまま残す。B〜H も同じバイト |
| Target Throttle Plate Position Maximum | `13c834` | 要求トルク `13c784` 21点、回転 `13c7d8` 23点 | 要求トルク 0〜1、回転 800〜7400。開度は 0% から最終列で約 102.4% |
| Engine Load Compensation (MP) | `104ed0` | 吸気圧 `104e5c` 14点、回転 `104e94` 15点 | 吸気圧 -11.31〜0.00psi、回転 600〜4800。高真空側は約 +4〜8%、大気圧付近は 0% 前後 |
| Transient Ignition Retard | `116a98` | 負荷 `116a1c` 7点、回転 `116a38` 24点 | 負荷 0.15〜0.70、回転 800〜7400。共通定義 `32BITBASE.xml` の `TransientIgnitionRetard` の式は `toexpr="x*.3515625-30"`。0度は中の数約85。800rpm は 10.08度（中の数114）〜19.92度（中の数142）。5200rpm までは低負荷も約19.92度だが、5600rpm 以降の負荷 0.15〜0.50 付近だけ中の数43で -14.88度になる。負荷 0.60 と 0.70 は 19.92度のまま。マイナスは走行結果ではなく、85未満が式で0を下回った表示。共通定義の範囲は 0〜26.72度なので範囲外。式は変えていない |
| Transient Ignition Retard Temperature Compensation | `1169ac` | 水温 `116950` 16点、吸気温 `116990` 7点 | 水温は -40〜230°F（中の値 -40〜110℃）、吸気温は -40〜176°F（中の値 -40〜80℃）。マスは全面 1.0000。中の数は 128 で、共通定義の単位表示は Estimated Air/Fuel Ratio。点火の度ではなく、その式の 1.00 |
| Calculated Torque A | `101fb0` | 負荷 `101f24` 12点、回転 `101f54` 23点 | 負荷 0.10〜1.20、回転 800〜7400。800rpm は 14.01 から始まり、負荷 1.00 以降は 143.32。高回転の低負荷は 40 前後、高負荷は 220 前後 |
| Calculated Torque B | `102260` | 負荷 `1021d8` 11点、回転 `102204` 23点 | 負荷 0.10〜1.10、回転 800〜7400。800rpm は 14.01 から始まり、負荷 0.70 以降は 115.87 |
| Cylinder Fill Percentage | `1075c4` | 回転 `10752c` 16点、スロットル `10756c` 22点 | 回転 800〜6800、スロットル 0〜84%。0% は全面 0。開くほど 100 に近づき、高回転側は低くなる。84% でも高回転は 100 より低い |
| GDI Flow Rate | `1143cc` | 燃圧 `11437c` 6点、MAF電圧 `114394` 14点 | 燃圧 2〜20MPa、電圧 0.60〜5.00V。値はだいたい 0.97〜1.20。単位表示は Flow |
| Ignition Timing Compensation Idle Target In Error Range A | `116740` | 回転誤差 `114de0` 9点、回転変化 `11671c` 9点 | 誤差 -300〜200rpm、回転変化 -20〜20rpm。度はおおよそ -10〜10。カテゴリは ALPHA Idle Control |
| Ignition Timing Compensation Idle Target In Error Range B | `1167f8` | 回転誤差 `1167b0` 9点、回転変化 `1167d4` 9点 | 誤差は -200〜200rpm。A と数字は違う。度はおおよそ -12〜12 |
| Desired Overrun Mass Airflow A | `119a14` | 回転 `119980` 21点、水温 `1199d4` 16点 | 回転 400〜6800、水温 -40〜230°F。水温の行はすべて同じ。400rpm は 1.83、6800rpm は 19.06。画面下の単位は Unknown |
| Desired Overrun Mass Airflow B | `119d60` | 回転 `119ccc` 21点、水温 `119d20` 16点 | 軸は A と同じで、水温の行もすべて同じ。400rpm は 1.52、6800rpm は 9.64。単位は Unknown |
| Idle Speed Target A〜G | A `118b40`、B `118b60`、C `118b80`、D `118ba0`、E `118bc0`、F `118be0`、G `118c00` | 水温 `117fdc` 16点（共通） | 水温 -40〜230°F。A は 1800rpm から 650、B は 1800（86°F で 1650）から 650、C は 1200 から 700、D は 1250 から 650、E と F は同じ中身で 1325 から 700、G は 1200 から 700（104〜158°F が 1050/1000/950/850/750 の段）。決め方は、同じ水温軸の16点曲線が 32 バイトおきに 7 本並び、`ZA1JF00C.xml`の配置と一致したこと |
| Cranking Fuel Injector Pulse Width A (ECT)_ | `1120a8` | 水温 `10cd78` 16点、段 `11209c` 3点（2・4・5） | 水温 -40〜230°F。段2・4は -40°F で 114.80ms から 230°F で 11.00ms。段5は 268.60ms から 8.80ms。決め方は、確認済みの Cranking Fuel IPW Compensation (MAP) を読む始動プログラム（`57aa2`〜`58660`）がこの5枚を読み、5枚の間隔（0xF8、0x48、0xD8、0x48）が`ZA1JF00C.xml`と一致したこと。共通定義に無い名前なので表の形（3D、ms 換算）はこの定義ファイルに書いた |
| Cranking Fuel Injector Pulse Width B (ECT)_ | `1121a0` | 水温 `10cd78` 16点、段 `112198` 2点（4・5） | 段4は 100.00ms から 11.00ms、段5は 90.00ms から 8.80ms |
| Cranking Fuel Injector Pulse Width C (ECT)_ | `1121e8` | 水温 `10cd78` 16点、段 `1121e0` 2点（4・5） | 段4は 107.40ms から 11.00ms、段5は 179.30ms から 8.80ms |
| Cranking Fuel Injector Pulse Width D (ECT)_ | `1122c0` | 水温 `10cd78` 16点、段 `1122b8` 2点（4・5） | 中身は B と同じ |
| Cranking Fuel Injector Pulse Width E (ECT)_ | `112308` | 水温 `10cd78` 16点、段 `112300` 2点（4・5） | 中身は C と同じ |
| Cranking Fuel Injector Pulse Width F (ECT) | `10dd76` | 水温 `10cd78` 16点 | -40°F で 114.80ms、14°F で 124.00ms、230°F で 11.50ms。同じ始動プログラムが読む ms 換算の水温曲線はこれ1本 |
| Front Oxygen Sensor Scaling | `11e428` | 電流 `11e3f4` 13点 | -0.75mA で 12.17、0.00mA で 14.70、0.30mA 以上で 20.28 の A/F。13点の曲線は 2 本あるが、プログラムから読まれているのは `11e428` だけ（`4d074` 経由）。`11e490` はどこからも読まれていない予備 |
| Timing Compensation A (ECT) | `1151f2` | 水温 `114b30` 16点 | 水温 -40〜230°F で全面 0.00 度。プログラムが B と続けて読む組（`6a5d4`）。A-B の距離 0x10、軸との距離 0x6C2 が`ZA1JF00C.xml`と一致 |
| Timing Compensation B (ECT) | `115202` | 水温 `114b30` 16点 | 全面 0.00 度 |
| CL Fueling Target Compensation A (Load) / B (Load) | A `1138ac`、B `1139f8` | A は負荷 `113854` 11点・回転 `113880` 11点、B は負荷 `1139a0`・回転 `1139cc` | A は B と同じバイト。負荷 0.20〜1.20、回転 800〜5600。800rpm は -0.029、回転が上がるほどマイナスが増え、5200rpm 以上は -0.294、高負荷側は -0.441（A/F の加算）。プログラム `5e7b4` が A、`5e7c2` が B を読み、RAM のフラグ（`fff8c917`）が 0 のとき A、それ以外は B |
| Primary Open Loop Fueling Additive | `111238` | 負荷 `1111a8` 13点、回転 `1111dc` 23点 | 負荷 0.30〜1.40、回転 800〜7400。負荷 0.80 以下は 0.00（高回転は 0.05 前後）、0.85 以上で 0.19〜0.30、7400rpm の高負荷は 0.45。同じ形の表は 2 枚あるが、共通定義の換算（0 起点の加算）に合うのはこれだけ。もう 1 枚 `111408` は 128 を 1.00 とする倍率表で別物 |
| Intake Cam Advance Angle Base AVCS_ | `12201c` | 負荷 `121f98` 12点、回転 `121fc8` 21点 | 負荷 0.15〜1.00、回転 800〜6800。800rpm は全面 0 度、2200〜3200rpm の負荷 0.90 以上で最大 37 度、6800rpm の負荷 0.90 以上は 0 度。吸気カムのプログラム（`8dc88`）が読む 12×21 |
| Exhaust Cam Retard Angle Base AVCS_ | `121a48` | 負荷 `1219c4` 12点、回転 `1219f4` 21点 | 負荷 0.15〜1.00、回転 800〜6800。低回転・低負荷は 0 度、2400〜2800rpm の負荷 0.70〜0.80 で最大 50 度、4800rpm 以上の低負荷は 40 度、高負荷側は 20 度以下。排気カムのプログラム（`9022a`）が読む 12×21。この ROM では 1 バイト・-40 の換算なので、共通定義（2 バイト）は使わず、この定義ファイルに `RetardBRZ(degrees)u8` を書いた |
| Cranking Fuel IPW Compensation A (RPM) | `110a34` | 回転 `110a04` 5点、水温 `110a18` 7点 | 回転 115〜515（100 刻み）、水温 -22〜32°F。全面 0.0%。この形（5×7）の表は 1 枚だけ |
| GDI Firing Angle Cold Idle / High Load Cold / High Load Hot / Low Load Cold / Low Load Hot | `110198`、`1102c4`、`1103f0`、`11051c`、`110648` | 負荷 11点・回転 17点。順に負荷 `110128` `110254` `110380` `1104ac` `1105d8`、回転 `110154` `110280` `1103ac` `1104d8` `110604` | 負荷 0.20〜1.20、回転 800〜7200。800rpm は負荷 0.70 まで 320 度、0.80 以上は 300 度。3600rpm は全面 300 度。7200rpm は低負荷 320 度から高負荷 370 度。5 枚の中身は同じ。データ番地は `110198` から 0x12C おきで、`ZA1JF00C.xml`の間隔と同じなので、その並びのまま名前を付けた。どの条件で何枚目を読むかは、クランキング A〜E の文字と同じで並び順 |
| 故障コード（P と U）197個 | 記録の先頭バイト。先頭は `11bff0`。P0300 は記録が 2 件（`11bff0` と `11bffc`） | 1バイト。0 が disable（オフ）、1 が enabled（オン） | 197個のうち disable（オフ）は 69 個。残り 128 個は enabled。記録は 12 バイトで `11bff0` から 198 件。P0300 だけ記録が 2 件なので、197 + 1 = 198。プログラムは先頭が 1 のときだけその記録を使う。共通定義に名前が無かった P0504 は、この定義ファイルに名前と換算を書いた。P2158、P2270、P2271 は記録に番号が無いので定義から外した |

## 断定できない

定義ファイルからは外しました。場所が決まっていないものは不明と書きます。

| 表 | データ番地 | 理由 |
| --- | --- | --- |
| Injector Flow Scaling | 不明 `10ed28` | 流量の定数が1か所に定まらなかった。`10ed28` の中身は 50.0 で、それらしい値だが証明できていない |
| MAF Compensation A/B (IAT) | 定義に無し | この ROM の定義は MAF Compensation (IAT) だけを参照している |
| Manifold Pressure Sensor Scaling | 不明 `11f860` | 倍率と切片の組が多数あり、1か所に定まらない。`11f860` の中身は 0.0 で、この ROM の換算ではない |
| Knock Correction Advance Max A | 不明 `119c44` | 共通定義 `32BITBASE.xml` は負荷16×回転18、`ZA1JF00C.xml` は負荷14×回転23。この ROM の 14×23 は Base Timing A/B と燃料の 3 枚だけ、16×18 は要求トルク A だけ。ノック上限の表はこの形では存在しない |
| Intake Cam Advance Angle Safe / Normal AVCS_、Exhaust Cam Retard Angle Safe / Normal AVCS_ | `121bf8`、`121e18`、`1221f8`、`122598` | 16×24 が 4 枚。4つのどれがどの表かは確定していない。混ぜ率 `fff81180` が 0.4 以上のとき `121bf8` と `1221f8` を一緒に読む。0.4 未満のとき `121e18` と `122598` を一緒に読む。軸は順に負荷 `121b58` 回転 `121b98`、負荷 `121d78` 回転 `121db8`、負荷 `122158` 回転 `122198`、負荷 `1224f8` 回転 `122538`。`fff81180` に 0.7 を書くのは、`fff8b26a` が 4 で `fff8c798` が 0 のとき、または `fff8c798` が 0 以外で `fff895ae` が 0 のとき。0.0 を書く箇所は `6f1c6`。計算途中の値を書く箇所は `6f046`。水温やアクセルの数値との比較には届いていない。0.7 の定数は `114a2c`、書き込み関数は `11a2c`（`6f17e`）。同じとき `114a30` の 0.0 を `fff81188` に書く。`fff8c798` を読むのは `544f4` で、0 以外なら 4 を返す。このバイトの書き込みは見つかっていない。`fff8b26a` を書くのは `6ec84`、`6ecb8`、`6f19a` |
| Total Injection Ratio Port Cold/Hot/Warm | `110afc`、`110bcc`、`110c9c` | `fff8a286` が 0 のとき、または `fff8a288` が 1 でないときは 3 枚とも使わない。`fff8a2e2` が 1 のとき `110afc`。`fff8a2e3` と `fff8a2e4` が両方 1 のとき `110bcc`。それ以外は `110c9c`。`fff892cc` が 55 未満なら `fff8a2e2` を 1、60 以上なら 0 にする。75 未満なら `fff8a2e4` を 0、80 以上なら 1 にする。その間は前回の値のまま。`fff892cc` が水温かどうかは断定できない。Cold / Hot / Warm のどれかは決まらない。呼び出しは `59836`、`5984c`、`59856`。`fff8a2de` が 1 のときも 3 枚とも使わない。55 と 60 の定数は `10c490`、`10c48c`。75 と 80 の定数は `10c4a0`、`10c49c`。この比較は `5972c`。`fff8a286` を 1 にする箇所は `59504`。同じ関数が `10c47c`（110.0）と `10c480`（30.0）を `fff892cc`、`fff892dc`、`fff89590`、`fff89614` と比べている。どの組み合わせで 1 になるかは未分解。`fff8a288` を直接書く箇所は見つかっていない |
| Tip-in Enrichment Compensation（18 点曲線） | 不明 `10efec`、`10f058`、`10f07c`、`10f09c` | 18 点の軸 `10efa4` と `10f010` は同じで、0, 0.98, 1.95, 3.91, 5.86, 7.81, 9.77, 11.7, 13.7, 15.6, 17.6, 19.5, 21.5, 23.4, 25.4, 27.3, 29.3, 31.3。2.56 倍すると 0, 2.5, 5, 10, 15, …, 80 に揃う。水温 -40〜110 ではない。`fff8b3ff` が 1 のとき `10efec`（高い側だけ 0.98 から 13.7）。1 でないとき `10f058`（全部 0）。同じ分岐が水温軸 `10cd78` の 16 点も読む。1 のとき `10f07c`、1 でないとき `10f09c`。どちらも 0。A と B のどちらがどちらかは決まらない。`fff8b3ff` を読む箇所は `4ef2c`、`4f712`、`4fbf8`、`5bc56`、`5bf80`、`64c82`、`6523c`。曲線を選ぶのは `6523c`。直接書く箇所は見つかっていない。記述子は `b5148`（`10efec`）、`b515c`（`10f058`）、`b5170`（`10f07c`）、`b5184`（`10f09c`）。参照関数は `11358` |
| Solenoid Control / Solenoid Duty | 不明 | 7×5 の未使用マップは `107f9c` の 1 枚だけ。2 つの名前を 1 枚に載せられない |
| Injector Flow Scaling BRZ | 不明 | Injector Flow Scaling と同じで、流量の定数が 1 か所に定まらない |
| CL to OL Transition with Delay (Accelerator) / (Base Pulse Width)、CL Delay | 不明 | この ROM では番地が 1 か所に定まっていない |
| A/F Learning #1 Limits、A/F Learning #1 Airflow Ranges A/B | 不明 | この ROM では番地が 1 か所に定まっていない |
| Hotstart Enrichment | 不明 | この ROM では番地が 1 か所に定まっていない |
| GDI Pressure Target A/B、GDI Pressure Multiplier A/B | 不明 | この ROM では番地が 1 か所に定まっていない |
| Intake Duty Correction A〜D、Exhaust Duty Correction A〜D | 不明 | この ROM では番地が 1 か所に定まっていない |
| AFR Sensor Heater Duty Cycle A/B、AFR Sensor Heater Protection | 不明 | この ROM では番地が 1 か所に定まっていない |
| Intake Temp Sensor Scaling | 不明 | この ROM では番地が 1 か所に定まっていない |
| 1D の定数（回転や負荷のしきい値） | 不明 | 同じ数値の候補が多く、番地を特定できない |
