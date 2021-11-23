[TOC]

# DataScience_AI

Materials for lecture 2021 MU

#　「環境データサイエンスとAI」

<br>

本テキストは、pythonを用いてコードを作成し、大量のデータから有意義な情報を引き出す統計計算や機械学習の基礎を学ぶことを目的としています。以下の教科書等は、全般に関する知識として、色々ある中で個人的に役に立つと思うものをあげています。

1) Bill Lubanovic, 入門 Python 3, 斎藤康毅(監修),長尾高弘(訳), オライリージャパン, 2015（第2版2021）
2) ディジタル画像処理編集委員会, ディジタル画像処理（改訂第2版）, 画像情報教育振興協会, 2020
3) 石井健一郎他, わかりやすいパターン認識（第2版）, オーム社, 2019
4) 斎藤 康毅, ゼロから作るDeep Learning―Pythonで学ぶディープラーニングの理論と実装, オライリージャパン, 2016
5) David Foster, 松田 晃一他,　生成 Deep Learning ―絵を描き 物語や音楽を作り ゲームをプレイする, オライリージャパン, 2020
6) Pythonプログラミング入門, 東京大学 数理・情報教育研究センター (CC BY-NC-ND 4.0), https://utokyo-ipp.github.io/index.html

<br>

<br>





## １　Pythonのインストールなど

<br>

### １ー１　標準python

<br>

理科系ではMatLabやRなどを使用したことがあるかもしれませんし、JavaやCの言語を使える方もいるでしょう。Pythonはそれに比べて、汎用性の高いライブラリーが多く開発され、科学分析において多くの人が使うようになりました。科学計算に必要なライブラリーが備わってきたこと、さらには読みやすく、書きやすく設計された言語であることが人気の一つと言われます。また、Githubなどの共同開発のサイトなどの活用により、コードが何度も読まれ、改訂されるたびに、さらに分かりやすくなるといわれます。なぜpythonかといえば、そういうコミュニティーがあり、常に良い言語を話そうとする人たちが、有益な情報をネットに上げてくれているということも上げておくべきでしょう。

とは言え、言語ですからある程度覚えないと話せません。しかし、苦しい時期はおそらく思っているより短いと思います。

Python3をインストールします。このテキスト執筆時点で、最新のバージョンは　3.10ということですので、そのうち4が出てきてまたアタフタする様なことになりそうですが、とりあえず6ヶ月くらい前にレリースされた安定バージョンをインストールするのがいいように思います。理由は、科学技術計算や機械学習で利用するパッケージの対応を遅れている可能性があるからです。ちなみに私はM1 Macを使っていますが、Pythonは3.8.２です。インストールの際、scikit-learn, scikit-image, tensorflowという、パターン認識、機械学習、画像処理に必要なものが問題なく動くバージョンということで選択しました。

あまり悩むことなく標準のパイソンをhttps://www.python.org/ からインストールしてみましょう。
必要なパッケージはその都度インストールしますが、この講義では使うのは以下の通りです。
numpy, pandas, scikit-learn, scikit-image, opencv, matplotlib, tqdm, tensorflow, openpyxl, pillow, jupyter, jupyterlab, ipython, seaborn, hdf5, geopanda, 

<img src="https://www.python.org/static/img/python-logo@2x.png" height="50" >
<img src="https://scikit-learn.org/stable/_static/scikit-learn-logo-small.png" height="50" >
<img src="https://scikit-image.org/_static/img/logo.png" height="50" >

ハードディスクに余裕があって、いろいろな科学技術計算のパッケージがプレインストールされる方がいい場合は、anaconda pythonをインストールしてください。

<br>

### １ー２　クラウドサービスの利用

<br>

Colaboratory（略称: Colab）は、ブラウザから Python を記述、実行できるサービスです。Googleの提供するサービスなので利用する人はGoogleアカウントを取得してください。計算時間とか、ファイルの保存期間とかに制限がありますが、GPUも提供されていて深層学習も実行可能なサービスです。

https://colab.research.google.com/notebooks/welcome.ipynb?hl=ja#scrollTo=5fCEDCU_qrC0



<br>

## ２　電卓を作る

<br>

### ２ー１　Pythonで扱うデータ

<br>

取り扱うデータ型は以下の通りです。
+ ブール値（Boolean)：TrueとかFalseという値
+ 整数（integer):小数点以下がない数
+ 浮動小数点数（float):少数以下を含む数、指数表現で表される数
+ 文字列（character):文字の並びで表されるもの

<br>

### ２ー２　演算子

<br>

四則演算で必須なものは次の通りです。
+ `+`：加算
+ `-`：減算
+ `*`：乗算
+ `**`：指数（べき乗）
+ `/`：浮動小数点数の割り算
+ `//`：整数の除算（商切り捨て）
+ `%`：剰余

<br>

### ２ー３　比較演算子

<br>

主な比較演算子は次の通りです。

+ `a < b`：a は b より小さい
+ `a <= b`：a は b と等しいか小さい
+ `a > b`：a は b より大きい
+ `a >= b`：a は b と等しいか大きい
+ `a == b`：a と b は等しい
+ `a != b`：a と b は等しくない

<br>

上の演算子を使って割り算の関数を作ります。入力は2つ （x と y)　商と余りを返すことします。

```python
>>> a=5.0  # .0 をつけて浮動小数点数と定義する
>>> b=23.0
>>> b/a　　#結果を浮動小数点数で表示
4.6
>>> b//a　#商は
4.0
>>> b			#余は
3.0
>>> def warizan(x,y):  # 商と余を同時に計算する自分の関数
...     sho=x//y
...     amari=x%y
...     return sho,amari
...
>>> s,a = warizan(34,6)
>>> print('sho',  s, ' amari ', a)
6.0, 4.0
```

<br>

### ２ー４　練習

<br>

１）9時00分00秒から3333秒後は、何時何分何秒ですか？

２）1)を計算する関数を作りなさい。

<br>

## ３　データの型

<br>

電卓の時は、１つの入力に対して1つの出力があった。ここで取り上げるデータは複数あるいはもっと多元的な複雑なデータである。まずは一次元の要素の並びを考える。

前出の文字列がどう扱われるかを説明しましょう。’university' という文字列は、数値と違って、アルファベットの列と捉えられ、単語全体では10個の文字からなると認識されます。整数のインデックスで先頭から順番に各要素を取り出すことができ、3番目は'i’の文字というように、一つのシークエンスとして扱えます。pythonでは要素の1つ目を０に定義するので、3番目は0,1,2の２となることに注意しましょう。

```python
>>> word='university'
>>> print(len(word), word[2])
(10, 'i')
```

<br>

これと同じように、リストとタプル型のシーケンス構造が提供されています。リストは変更のきくシークエンス（並び替えが可能）で、タプルは辞書向きで、書き換えることができません。前者をミュータブル(mutable)、後者をいミュータブル(immutable)といいます。

<br>

### ３ー１　リスト型

<br>

リストは０個以上の要素をカンマで区切り角かっこ`[　]`で囲んだものです。リストの中の要素は、先頭から順番に指定して取り出すこと、範囲を決めて複数取り出すこと、など色々設定可能です。

```python
>>> subjects=['physics', 'chemistry', 'biology', 'history']
>>> score=[88,75,87,92]
>>> subjects[2],score[2]
('biology', 87)
>>> subjects[0:2]
['physics', 'chemistry']
>>> subjects[::2]
['physics', 'biology']
>>> subjects[::-1]
['history', 'biology', 'chemistry', 'physics']
```

<br>

`list( )`関数は他のデータ型をリストに変換します。例えば、文字列の場合

```python
>>> list('university')
['u', 'n', 'i', 'v', 'e', 'r', 's', 'i', 't', 'y']
>>> word='university'
>>> word.split('r')
['unive', 'sity']
```

<br>

### ３ー２　セット型

<br>

ちょっと複雑になりますが、この機能を使ってリストの中の要素を取り出すことができます。それにはリストを`set( )`関数に入れるか、リストを`{  }`で囲みます。データが書き込まれるメモリの位置によて順番が変わるので、いつも同じ順番とは限らないので、順番を気にするときは注意が必要です。

```python
>>> word='university students'
>>> list(word) # 単語をアルファベットに分解してリストの要素にする
['u', 'n', 'i', 'v', 'e', 'r', 's', 'i', 't', 'y', ' ', 's', 't', 'u', 'd', 'e', 'n', 't', 's']
>>> lw=list(word)　
>>> set(lw)　　# 使われている文字の要素を書き出す。元々のデータの並びの順番とどうか？
set([' ', 'e', 'd', 'i', 'n', 's', 'r', 'u', 't', 'v', 'y'])
>>> sorted(set(lw),key=lw.index)　# 使われている文字の要素をリストの順番に書き出す
['u', 'n', 'i', 'v', 'e', 'r', 's', 't', 'y', ' ', 'd']
#　同じ事を{ }を使うと
>>> wordset={'u', 'n', 'i', 'v', 'e', 'r', 's', 'i', 't', 'y', ' ', 's', 't', 'u', 'd', 'e', 'n', 't'}
>>> wordset
>>> {'n', 'd', 'r', 'e', 'u', 's', ' ', 't', 'y', 'i', 'v'}
```

<br>

セット型のデータは集合演算につかいます。

+ `|`：和集合（ユニオン）
+ ` &`：積集合（インターセクション）
+ `-`：差集合
+ `^`：対称差集合
+ `<=`：部分集合か判定
+ ` >=`：上位集合か判定

```python
>>> a=set(list('university'));b=set(list('student'))
>>> a | b
{'n', 'r', 'd', 'e', 'u', 's', 't', 'y', 'i', 'v'}
>>> a & b
{'n', 'e', 's', 'u', 't'}
>>> a - b
{'i', 'r', 'v', 'y'}
>>> a ^ b
{'r', 'd', 'y', 'i', 'v'}
```

<br>

### ３ー３　タプル型

<br>

辞書などの作成すると変更しないようなデータのために準備されています。タプルは`(  )`で囲んで作成します。
 例えば京都の地理的位置や、学生の科目別成績など、**複数の要素から構成される独立したデータ**をあらわすときはタプルを使用します。タプルは`[ ] `で引数を入れることで個別に取り出すことができます。またタプルはリスト型に直すことで値の変更が可能です。

```python
>>> kyoto=35.02139,135.75556 # 例えば 京都の市役所
>>> kyoto
(35.02139, 135.75556)　　　# （　）括りになりました
>>> osaka=34.68639,135.52　# 大阪の市役所
>>> kyoto == osaka　　# 同じ位置かどうかの判定
False
>>> print('京都の緯度は',kyoto[0],'経度は',kyoto[1]) # 個別に値を取り出す
京都の緯度は 35.02139 経度は 135.75556
>>> list(kyoto) # 型の変換
[35.02139, 135.75556]
>>> yakusho_dic={'大阪':osaka,'京都':kyoto}
{'大阪':(34.68639, 135.52), '京都': (35.02139, 135.75556)}
```

<br>

### ３ー４	練習

<br>

１）近畿地区の国立大学の名称と緯度・経度の辞書を作成しなさい。

| Name                          | Latitude  | Longitude  |
| :---------------------------- | --------- | ---------- |
| Kyoto University              | 35.026244 | 135.780822 |
| Kyoto University of Education | 34.950215 | 135.773187 |
| Kyoto Institute of Technology | 35.049664 | 135.782046 |



<br>

## ４　データの特徴

<br>

### ４ー１　イテラブル、イテレータ

<br>

イテラブル(iterable)とか、イテレータ(iterator)とは『反復可能な』や『繰り返し可能な』という意味です。この要素を使いこなせるようになると一気にやれることが増えてきます。

パソコンは「繰り返し処理をやらせるには最適」と考える人は少なくないようですが、その繰り返しの処理を考えてみましょう。

パソコンにログインしていつものように作業をします。そのときあなたのディレクトリーはどこですか？30年前であれば、この質問全員正解だったでしょうが、みなさんはどうですか。GUI（graphic user interface)のおかげで、知る必要のない世代の皆さんは質問の意味もわからないかもしれません。

```python
>>> import os
>>> os.getcwd()　# get current working directory
'/Users/yourname'
>>> os.listdir()  # list directory
['Music','Pictures', 'Applications',　'Desktop', 'Documents']
```

<br>

上に示したコードの `os.listdir()` は 今自分が利用しているディレクトリをリスト型で出力してます。デスクトップの一つ下の階層です。 list形式のデータはイテラブルなので、その要素を順番に取り出すことができ、繰り返し処理につかえます。例として、ディレクトリの中にいくつファイルがあるか順番に出力してみます。

```python
>>> My_dirs=os.listdir()
>>> for my_dir in My_dirs:
>>>   number_of_files=len(os.listdir(my_dir))
>>>		print('ディレクトリ'+my_dir+'のファイル数は'+str(number_of_files))
ディレクトリMusicのファイル数は4
ディレクトリPicturesのファイル数は6
ディレクトリApplicationsのファイル数は1
ディレクトリDesktopのファイル数は23
ディレクトリDocumentsのファイル数は8
```

<br>

上の簡単な `for ~ in` の簡単なループは、My_dirsの中のリストからひとつづつディレクトリー名をmy_dirに呼び出し、各ディレクトリにあるファイル数を出力するという意味になります。

上はリスト型データの例ですが、数字の場合も`range()`という便利なイテレーターが準備されています。

```python
>>> list(range(10)) # range(0,10,1) と同じ
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1,10,3)
[1, 4, 7]
```

<br>

もう少し複雑な繰り返し分を考えてみます。例えば複数のリストがあり、それらから同時に一つずつ取り出すことを考えます。複数のリストから一つづつまとめて取り出す`zip( )` , 取り出した順に序数をつける`enumerate ( )`を使います。

```python
>>> prefecture=['滋賀','京都','大阪','兵庫','奈良','和歌山']
>>> city=['大津市','京都市','大阪市','神戸市','奈良市','和歌山市']
>>> tree=['モミジ','北山スギ','イチョウ','クスノキ','スギ','ウバメガシ']

>>> for i,p in enumerate(zip(prefecture,city,tree)):
...     print(str(i+1)+'番'+' 都道府県名 '+p[0]+' 県庁所在地 '+p[1]+' 県の木 '+p[2])
```

<br>

### ４ー２　条件文　if〜else

<br>

例えば解析用に作ったデータの中にいわゆる不可視ファイル（実際に存在はするのだけど画面上には表示されないシステムが使うファイル）があります。ところが、プログラムでデータを読み込むとファイルが全部読まれてしまいします。それを避けてファイルを読むには次のように処理します。

```python
>>> My_jpg_list=[]
>>> My_list=os.listdir('Gaszou')
>>> for filename in My_list:
...		if filename.endswith('.jpg')
...			My_jpg_list.append(filename)
...		else 
...			print(filename+'is not a jpg file !')
>>> My_jpg_list
```

<br>

上の例では、Gazouのファイルにあるファイルのうち、拡張子が.jpgでないものを無視してjpegファイルのみのリストをMy_jpg_listに格納します。複数の用件を同時に満足する、あるいはどちらかを満足するという条件が必要な場合は、`and` あるいは`or` で複数の条件を併記します。

```python
>>> testdata=[1,2,3,4,5,6,7,8,9,0]
>>> for i in testdata:
...   if i > 4 and i<7:
...       print(i)
5
6
```

<br>

以上のように、イテレータと条件文はプログラムの中で、繰り返す・判断するという二つの重要なプロセスを実現します。

<br>

### ４ー３　内包表記

<br>

繰り返しと条件文は数行のプログラムで書けるものですが、内包的表現を使うと１行で書くことができます。

例えば ある特定のディレクトリの中から特定の拡張子のファイルだけを読み出したい場合、そのリストを作るには次のようにします。

```python
[fl for fl in os.listdir('my_target_dir') if fl.endswith('.xlsx')]  ＃　例えばエクセルのファイル
```

<br>

また、不可視ファイルを除いたリストが欲しい場合（MacOSの場合は .filenameの形式で最初にドットがつきます）には次のようにします。

```python
[fl for fl in os.listdir('my_target_dir') if fl.startswith('.')]  ＃　例えば不可視ファイル
```

<br>

### ４ー４　ジェネレーター

<br>

これまで説明したイテレータは一度に全てのデータをメモリに読み込んでしまいます。パソコンのディレクトリの場合は問題なくても、たとえば何千枚もの画像を読み込もうとするとメモリはパンクしてしまいます。ジェネレーターは、そのような大きなイテラブルなオブジェクトに対して、指定した大きさで逐次読み出しをするための仕組みです。画像を扱う深層学習では普通に使うツールですので理解しておきましょう。次の例は、1から100の範囲、増分３の等差数列から7で割り切れる数字を順に出力する例です。２−４の関数では`return`で戻り値を得たのに対して、ここではyield であることに注意です。

```python
>>> def generator(input):
...     for x in input:
...         if x%7==0:  #### ７で割り切れたらその都度支出力
...             yield x
>>> input=list(range(1,100,3))
>>> mygen=generator(input)
>>> next(mygen)
```

<br>

### ４ー５　練習

１）testdata=[1,2,3,4,5,6,7,8,9,0]　からイテレータと条件文をつかって3,5,6,9 を出力しなさい。

２）2022年元旦から12月末まで木曜日の日付を出力しなさい。

<br>



## ５　汎用モジュールとライブラリー

<br>

pythonは、オブジェクト指向型の言語と言われます。さまざまな目的を達成するために必要なひとつひとつの要素を**オブジェクト**といいます。一番上位にある目的のために特別な関数や値をまとめたもの**モジュール**、その一つ下の括りを**ライブラリー**と呼んでいます。

<br>

### ５ー１　数値演算

<br>

> NumPy is an open source project aiming to enable numerical computing with Python. It was created in 2005, building on the early work of the Numeric and Numarray libraries. NumPy will always be 100% open source software, free for all to use and released under the liberal terms of the [modified BSD license](https://github.com/numpy/numpy/blob/main/LICENSE.txt). (From HP)

<br>

**NumPy** (https://numpy.org/) は数値計算を効率的に行うための**拡張モジュール**で、特に多次元配列（例えばベクトルや行列などを表現できる）を扱うことができ、その操作のための広範かつ高速で動作する**数学関数ライブラリー**を提供しています。　NumPy を使うには、まずnumpy を省略形npでプログラムに読み込むと、numpyに含まれているいるさまざまな関数や処理を`np.関数`という書式で呼び出すことができる。

<br>

#### ５ー１ー１　多次元配列

<br>

リストと配列の違いを理解しましょう。リストはイテラブルですが計算はできません。リストで作った配列を`np.array( )`に代入すると、個々の数値に対して同じ演算をすることができるようになります。またリストの中にリストがある入れ子の場合、`np.array( )`に渡すと、多次元の配列となります。下の例では５個の要素からなるリストを３倍の長さにして、それを３x５の行列に書き換えます。最後にそれを`np.log()`関数で対数変換します。

```python
>>> import numpy as np
>>> a_list=[1,2,3,4,5]
>>> a_list*3
[1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 1, 2, 3, 4, 5]
>>> a_array=np.array(a_list)
>>> a_array*5
array([ 5, 10, 15, 20, 25])
>>> x=np.array(a_list*3).reshape(5,3)
>>> x
array([[1, 2, 3],
       [4, 5, 1],
       [2, 3, 4],
       [5, 1, 2],
       [3, 4, 5]])
>>> 3*np.log(x)
array([[0.        , 2.07944154, 3.29583687],
       [4.15888308, 4.82831374, 0.        ],
       [2.07944154, 3.29583687, 4.15888308],
       [4.82831374, 0.        , 2.07944154],
       [3.29583687, 4.15888308, 4.82831374]])
>>> x=3*np.log(x)
```

<br>

配列要素の情報を知る関数は次のとおりです。

| 属性      | 意味                                          |
| :-------- | :-------------------------------------------- |
| `a.dtype` | 配列 `a` の要素型                             |
| `a.shape` | 配列 `a` の形（各次元の長さのタプル）         |
| `a.ndim`  | 配列 `a` の次元数（`len(a.shape)` と等しい）  |
| `a.size`  | 配列 `a` の要素数（`a.shape` の総乗と等しい） |
| `a.flat`  | 配列 `a` の1次元表現（`a.ravel()` と等しい）  |
| `a.T`     | 配列 `a` を転置した配列（`a` と要素を共有）   |

<br>

上で作ったxでどのように出力されるか確認しましょう。

```python
>>>print(x.dtype)
float64
>>>print(x.shape)
(5, 3)
>>>print(x.size)
15
>>>print(x.T)
[[0.         4.15888308 2.07944154 4.82831374 3.29583687]
 [2.07944154 4.82831374 3.29583687 0.         4.15888308]
 [3.29583687 0.         4.15888308 2.07944154 4.82831374]]
```

<br>

#### ５ー１ー２　配列を作る関数

<br>

以下の関数で等差数列をはじめとしてn次元の様々な数列を作ることをができます。

| 関数                          | 説明                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| `np.arange(start, stop)`      | start, stop あるいは stop のみ、stepは整数１                 |
| `np.arange(start,stop,step)`  | start, stop, step: `range`と異なり、浮動小数点数`float`を引数に指定可能。 |
| `np.linspace(start,stop,num)` | numは要素数。それらに応じた間隔（公差）が自動的に算出される。 |
| `np.zeros(x)`                 | xが6のとき一次元６要素の０の配列、(2,3)のとき2x3の２次元６要素の0の配列 |
| `np.ones(x)`                  | xが6のとき一次元６要素の1の配列、(2,3)のとき2x3の２次元６要素の1の配列 |
| `np.random.rand(x)`           | xが6のとき一次元６要素の乱数、2,3のとき2x3の２次元６要素の乱数（0〜1の範囲） |

<br>

#### ５ー１ー３　配列のインデックス、スライスによるアクセス

<br>

次の例では、5x5の乱数からなる２次元配列を作ります。個々の値は行と列に対応するインデックスを持っていて、その値を取り出したり、加工したりすることが可能です。たとえば、配列matのp行、q列の値は、`mat[p,q]`です。また、複数の行や列を取り出してスライス配列として扱うことができます。例えば、行はp、列はqの前後合わせた３つのスライス配列は`mat[p, q-1:q+1] `で与えられます。

```python
>>> mat=np.random.rand(5,5)
>>> mat
array([[0.93987159, 0.755175  , 0.25051673, 0.91663363, 0.6494    ],
       [0.50657243, 0.17434289, 0.13504302, 0.54144137, 0.22875137],
       [0.09517721, 0.43037945, 0.08206899, 0.54896378, 0.33087475],
       [0.17262683, 0.51725863, 0.83124545, 0.70180956, 0.35399325],
       [0.30247671, 0.52517184, 0.92602194, 0.01585037, 0.26942446]])
>>> mat[1:3,2:4]
array([[0.13504302, 0.54144137],
       [0.08206899, 0.54896378]])
>>> mat[1:3,2:4]=0
>>> mat
array([[0.93987159, 0.755175  , 0.25051673, 0.91663363, 0.6494    ],
       [0.50657243, 0.17434289, 0.        , 0.        , 0.22875137],
       [0.09517721, 0.43037945, 0.        , 0.        , 0.33087475],
       [0.17262683, 0.51725863, 0.83124545, 0.70180956, 0.35399325],
       [0.30247671, 0.52517184, 0.92602194, 0.01585037, 0.26942446]])
```

<br>

#### ５ー１ー４　配列の統計量

<br>

NumPy配列に組み込まれている統計量は以下の通りです。この関するの( )内に軸を設定することで、行あるいは列でそれぞれの統計量を計算することができます。たとえば、上のmatの例で縦方向の行で集計する場合は`a.sum(axis=0)`横方向の列で集計する場合は、`a.sum(axis=1)` となります。

| 属性 またはコマンド            | 意味                                |
| ------------------------------ | ----------------------------------- |
| `a.sum()` or `np.sum(a)`       | 配列`a`の合計                       |
| `a.mean()` or `np.mean(a)`     | 配列`a`の平均                       |
| `a.var() `or `np.var(a)`       | 配列`a`の分散                       |
| `a.std()` or `np.std(a)`       | 配列`a`の標準偏差                   |
| `a.argmax()` or `np.argmax(a)` | 配列`a`の最大値を与えるインデックス |
| `a.argmin()` or `np.argmin(a)` | 配列`a`の最小値を与えるインデックス |

<br>

### ５ー２　作図

<br>

> Matplotlib is the brainchild of John Hunter (1968-2012), who, along with its many contributors, have put an immeasurable amount of time and effort into producing a piece of software utilized by thousands of scientists worldwide.　(From HP)

<br>

科学技術計算においてNumPyと同様に、グラフ表示に必要な**Matplotlib** ライブラリー ( https://matplotlib.org )は欠かせません。棒グラフ、折れ線グラフ、散布図はもとより、アニメーションや動画などの可視化ができます。覚えることも多いですが、パラメータの意味を習得することで、様々なグラフやデータを重ね合わせたり、合体させたりできるのも特徴です。例としてxの範囲-3から3の $$y＝x^3$$ のグラフを描いてみます。

```python
>>> import numpy as np
>>> x= np.arange(-3,3,0.1)
>>> y=x**3

>>> import matplotlib.pyplot as plt
>>> %matplotlib inline
>>> plt.plot(x,y,label="y=x^3")
>>> plt.legend()
>>> plt.xlabel('x')
>>> plt.ylabel('y')
>>> plt.show()
```

<img src="./img/yx3.png" alt="Alt text" style="zoom:30%;" />



<br>複数のグラフを作ることも容易ですが、文法が少し変わるので注意が必要です。y=xから1/3乗、1/2乗、1乗、2乗、3乗、5乗の6つ　を２行３列に書くには

```python
>>> fig, axes = plt.subplots(ncols=3,nrows=2, figsize=(12,8))
>>> power=[1/3,1/2,1,2,3,5]
>>> for i,p in enumerate(power):
...     c,r=divmod(i,3)
...     axes[c,r].plot(x,x**i,label="power of"+str(power[i]) )
...     axes[c,r].legend()
...     axes[c,r].set_xlabel('x')
...     axes[c,r].set_ylabel('y')
>>> plt.show()
```

<img src="./img/yxpowers.png" style="zoom:50%;" />

<br>

 ### ５ー３　表計算

<br>

> When working with tabular data, such as data stored in spreadsheets or databases, pandas is the right tool for you. pandas will help you to explore, clean, and process your data. In pandas, a data table is called a [`DataFrame`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html#pandas.DataFrame). (From HP)

<br>

Pandas (https://pandas.pydata.org/) ライブラリーはエクセルで扱うような表形式のデータを扱うツールです。外部ソフトで作成したtext, csv, JSON, Excelなどはもちろん、配列を表形式DataFrame() に読み込むことで、用意された豊富な統計処理や表計算を実行できます。またこのライブラリーにはmatplotlibと連携したグラフ表示機能も組み込まれています。

<br>

３ー４で作成したdictデータをpandasに読み込んでみましょう。さらに、住所、各大学の学生数、創立年の情報を加えて表にします。

```python
>>> univ_dic={'Kyoto University':(35.026244,135.780822),'Kyoto University of Education':(34.950215,135.773187),'Kyoto Institute of Technology':(35.049664,135.782046)}
>>>
>>> import pandas as pd
>>> df=pd.DataFrame(univ_dic, index=('latitude','longitude'))
>>> dfn=df.T
>>> dfn['address']=['京都府京都市左京区吉田本町','京都府京都市伏見区深草藤森町1','京都府京都市左京区松ヶ崎橋上町1']
>>> dfn['students']=['12,958','1,332','2,656']
>>> dfn['teachers']=['3,441','110','281']
>>> dfn
```

| University                    |  Latitude |  longitude |                         Address | Students | Teachers |
| :---------------------------- | --------: | ---------: | ------------------------------: | -------: | -------- |
| Kyoto University              | 35.026244 | 135.780822 |      京都府京都市左京区吉田本町 |   12,958 | 3,441    |
| Kyoto University of Education | 34.950215 | 135.773187 |   京都府京都市伏見区深草藤森町1 |    1,332 | 110      |
| Kyoto Institute of Technology | 35.049664 | 135.782046 | 京都府京都市左京区松ヶ崎橋上町1 |    2,656 | 281      |

<br>

最後に作成したdfn からデータを読み込んで緯度経度の値から地理的な関係と、学生と教員の関係を示す散布図を表示します。最初のグラフではプロットの大きさに学生の人数が反映されるようにします。また二つ目にはプロットの凡例をつけています。

```python
import matplotlib.pyplot as plt
import numpy as np
fig, ax=plt.subplots(ncols=2,figsize=(10,5))

for i, u in enumerate(dfn.index):
    dfn['students'].values[i]
    ax[0].scatter(dfn['longitude'][i],dfn['latitude'][i],s=dfn['students'].values[i],label=u)
    ax[0].set_ylabel('latitude')
    ax[0].set_xlabel('longitude')
    ax[1].scatter(dfn['students'][i],dfn['teachers'][i],s=100,label=u)
    ax[1].set_ylabel('students')
    ax[1].set_xlabel('teachers')
    ax[1].legend()
plt.show()
```

<img src="./img/u_in_kyoto.png" style="zoom:50%;" />

<br>

### ５ー４　練習

１）　0,0,1,0,0,1.... を繰り返す総数250個の1次元の数列をつくり、それを16*16の２次元数列に変換しなさい。

２）　作成した配列をmatplotlibの`imshow()`を使って表示しなさい。

３）　４ー１の例で扱った関西地域の県名、県庁所在地、県の木のデータに合わせて、県の花を加えて表にしなさい。











