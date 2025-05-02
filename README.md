# BPM-Syncer
bpm同期オブジェクトのエイリアス集

## デモ


https://github.com/user-attachments/assets/c7c1ab0e-ebf7-45f9-b1e5-94516c46027b



## 概要
基本図形とテキストを任意のBPMに同期させる．

### bar
- 4つ打ちのプログレスバー
- BPM同期スクリプトが必要

### blinker
- 図形が明滅する
- スクリプト制御で編集

**記述例**
```lua
--プロパティ
bpm=60
x_dist=0
y_dist=0

shape="四角形"
color=0xffffff
size=50

b_1=bpm/15
b_4=bpm/60
b_16=bpm/240

--処理
obj.load("figure",shape,color,size,4000)
if(math.floor(b_4*obj.time)%2 == 0) then
  obj.draw(0*x_dist,0*y_dist)
else
  obj.load("figure",shape,color,size,0)
  obj.draw(0*x_dist,0*y_dist)
end
```

### counter
- 小節数カウンタと1/4 & 1/16のビートループ
- ファイル末尾のclrはオブジェクトの位置（center, left, right）
- テキストで編集

**記述例**
```lua
<?
  --プロパティ
  bpm=60
  a=0
  b_4=bpm/60
  ot=b_4*obj.time+a
  
  --処理
  mes(string.format("%01d",ot%4))
?>
``` 

### flow
- 図形が左から右に流れる
- スクリプト制御で編集

**記述例**
```lua
--プロパティ
bpm=60
x_dist=100
y_dist=0

shape="四角形"
color=0xffffff
size=50

b_1=bpm/15
b_4=bpm/60
b_16=bpm/240

--処理
obj.load("figure",shape,color,size,4000)
if(math.floor(b_4*obj.time)%4 == 0) then
  obj.draw(-1.5*x_dist,0*y_dist)
elseif(math.floor(b_4*obj.time)%4 == 1) then
  obj.draw(-0.5*x_dist,0*y_dist)
elseif(math.floor(b_4*obj.time)%4 == 2) then
  obj.draw(0.5*x_dist,0*y_dist)
elseif(math.floor(b_4*obj.time)%4 == 3) then
  obj.draw(1.5*x_dist,0*y_dist)
end
```

## インストール
エイリアスの配置は以下の通りに行う．
 ```
AviUtl
　├ exedit.auf
　└ @bpm_sync
    └ bar.exa
    └ blinker.exa
    └ counter_c.exa
    └ counter_l.exa
    └ counter_r.exa
    └ flow.exa
```

**bar**
の利用には以下の2つのスクリプトを導入する．

**BPM同期効果処理**

https://commons.nicovideo.jp/works/sm38516538

**角丸四角形(hksy)**

https://purinka.work/download/hksy.html
