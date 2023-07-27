# Python : for文の処理をインデクシングに置き換えて高速化する。
## 制作物PRです。Python、Githubを学習中です。

### 概要
２つのラベル画像を比較して、重なるラベル領域の面積を取得するプログラムです。プログラムの制作を通じて、Pythonのインデクシングを学習しました。インデクシングを用いた処理を学習することで、より複雑なfor文の処理を高速化できるようになると思います。

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](/fig.1.jpg)

インデクシングを用いたプログラムです。
```python
#重なる部分の画素数を取得
#画素数取得用配列
__seg_AND = np.zeros( (__segments, __max_label_cell_net + 1) )
#生体モデルのラベルの要素番号
for __ii in range( 0, __max_label_cell_net + 1):
    #__mem_list1[__im_count]のラベル番号と同じ位置にある__BSDS300_labelのラベル番号のリストを取得
    #__mem_list1[__im_count]と__BSDS300_labelは同じサイズの2次元配列
    __over_laps_list = __BSDS300_label[ __mem_list1[__im_count] == __ii ]
    #同じ位置にあるラベル番号を参照して、画素数をカウントする．
    for __i, __value in enumerate( __over_laps_list ):
        __ivalue = int( __value )
        __seg_AND[ __ivalue, __ii ] += 1 #重なる部分の画素数を取得
```

上記のインデクシング部分をfor文で書いたプログラムです

```python
#重なる部分の画素数を取得
#画素数取得用配列
__seg_AND = np.zeros( (__segments, __max_label_cell_net + 1) )
#BSDS300のラベルの要素番号
for __i in range( 0, __segments):
    #生体モデルのラベルの要素番号
    for __ii in range( 0, __max_label_cell_net + 1):
        #画像の範囲内を探索
        for __y in range( 0, __height ):# 0 ～ (__height-1)
            for __x in range( 0, __width ):# 0 ～ (__width-1)
                #互いのラベルの座標が同じになる場合
                if (__BSDS300_label[ __y, __x ] == __i and
                    __mem_list1[__im_count][ __y, __x ] == __ii):
                    #重なる部分の画素数を取得
                    __seg_AND[ __i, __ii ] += 1
```