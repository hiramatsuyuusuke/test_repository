# Python : for文の処理をインデクシングに置き換えて高速化する。
## 制作物PRです．PythonとGithubを学習中です。

### 概要

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](/test.jpg)

```python
#BSDS300のラベルの面積を取得
#__segmentsはラベル数( = 最大ラベル番号 + 1 )
__area_BSDS300 = np.zeros(__segments)
for __i in range( 0, __segments):# 0 ～ (__segments-1)
    #ラベルの画素数(面積)を要素数とするラベルのリストを取得
    #__mem_list1[__im_count][ y座標, x座標 ]
    __area_labels_list = __BSDS300_label[ __BSDS300_label == __i ]
    #ラベルの面積（ =リストの要素数 )を取得
    __area_BSDS300[ __i ] = len( __area_labels_list )
```
wwww

```python
#BSDS300のラベルの面積を取得
#__segmentsはラベル数( = 最大ラベル番号 + 1 )
__area_BSDS300 = np.zeros(__segments)
for __i in range( 0, __segments):# 0 ～ (__segments-1)
    for __y in range( 0, __height ):# 0 ～ (__height-1)
        for __x in range( 0, __width ):# 0 ～ (__width-1)
            if __BSDS300_label[ __y, __x ] == __i:
                __area_BSDS300[ __i ] += 1
```