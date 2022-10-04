# EMUZ80_MON
unimonの機能拡張を行いました。
合わせて、GRANT's BASIC版のZ80 BASIC Ver 4.7bも搭載してあります。

電脳伝説(@vintagechips)さんのオリジナルメモリマップでの動作確認と、
PIC18F47Q84でRAMサイズを12Kまで拡張したファームウエアで
動作させています。

RAM12K版のファームウェアは、メモリマップを以下の様に変更してあります。

ROM 0000H - BFFFH (48K)

RAM C000H - EFFFH (12K)

I/O F000H - FFFFH (4K)

(UART)

FF00H	; UART DATA REGISTOR

FF01H	; UART CONTROL REGISTOR

ＣＬＣを8個使い、メモリの読み書きのベクター割り込み処理はデータ転送の最小限の
処理に留めてあります。
アセンブラは使用していませんので、チューニングの余地はあります。
BASICのASCIIARTは、2.5MHZのZ80で1240秒程度でした。


PIC18F47Q84_firmwareのフォルダにRAM8KとRAM12K用のファームとヘキサファイル
があります。オリジナルメモリマップを使用すのであれば、RAM8Kを使用してください。

一応PIC18F47Q43_firmwareでRAM4K版も作成しましたが、手元にQ43が無いため、動作
確認は出来ていません。RAM4KをQ84で再構成して動作することは確認していますので、
多分大丈夫だと思います。

BASICは2000H番地から配置されています。Monitorから、Gコマンドでジャンプするか
#コマンドでローンチすることが出来ます。

BASICからは、MONITORコマンドでMonitorに戻ります。

モニターの操作方法ですが、？コマンドで以下のヘルプが出ます。
詳細は、MoniorDEbugCommand Document.txtを参照してください。

? : Command Help

D[addr] : Dump Memory [addr]

S[addr] : Set Memory [addr]

R[reg] : Set or Dump [reg]

G[addr][,stop addr] : Go and Stop specified address

L : Load Hex File

P[I|S] : Save Hex File (I:Intel, S:Motorola

#L|Number : Launch program

B[1|2[,BP addr]] : Set Break Point

BC[1|2] : Clear Break Point

T[addr][,steps|-1] : Trace command

TP[ON|OFF] : Trace Print Mode

TM[I|S] : Trace Option for CALL

