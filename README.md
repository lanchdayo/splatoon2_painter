# **スプラトゥーン2の自動ドット打ち**
## **はじめに**
***
### **これなに？**
Splatoon2 のイラスト投稿の自動ドット打ちをAruduino UNO R3を使って書き込みます。Dockerコンテナ使うのでアレコレしなくても1発で書き込みファイル生成出来ます。

### **やりたいんだけど何すればいい？**

物理的に必要なものは以下のマイコンだけ買えばOK！

* Arduino用UNO R3コントロールボード
    * ↑ どれでもいいワケじゃなくてマイコンが必ずatmega16u2の買う。1800円くらい安い

### **でもさー難しいんでしょ？**

ネットで色々調べたらPyhton入れたり必要なモジュール入れたり色々面倒だったので、このリポジトリではそんな事しなくていいように最初から構築済みDockerコンテナを自動生成してその中で処理するようにしてるよ！知識ある人は一瞬で利用できると思うけどDockerって何？って人は他の方法でやるといいかも。（説明めんどい）

### **俺Macだけど動く？あとローカル汚したくないんだけど…**
Dockerコンテナで動くからWindowsだろうがMacだろうが関係なく実行できるよ！環境に優しいよ！


## わかった！やり方教えて！
***
### 必要な環境
* VSCode Remote Containerが動く環境
    * VSCODE
        * 適当にインストールすればOK
    * Docker Desktop
        * 適当にインストールすればOK
        * Windowsの人はWSL構築してからその中で実行すればいいよ
    * dfu-programmer
        * 適当にダウンロードして解凍しとく
### まずは環境準備！
上の`必要な環境`が揃ってる前提で話するね。

1. まずこのリポジトリをクローン(当たり前だけどVSCODEでやってね)
```
$ git clone https://github.com/lanchdayo/splatoon2_painter.git
```

2. クローンしたリポジトリへ移動
```
$ cd splatoon2_painter
```

3. 移動先をワーキングディレクトリにする
    * ↑ 新しいVSCODEが立ち上がるので今後はそこで作業する
```
$ code .
```

4. VSCODEから「Reopen in Container」を開く
    * 開いたらDockerコンテナが自動的に生成されます。

5. お疲れ様でした！もうこれで使えるよ！

## **よっしゃ！使い方**
***

### **PC側の作業**
1. 320x120のサイズで白黒画像を作る
2. 白黒画像のファイル名を「splatoonpattern.png」にしてワーキングディレクトリ直下に入れる
3. start.shを叩く
    * 実行権限無い時は「`$ chmod +x ./start.sh`」で付与してにょ
```
$ ./start.sh
```
4. マイコンをPCに刺す
    * ドライバも手動インストールする必要あると思うけど適当にいれてね
5. 「Joystick.hex」が出来上がるのでそれを解凍してた`dfu-programmer`フォルダ直下に入れて以下実行
```
> dfu-programmer.exe ATmega16U2 erase --force
> dfu-programmer.exe ATmega16U2 flash Joystick.hex
> dfu-programmer.exe ATmega16U2 reset
```
6. マイコンをPCから外す

### **SwitchSwitch側の作業**

1. スプラトゥーン2起動してポスト前にいく
2. 投稿画面になったら筆サイズを最小にして一番右上にセットしておく
3. マイコンをSwitchに接続する
4. すると自動ドット打ちが始まるので終わるまでらんちくんすごいなーって思ったらOK。


以上、おわり！

