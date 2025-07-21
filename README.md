# PC6001RGB
PC-6001mk2 RGB converter

# これはなに？

PC-6001mk2/PC-6601 などの 15 色対応 RGB コネクタの信号をアナログ RGB の信号に変換します。
レート変換は行っていませんので、15HKz 対応のモニタを使うか別途スキャンコンバータなどをご使用ください。

# 使い方

GreenPAK SLG46826G (TSOP)のプロジェクトになっています。
SLG46826V (QFN)で使う場合には、ピンの番号が逆になります。

入力ピン
- Pin19: PC-6001 Red
- Pin18: PC-6001 Green
- Pin17: PC-6001 Blue
- Pin16: PC-6001 輝度信号
- Pin15: PC-6001 Hsync
- Pin11: GND
  
出力ピン

- Pin1: VGA Red0
- Pin2: VGA Red1
- Pin3: VGA Green0
- Pin4: VGA Green1
- Pin5: VGA Blue0
- Pin6: VGA Blue1
- Pin8: VGA Hsync

各色の 0 と 1 は以下のように接続します

```
Red0 -- R(470 ohm) --+
                     |
Red1 -- R(1K ohm) ---+---> VGA Red
```

PC-6001 の VSYNC と VGA の VSYNC は直接接続します。
(あと GND も)

電源は RFコンバータ端子、または外部の 5V 電源を用いて VDD と VDD2 に供給してください。

#　回路について

変換回路については、[ゆみたろさんのRGBコンバータ](http://papicom.net/elec/rgb1/index.html)のロジックを参考にさせていただきました。
液晶ディスプレイに接続すると、短いスパイクが発生するのでダミーのゲートを入れてタイミング調整しました。

GreekPAK のゲート的には余裕があるので、CSYNC の合成回路なども入れることができると思います。

