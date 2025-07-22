# PC6001RGB
PC-6001mk2 RGB converter

# これはなに？

PC-6001mk2/PC-6601 などの 15 色対応 RGB コネクタの信号をアナログ RGB の信号に変換します。
レート変換は行っていませんので、15KHz 対応のモニタを使うか別途スキャンコンバータなどをご使用ください。

# 使い方

`PC6001RGB.gp6` ファイルを Go Configutre Software Hub の GreenPAK designer から開きます。
GreenPAK SLG46826G (TSOP)のプロジェクトになっています。
SLG46826V (QFN)で使う場合には、ピンの番号が逆順に(6001 Red が Pin2)なります。

GreenPAK は小規模な FPGA のようなものです。
I2Cで書き換えができますので、
専用のプログラマーがなくても Arduino を使って書き込み出来ます。
(秋月でも売ってます)

入力ピン(DIN8から)
- Pin19: PC-6001 Red (6)
- Pin18: PC-6001 Green (7)
- Pin17: PC-6001 Blue (8)
- Pin16: PC-6001 輝度信号 (3)
- Pin15: PC-6001 Hsync (4)
- Pin10: GND (2)
  
出力ピン(DSUB HD15 へ)
- Pin1: VGA Red0 (1)
- Pin2: VGA Red1 (1)
- Pin3: VGA Green0 (2)
- Pin4: VGA Green1 (2)
- Pin5: VGA Blue0 (3)
- Pin6: VGA Blue1 (3)
- Pin8: VGA Hsync (13)

各色の 0 と 1 は以下のように接続します

```
Red0 -- R(470 ohm) --+
                     |
Red1 -- R(1K ohm) ---+---> VGA Red (1)
```

PC-6001 の VSYNC (5) と VGA の VSYNC (14) は直接接続します。
(あと GND も)

電源は RFコンバータ端子、または外部の 5V 電源を用いて VDD と VDD2 に供給してください。

# 回路について

変換回路については、[ゆみたろさんのRGBコンバータ](http://papicom.net/elec/rgb1/index.html)のロジックを参考にさせていただきました。
液晶ディスプレイに接続すると、短いスパイクが発生するのでダミーのゲートを入れてタイミング調整しました。

GreenPAK のゲート的には余裕があるので、CSYNC の合成回路なども入れることができると思います。
