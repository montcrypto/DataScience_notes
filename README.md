# DataScience_AI

Materials for lecture 2021 MU

## 「環境データサイエンスとAI」　

本テキストは、pythonを用いてコードを作成し、大量のデータから有意義な情報を引き出す統計計算や機械学習の基礎を学ぶことを目的としています。以下の教科書は、全般に関する知識として、色々ある中で個人的に役に立つと思うものをあげています。

1) Bill Lubanovic, 入門 Python 3, 斎藤康毅(監修),長尾高弘(訳), オライリージャパン, 2015（第2版2021）
2) ディジタル画像処理編集委員会, ディジタル画像処理（改訂第2版）, 画像情報教育振興協会, 2020
3) 石井健一郎他, わかりやすいパターン認識（第2版）, オーム社, 2019
4) 斎藤 康毅, ゼロから作るDeep Learning―Pythonで学ぶディープラーニングの理論と実装, オライリージャパン, 2016
5) David Foster, 松田 晃一他,　生成 Deep Learning ―絵を描き 物語や音楽を作り ゲームをプレイする, オライリージャパン, 2020

### 目次

１　Pythonのインストールなど

２　電卓をつくる

２−１　演算記号

２−２　比較演算子

２−３　データのタイプ

２−４　練習

３　データの型

３−１　リスト型

３−２　セット型

３−３　タプル型

４
　４−１

５
  ５−１

６
  ６−１

７
  ７−１

８
  ８−１

９
  ９−１

１０
  １０−１

１１
  １１−１

１２
  １２−１



## 1　Pythonのインストールなど

#### １ー１　標準python

理科系ではMatLabやRなどを使用したことがあるかもしれませんし、JavaやCの言語を使える方もいるでしょう。Pythonはそれに比べて、汎用性の高いライブラリーが多く開発され、科学分析において多くの人が使うようになりました。科学計算に必要なライブラリーが備わってきたこと、さらには読みやすく、書きやすく設計された言語であることが人気の一つと言われます。また、Githubなどの共同開発のサイトなどの活用により、コードが何度も読まれ、改訂されるたびに、さらに分かりやすくなるといわれます。なぜpythonかといえば、そういうコミュニティーがあり、常に良い言語を話そうとする人たちが、有益な情報をネットに上げてくれているということも上げておくべきでしょう。

とは言え、言語ですからある程度覚えないと話せません。しかし、苦しい時期はおそらく思っているより短いと思います。

Python3をインストールします。このテキスト執筆時点で、最新のバージョンは　3.10ということですので、そのうち4が出てきてまたアタフタする様なことになりそうですが、とりあえず6ヶ月くらい前にレリースされた安定バージョンをインストールするのがいいように思います。理由は、科学技術計算や機械学習で利用するパッケージの対応を遅れている可能性があるからです。ちなみに私はM1 Macを使っていますが、Pythonは3.8.２です。インストールの際、scikit-learn, scikit-image, tensorflowという、パターン認識、機械学習、画像処理に必要なものが問題なく動くバージョンということで選択しました。

あまり悩むことなく標準のパイソンをhttps://www.python.org/ からインストールしてみましょう。
必要なパッケージはその都度インストールしますが、この講義では使うのは以下の通りです。
numpy, pandas, scikit-learn, scikit-image, opencv, matplotlib, tqdm, tensorflow, openpyxl, pillow, jupyter, jupyterlab, ipython, seaborn, hdf5

<img src="https://www.python.org/static/img/python-logo@2x.png" height="50" >
<img src="https://scikit-learn.org/stable/_static/scikit-learn-logo-small.png" height="50" >
<img src="https://scikit-image.org/_static/img/logo.png" height="50" >

ハードディスクに余裕があって、いろいろな科学技術計算のパッケージがプレインストールされる方がいいばあいは、anaconda pythonをインストールしてください。



#### １−2　クラウドサービスの利用

Colaboratory（略称: Colab）は、ブラウザから Python を記述、実行できるサービスです。Googleの提供するサービスなので利用する人はGoogleアカウントを取得してください。計算時間とか、ファイルの保存期間とかに制限がありますが、お試しには夢のようなサービスです。

https://colab.research.google.com/notebooks/welcome.ipynb?hl=ja#scrollTo=5fCEDCU_qrC0





## ２　電卓を作る

#### ２ー１　Pythonで扱うデータ

取り扱うデータ型は以下の通りです。
+ ブール値（Boolean)：TrueとかFalseという値
+ 整数（integer):小数点以下がない数
+ 浮動小数点数（float):少数以下を含む数、指数表現で表される数
+ 文字列（character):文字の並びで表されるもの

#### ２−１　演算子

四則演算で必須なものは次の通りです。
+ +：加算
+ -：減算
+ *：乗算
+ **：指数（べき乗）
+ /：浮動小数点数の割り算
+ //：整数の除算（商切り捨て）
+ %：剰余

#### ２−２　比較演算子

主な比較演算子は次の通りです。

+ a < b：a は b より小さい
+ a <= b：a は b と等しいか小さい
+ a > b：a は b より大きい
+ a >= b：a は b と等しいか大きい
+ a == b：a と b は等しい
+ a != b：a と b は等しくない

#### ２−３　練習

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
...     print(sho,' amari ',amari)
...
>>> warizan(34,6)
(5, ' amari ', 4)
```

１）9時00分00秒から3333秒後は、何時何分何秒ですか？

２）1)を計算する関数を作りなさい。

→ step1.ipynb



## ３　データの型

電卓の時は、１つの入力に対して1つの出力があった。ここで取り上げるデータは複数あるいはもっと多元的な複雑なデータである。まずは一次元の要素の並びを考える。

前出の文字列がどう扱われるかを説明しましょう。’university' という文字列は、数値と違って、アルファベットの列と捉えられ、単語全体では10個の文字からなると認識されます。整数のインデックスで先頭から順番に各要素を取り出すことができ、3番目は'i’の文字というように、一つのシークエンスとして扱えます。pythonでは要素の1つ目を０に定義するので、3番目は0,1,2の２となることに注意しましょう。

```python
>>> word='university'
>>> print(len(word), word[2])
(10, 'i')
```



これと同じように、リストとタプル型のシーケンス構造が提供されています。リストは変更のきくシークエンス（並び替えが可能）で、タプルは辞書向きで、書き換えることができません。前者をミュータブル(mutable)、後者をいミュータブル(immutable)といいます。

#### ３−１ リスト型

リストは０個以上の要素をカンマで区切り角かっこ[　]で囲んだものです。リストの中の要素は、先頭から順番に指定して取り出すこと、範囲を決めて複数取り出すこと、など色々設定可能です。

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

list( )関数は他のデータ型をリストに変換します。例えば、文字列の場合

```python
>>> list('university')
['u', 'n', 'i', 'v', 'e', 'r', 's', 'i', 't', 'y']
>>> word='university'
>>> word.split('r')
['unive', 'sity']
```


#### ３−２　セット型

ちょっと複雑になりますが、この機能を使ってリストの中の要素を取り出すことができます。それにはリストをset( )関数に入れるか、リストを{  }で囲みます。データが書き込まれるメモリの位置によて順番が変わるので、いつも同じ順番とは限らないので、順番を気にするときは注意が必要です。

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
セット型のデータは集合演算につかいます。

+ 和集合（ユニオン）: |
+ 積集合（インターセクション）: &
+ 差集合: -
+ 対称差集合: ^
+ 部分集合か判定: <=
+ 上位集合か判定: >=

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

#### ３−３　タプル型

辞書などの作成すると変更しないようなデータのために準備されています。タプルは(  )で囲んで作成します。
 例えば京都の地理的位置や、学生の科目別成績など、**複数の要素から構成される独立したデータ**をあらわすときはタプルを使用します。タプルは[ ] で引数を入れることで個別に取り出すことができます。またタプルはリスト型に直すことで値の変更が可能です。

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
```



## ４　データの特徴



 ### イテラブル・イテレーター



イテラブル(iterable)とか、イテレータ(iterator)とは『反復可能な』や『繰り返し可能な』という意味です。この要素を使いこなせるようになると一気にやれることが増えてきます。

「パソコンは「繰り返し処理をやらせるには最適」だけど考えるのは人間！」とは30年前の言葉ですが、ある意味で今でも真実です。その繰り返しの処理を考えてみましょう。

パソコンにログインしていつものように作業をします。そのときあなたのディレクトリーはどこですか？この質問、30年前であれば皆正解かもしれない質問ですが、みなさんはどうでしょうか。GUI（graphic user interface)のおかげで、知る必要のない皆さんは質問の意味がわかるでしょうか。

```python
>>> import os
>>> os.getcwd()
'/Users/sugiyama'
>>> os.listdir()
['Music','Pictures', 'Applications', 'Documents']
```

上に示したコードのos.listdir()は私のコンピュータの中のディレクトリをリスト型で出力していることがわかります。 list形式のデータはイテラブルなので、繰り返し処理につかえます。例として、ディレクトリの中にいくつファイルがあるか順番に出力してみます。

```python
>>> My_dir=os.listdir()
>>> for my_output in My_dir:
>>>   tmp_files=os.listdir(my_output)
>>>		print('ディレクトリ'+my_outpu+'のファイル数は'+str(len(tmp_files)))
ディレクトリMusicのファイル数は4
ディレクトリPicturesのファイル数は6
ディレクトリApplicationsのファイル数は1
ディレクトリDocumentsのファイル数は8
```

上の簡単なfor ~ in の簡単なループは、My_dirの中のリストから、ひとつづつmy_outputに出力して、印刷せよという意味になります。

以上リスト型のですが、数字の場合もrange()という便利なイテレーターが準備されています。

```python
>>> list(range(10)) # range(0,10,1) と同じ
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1,10,3)
[1, 4, 7]
```



#### 条件文　if

例えば解析用に作ったデータの中にいわゆる不可視ファイル（実際に存在はするのだけど画面上には表示されないシステムが使うファイル）があります。ところが、プログラムでデータを読み込むとファイルが全部読まれてしまいします。それを避けてファイルを読むには次のように処理します。

```python
>>> My_jpg_list=[]
>>> My_list=os.listdir('Gaszou')
>>> for filename in My_list:
>>>		if filename.endswith('.jpg')
>>>			My_jpg_list.append(filename)
>>>		elif 
>>>			print(filename+'is not a jpg file !')
>>> My_jpg_list
```

上の例では、Gazouのファイルにあるファイルのうち、拡張子が.jpgでないものを無視してjpegファイルのみのリストをMy_jpg_listに格納します。

複数の用件を同時に満足する、あるいはどちらかを満足するという条件が必要な場合は、AND あるいはOR で複数の条件を併記します。

```python
>>> testdata=[1,2,3,4,5,6,7,8,9,0]
>>> for i in testdata:
...   if i > 4 and i<7:
...       print(i)
5
6
```



以上のように、イテレータと条件文はプログラムの中で、繰り返す・判断するという二つの重要なプロセスを実現します。



#### 内包的表現

繰り返しと条件文は数行のプログラムで書けるものですが、内包的表現を使うと１行で書くことができます。

例えば ある特定のディレクトリの中から特定の拡張子のファイルだけを読み出したい場合、そのリストを作るには次のようにします。

```python
[fi for fl in os.listdir('my_target_dir') if fl.endswith('.xslx')]  ＃　例えばエクセルのファイル
```

また、不可視ファイルを除いたリストが欲しい場合（MacOSの場合は .filenameの形式で最初にドットがつきます）には次のようにします。

```python
[fi for fl in os.listdir('my_target_dir') if fl.startswith('.')]  ＃　例えば不可視ファイル
```



#### ジェネレーター

```python
x=list(range(10000))
def gen(x):
	tmp=[]
	for i in x:
		tmp.append(i)
		if len(tmp)%%1000==0:  #### ここが問題
			yield tmp
```

