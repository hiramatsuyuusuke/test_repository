# Python : for文の処理をインデクシングに置き換えて高速化する。
## 制作物PRです。Python、Githubを学習中です。

### 概要
ラベル領域の面積を取得するプログラムです。ラベルデータの面積を取得する関数は、存在しますが、Pythonのインデクシングを学習する目的で制作しました。インデクシングを用いた処理を学習することで、より複雑なfor文の処理を高速化できると思います。

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](/test.jpg)

```python
#BSDS300のラベルの面積を取得
#segmentsはラベル数( = 最大ラベル番号 + 1 )
area_BSDS300 = np.zeros(segments)
for i in range( 0, segments):# 0 ～ (segments-1)
    #ラベルの画素数(面積)を要素数とするラベルのリストを取得
    area_labels_list = BSDS300_label[ BSDS300_label == i ]
    #ラベルの面積（ =リストの要素数 )を取得
    area_BSDS300[ i ] = len( area_labels_list )
```
wwww

```python
#BSDS300のラベルの面積を取得
#segmentsはラベル数( = 最大ラベル番号 + 1 )
area_BSDS300 = np.zeros(segments)
for i in range( 0, __segments):# 0 ～ (segments-1)
    for y in range( 0, __height ):# 0 ～ (height-1)
        for x in range( 0, __width ):# 0 ～ (width-1)
            if BSDS300_label[ y, x ] == i:
                area_BSDS300[ i ] += 1
```