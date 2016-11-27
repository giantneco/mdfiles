# PyCon JP 2016
## Keynote, Breaking the rules

jesica Mckeller
 director python community

 not python but systems

  programming chnagesthey way you think about ,,,

  tenets of free software, allow aus to do that

  tenets of free software'
   0 run
   1 study
   2 redistribute
   3 distribute

  programming has rules, but you can change the rules

  everything important is as systems

  most important system is people systems

  This is why i teach people to program

## 週末サイエンティストのすすめ

Yuta kashino, Bak FOo, inc. CEO

 Astro Physics /Ovservational Cosmology
 Zope/Python

週末サイエンティスト
 知的好奇心、勤務買い、休みの日に
 Publich OR Perish の義務なし
 必要に応じて勉強

週末研究が可能な背景
 安価な計算リソース
 オープンアクセスできるデータ
 オープンソース

安価な計算リソース
 クラウド
 安価な高速回線
 仮想化技術

オープンアクセス
 arXiv オープンアクセスジャーナル
 オープンデータ
 技術部露軍、カンファレンス
  google brain, OpenAi
 勉強会ミートアップ
 計算機協議コンテスト -> kaggle

オープンソース
 github

週末研究
 論文を読んで研究
  科学的方法論に沿って研究する
  研究リテラシーをもって研究する

 研究リテラシーとは
  研究アイディアを思いつき、育てる
  論文を探す
  理解できないときは足りない知識を自学自習する
  科学的方法論
  再現性
  ねつ造・剽窃を行わない

計算機環境をどうするか

 大人の道楽は年間 100 万かかるのも仕方ない

  信頼できる業者からサーバを借りる
   GPUの場合はAWS,さくら、Azure,Softlayer
   おすすめは さくらの高火力、超安定、コスパはよい
   AWS,コスパはよくないドライバは古い、しかしスケーリングは劇的

  OS
   Ubuntu 一択
    業界標準、化学スタックはほとんどUbuntuで開発されている
    ソースからビルドする場合も大体うまくいくことが多い

   Python
    Anaconde （conda + pip) にする
     科学技術計算では conda (Anaconda) が標準

  実験環境
   状況による、docker/docker compose が適している場合が多いかもしれない

 コード保全をどうするか

科学スタック

 Python 科学スタック

論文を探す
 arxiv
 StatMLPapaer
 GitXiv / Arxiv Sanity Pareserver
 trending_arixiv /

 カンファレンスをチェックする
  NIPS, ICML, KDD, IVPR

 SNS で若手のアクティブな研究者をフォロー

  PEAK 問題
   一流になるのは才能か努力家
   継続的な deliberate practice
    コンフォートゾーンを超える練習
     目的を明確に
     フィードバックをうけ
     間違いを修正しながら
     飽きないように工夫して長期間継続する

  自学自習のポイント
   PEAKの原則に沿う
   早期練習には効果がある
   自分が発表する以外の勉強会は避ける
   MOOC/教科書はかなあず練習問題をやる

  科学的方法論に沿う

## Pythonで作る Web クローラー入門
   @amacbee

Webクローラとは？
 クローラ Wikipedia
  ウェブ上の文書や画像などを周期的に取得し、自動的にデータベース化するプログラムである
 混同されがち
  クローリング
   リンクをたどりながら保存
  スクレイピング
   保存したページから特定の情報を抽出

クローラの利用事例
 クローラで情報収集は最近多い
  類似映画検索システム
  ECサイトのトレンド分析システム など

事例１ 類似映画検索
 Azure上で動作
  数十万件パー３か月

事例２： ECサイトのトレンド分析
 ECサイトから在庫状況を見てどの商品が人気になっているかを分析

クローラを利用してデータを収集 －＞ データ分析の幅が広がる

Pythonを利用したクローラ作成・運用方法を紹介

LibraHack事件

クローリングの際に遵守したいこと
 著作権法に配慮
 robots.txt に記載されたアクセス制限をまもる
  クローリングをする前に robots.txt を最初に確認する
 APIがある場合はそちらを利用する
 サーバアクセスは 最低でも１秒以上開けてする
 会員のみが閲覧できるページは利用規約をまもる

### Scrapy
 クローラフレームワーク
 クローラ作成時に考慮しなければならない機能をオプションを指定するだけで簡単に実現可能
  サイトのクローリング間隔、robots.txtの解釈

 スケジューリング、ジョブ管理、etc の機能を内包
 scrapy1.1からpython3対応している

１回だけやるのには Scrapy は重いので、スケジューリングをして日々やるときにScrapyがよい

#### install
 Ubuntu の場合は apt-get install python-scrapy でできる

### Scrapy を用いたクローラ作成
 1. プロジェクト作成
    `scrapy startproject <プロジェクト名>`
 2. クロール対象を定義

 3. クローラ本体を作成
    `scrapy genspider クローラ名 クローラ対象ドメイン`
 4.

### Tips

 どこをスクレイピングするか？
  google chrome でスクレイピング箇所を特定できる

 scrapy shell でインタラクティブに結果を確認できる

 クローリング家庭とスクレイピング家庭は分けたほうがよい
  サイト構造がくぁることは頻繁にある

 対象サイトに javascript が夫君られているか確認する
  javascriptが含まれているかどうかで難易度に雲泥の差がある

### クローラの管理
 Scrapy Cloud
   scrapinghub が提供している Scrapy 環境
   優良だがクロール範囲が１サイトなら無料

## chainer で作る対話 bot

@showGushiGit

dialogue value
 new user experience
character

 how to add character to the bot
  hire senario writer -> too expensiv
 Add character to simple text
  -> NeuralStroyTeller
     makes: add chracter function to text with image?
 chat -> neural network
 quenstion -> elastic search

interface -> slack

### System
 choose the topic
  -> word net
    grouping concepts
   -> use wikipedia entity vector
   -> use cosine similarity to measure distance between entity
      コサイン類似度

why neural network

 expression
  text vectorize -> word baging (legacy)
                -> word2vec (new!)

 continuously
  phrase for cointinouely
  recurrent neural network

Focus
 Attention Model (Neural Network) to find important word from text

How to implement

### Question or just talk?
 We use "?"


## Packaging を支える技術
 小田切篤
 Beproud, Inc
  Pylons, Pyramid
### PyPA
 packaging をメンテするグループ
 github.com/pypa

#### PyPA 基本ツール
 - setuptools
 - virtualenv
 - pip
 - wheel

condaは使うべきではない？

#### setuptools
 配布物を作成する
 setup.py で使われる
 - no easy_install, distribute, egg
   使うべきでない
 - 27.2.0

### virtualenv
 python 環境の仮想化
 python3.3 からは python 本体が pyenv を入れている

### pip
 installer
  sdist and wheel
 requirements.txt でライブラリを構成管理する

### wheel
 wheel形式のパッケージを作成する

### ツールの導入
 python>=3.4
  pip,setuptools を導入する ensurepip が入っている
  python をインストールしたら pip が利用可能に

 どの環境でも get-pip.py で pip,setuptools,wheel を細心にできる
  ライブラリ作成者は これを入れておいて常に最初に実行する

### ubuntu の pyvenv
 14.04 - ensurepip が消されているため --without-pip をつけないとエラーになる
 16.04 - ensurepip は入っているが、 pkg_resource-0.0.0 という謎パッケージメタデータが入ってしまう
  回避策は --without-pip で環境をつくってから get-pip.py でツールを導入する必要がある

### PYTHONPATH と sys.path
### side-packages/user-isite-packages
 サードパーティ製ライブラリの標準インストール先
 debian ではさらに dist-packages というディレクトリがある

### wheel
 PEP 427
  バイナリ形式の配布フォーマット、すでに利用されている

 PEP 513
  これまでは Linux 向け wheel は pypi に挙げられなかった
   manylinux1 仮想のディストリビューション、これに対応すれば動くはず
  linux向けの wheel を作るために決められた

  Linux向け wheel のつらいところ
   どのようなライブラリがあると想定してよいか
   ライブラリの　ABI が合わない場合どうする？
   依存ライブラリ同梱のためのハックが setup.py に散らばることになる

Python の ABI
 pymalloc,ucs-4 昔
 python3.4 では統一

wheel の命名規約

manylinux1 の想定
 centos 5.11
 x86, x86_64 同時
 いろいろライブラリ

auditwheel
 linux 向け wheel を manylinux1 に変換してくれるツール
 manylinux1にないライブラリは 依存ライブラリを同梱して rpath も修正してくれる

docker イメージを利用してパッケージを作成できる
 docker イメージを pypa が用意している

ソースディストリビューション　sdist とは何か？
setuptools と pip の実装でなんとなく決まっている。PEPで決まっていない

現在のインストール手順に setup.py install は入っていない

PEP518
 パッケージ方法やそれに必要なツールを支持する
 パッケージに必要なツールを記述
  pyproject.toml
  TOMLフォーマット
   標準パッケージに入ってないのでインストーラが含むか、TOMLパーサを作るかしないといけないが。。。

setuptools に依存せずにパッケージングすると？
 distlib
  wheel パッケージ作成
  wheel パッケージインストール etc, PEP でできることはできる

まとめ
 setuptools や pip がなくてもパッケージングはできる
 いろんなツールがエコシステムにさんかできるように sdist の定義が検討されている

## 確率的ニューラルネットの学習と Chainer による実装
tokui @beam2d

Resesarcher at Preferred Networkds,Inc.

Stochastic Unit
 非決定的にふるまう

Stochastic Unit
 普通のニューラルネットは決定的

Stochastic Unit
 サンプリング付きのユニット
 ガウシアンな Stochastic Unit は平均と分散を前の層からもらうと、ガウス分布に基づいて値を出して次の層に渡す
 これに対して微分はどうやる？

 さらに出力が離散的になる場合もある i.e. ベルヌイユニット

どこで使う?
Stochastic feed-forward networks
 非決定的な　prediction
 多値の prediction
 e.g. inpainting lower-part of given images

Learning generative models 生成モデルを学習したい場合
 Loss function is ofen written as a compuatational graph
 e.g. variational autoencoder (VAE)
 実際に学習するモデルに確率で決まるものが出てくる場合

難しいか？
 Stochastic NN は非決定的
 期待値を最適化するモデルにしてしまう
  確率で重みづけられた loss

 出現する値を列挙
  ガウシアンは原理的に不可能
  ベルヌイは近似

よくつかわれるのは likelihood-ratio method
 普通のニューラルネットワークと同様にフォワードを計算してサンプリング
 ロスが高いサンプルの確率を下げるようにする
  実際には出てきたロスにひれする割合で下げる

reparametaization trick
  ノイズを設定して、ガウシアンのサンプルをとったものを扱う
   ガウシアンでしか使えないが、ノイズを入力と考えれば普通のNNとして扱えるので 扱いやすい

chainer
 numpy とかと自由に行き来ができるので実装はかなり楽にできた

## LT

### simple karaoke scoring system

### Deeplearning Mentor Wanted

### Python で簡単に仮想通貨の取引がｄけきるようにしてみた
 テックビューロ
 Fintech

### ＠CardinalXiao

### Python Astronomy
京都虹工房


## memo

http://togetter.com/li/1027133

## Keynote 2

@vlasovskikh Andrey vlasovskikh

what's new in python 3.6

not released yet

formatted string literals
```
print(f'Hello, {city}')
```

Syntax for variable annotatins
```
city: str ='tokyo'
```

underscores in numeric literals

asynchronous generator and....

story of python3

python 2 vs 3

for pycharm users, up to 29% use both 2 and 3
predicted equal usage in 2017-09

python 2 end-of-life is 2020

 python 2 retireent party at pycon us 2020
 django 2.0 will drop ptyhon 2 in 2017-1 2

Histroy of type hints

python 3.0: function annotation , just syntax, no semantics

3.5: standard notation for type hints
  based on function annotations
    the typing module for type system constructors
    third-party type chckers" mypy, pycharm

3.6: variable annotations
  native syntax insteard of type hints in comments

type hints: upsides
  tools for type checing, code completion refactoring
  better documentation
  enough to annotate APIs

downside
 may look like static typing
 tools don"t support all the features of type hints
 only a few libraries come with type hints

 porting python3,  expensive , tsiwted required abournt $60000
 start porting to typthon 3 by adding type hint

Async-Await

 history
  3.4: sequential syntax for Async-Await
   yield
   asyncio module
  3.5: new syntax for async
   async def
   await
  3.6: asynchronous generators and comprehensions
   yield in coroutine unctions
   ...

upsides
 sequential syntax for async
  make more readable
  new aio* family of libraries: aiohttp, aiopg, ...
 coroutine and awaitable as language Concepts
   async code looks pythoinc

donwside
 async versions for all blocking I/O libraries
 django and flask use blocking I/O
 No asyncfor CPU-intensive computations in threads

conclusion
 complicated past, but evlolving

## You might not want async

ID
 @uranusjr
 http://uranusjr.com

Not for
 infects the whole program
 async is not parallerism
 Third party support

example
```
import aioodbc

async def read+read(dbname):
    con = await aioodbc.connect(
        dsn=  
      )
```

```
import aiohttp
async def collect_contents(urls):
    contents = []
    with aiohttp.ClientSession() as session:
        for url in urls:
            async with settion.get(url) as rest:
                if resp.status != 200:
                    continue
                content + await resp.text()
                contents.append(content)
    return contents
```

how to test python3.4 asynciio code?

unittest does not know about asynciio
 coroutine methods are executed "normally"
 for test asynchronous functions, wrap function or use asynctest

## Deep Learning with Python & TensorFlow

Lan Lewis - @IanMLewis

Deep Learning 101

How do you classify these data points? nn an find a way to solve the problem.

tensor
 point or value or ... , milion of dimension ?

Breakthroughs

What is TensorFlow

## Pyton を支える技術 module, import 編
  @knzm2015

import の裏側で起きていること

 1. sys.path からモジュールに対応するファイルを検索する

 2. ファイルが見つかったらロードする

正確にはいろいろ足りない
 1. sys.meta_path を検索して、PathFinder の find_specを呼び出す
 ...

import -> __import__ -> importlib.import と内部で変換される

インポートフックと importer プロトコル

 インポートフック、モジュールの検索方法、ロード方法をカスタマイズするための方法

 import プロトコル、フックが満たすべき仕様？

メタフック インポート処理を開始するときのフックポイント

パスフック 検索・インポート実施時のフックポイント

ファインダー・インポーター・ローダー・モジュール除法

import pep 302

PEP 302 New import hooks

PEP 420 implicit namespace package

PEP 451 A ModuleSpec TYpe for hte Import SYstem
 モジュール仕様の追加、結構大きく変わった
 finder,loader で重複する仕様をなくした

用語の整理
 モジュール
  .py (.pyc, .so のことも)

 パッケージ
  通常のパッケージ
  python3.2 以前の名前空間パッケージ
  python3.3 以降の暗黙の名前空間パッケージ

モジュールオブジェクトの持つ属性
                    モジュール            パッケージ
`__name__`      csv                  json
`__file__`      .py                  __init__.py
`__path__`      NEVER               [filepath]
`__package__`


名前空間パッケージ

 zope や shpinx で採用している

 django はフリーダム

伝統的な名前空間パッケージ

 python2
  - pkgutil.extend_path() (python 2.3 から)
  - pkg_resources.declare_namespace() (from setuptools)

   欠点
    `__path__`の操作方法が統一されていない
    `__inint__.py`の存在が無題。どのディレクトリにあるものが読まれるかわからないのですべてに同じ内容を書かないといけなかった
                  の存在が邪魔、複数のパッケージを入れるときに衝突す    

名前空間パッケージ関連の　PEP
 PEP 420

PEP 366 main module explicit relative imports

学び
 python import システム、バージョンアップと根本的な改良の歴史
 PEP が公開されているので、義理音の経過がわかりやすく後からでも現在の仕様なった理由がわかりやすい

## メタプログラミンPYTHON

metaprogramming ruby を参考

## building a data preparation pipeline with Pandas and AWS Lambda

  - Fabian
  - denryoku.io

Why data preparation
 - showing it to an audience
 - a report from a survey?
 - a news article with charts?

But a lot of available data is messy
 - incomplete or missing data

it has all the reason to be messy
- human erros, ...

can have very bad consequences
- Crash in your report geretarto
- incomplete reports
...


data journalism and interactive visualizaion (ex)

How to preprare data

common operations
 date parsing
 desiding on  a stratege for null or non parseable values
 enforce value range
 sanitise strings

 Exsiting tools
 Trifacta Wrangler, Talend Dtaprep, Google Open Refine

Shy python and pands
with python, you can do anything, not difficulrt
pandas is a versatile tool, easy to specify transformations,

Jupiter notebook

testing your preparation
 unittests
 test for anticipated edge caes (defensive programming)
 property based testing (http://hypothesis.works/)

Pipeline with AWS Lambda

AWS Lambda: server less solution
 Serverless offer by AWS
 no lifecycle to manage or shared state
 low cost

some challenges
 dont let users run scriptsNo

 automateing is part of a quality process

## memo
 - https://github.com/esuji5/yonkoma2data

## END


BigData , 5
cience   , 5
Usefull tools , 4
Web frameworks , 4
Best Practice & Pattern , 3
Other , 3
Industry Uses , 3
Cloud , 3
Core Ptyhon , 3
Education , 2
Python Internals , 2
bussiness , 1
conccurency , 1
System Administration , 1
Packaging , 1
Mobile , 1
Testing , 1
Community , 1
Distributed Computing , 1
Emmbedded Systems , 1
Databases/NoSQL , 1
