# システムプログラミング会に参加してきました

7/2のシステムプログラミング会に参加してきました。

募集期間が非常に短かったのですが、たまたま TL を覗いた時に見つけたのでなんとか参加申込することができてラッキーでした。

時間切れのため途中で帰ってしまったのですが、懇親会を含めると結構長い時間やっていたようです。

以下メモ。

## New LLD Linker for ELF by Rui Ueyama (@rui314)

- windows 上でもリンクできるようにしたい
  - もともとのモチベーション
- コンパイラとかデバッガとか移植しないといけない
  - 作ってみたら意外とうまくいって、オープンソースなのでUNIXに移植しようということになった
- 現在 GNU でないといけないのはリンカぐらいしかない
  - BSD は GNU LD から移行したい
  - 現時点で BUILD WORLD とかは動く
- MIPSに対応
  - MIPS は ELF なんだけど MIPSのELF になっている
  - 一部リトルエンディアンで一部ビックエンディアンとか
    - ドキュメントはなく、GNU リンカーのソースコードを見ないとわからない状態
- icf オプション
  - identify content folding
    - ふつうは名前でまとめるが、このオプションをつけるとコンテンツをま    とめてフォールディングする
    - 基本的にはグループ分けして内容が違ったら分割、リロケーションがさしている先が同じだったらまとめる
    - 平衡に達したらマージ可能なグループになる
- LLD の設計としては、余計なことをしないことを主眼においている
- GNU LD のシンボル解決
  - 引数の順序によってリンクのされ方が異なるという問題があった
  - LLDではかなり変えていて、ファイル渡す順序によらずシンボルを解決している
- ファイルサイズはかなり小さくできている。
  - C++ で10,000行ぐらい。
- リンク時の名前解決
  - ハッシュ使用
    - 少なくとも１回はハッシュを使う 名前解決のため
      ハッシュに名前を入れるのも結構時間がかかる
    - C++だと関数が 50 バイトくらいなっていたり
      名前の変更がポインタの変更になっている
  - 別のファイルを読んだときに、すでにハッシュキーがあったらその先を書き換えて内容を変えたことにする
  - ```wrap```の利用
    - ld で ```wrap``` オプションを渡すと、```malloc``` は ```__wrap_mallock``` にリンカされる。
      - もとのmallocは ```__real_malloc``` で参照可能になる
- LLVM
  - Link Time Optimization (LTO)
    - グローバルなビューをリンカはもっている。
    - LLVMはバイトコードをもっているので、リンカが名前解決をするときに
      そのバイトコードを使ってネイティブコードに落とす （よくわからん）
- 今後の目標。 FreeBSDで普通に使う。カーネルのビルド。
- ハッシュ関数
  - 早くするために何かしているか？
     - 普通のハッシュ関数を使っている
     - はやくしたらというアイディアはある
     - キーはヌル終端なものなので、```strlen``` で結構時間を食っている
       - 長さを渡してあげれば？あるいは sha1 でできないかなど
### 感想
GNU LD についても知っているようで知らなかった話が結構聞けてよかった。

現状の GNU LD のことを考えると、案外あっさり置き換えられたりするのかも。

## Kati @shinh

 - http://shinh.skr.jp/slide/kati_sp/031.html
 - ビルドシステム
 - Android Platform
   - アプリ開発者というよりデバイス開発者向け
   - 結構でかい
   - 普通にmakeをつかっている
 - Android.mk
   - GNU makeのチューリング完全性を悪用して謎DSLをつかっている
 - Kati で GNU Make より高速ビルド
 - 最初は Go で書いていたが GC が遅いため C++ で書き直した
   - Android.mk では find を多用していおり遅くなっていたので自前の find を用意した
   - 最初にディレクトリ構造を持ち、次回からはそれを使用する

## LLVM と C++ でコンパイラフロントエンドつくった ＠Lind_pp
 -  https://speakerdeck.com/rhysd/make-a-compiler-frontend-using-c-plus-plus-and-llvm
 - プログラミング言語 Dachs
 - Ruby like な緩い構文
 - 強い型づけ＋型チェック成
 - パーサジェネレータの Boost.Spirit
 - 意味解析と LLVM IR の生成は vistor パターンを使用

### 感想
 LLVM 使うとやっぱりこういう風になりそうな気はする。

 質問タイムであったように最適化とかをやりたいというような用途には向いていないっぽい。

## なんかトレースする話 @nalsh
 - https://speakerdeck.com/naruse/nankatoresusuruhanasi
 - ps -elF
 - perf top
   - 楽しい
   - 特権が必要
 - procfs
   - ```/proc/<pid>/stat```
     - 実行中のアドレスがわかる
     - バイナリと合わせて実行中の関数が推測できる

## Programming TCP for responsiveness by Kazuho Oku (@kazuho)
 - http://www.slideshare.net/kazuho/programming-tcp-for-responsiveness
 - H2O HTTPサーバ
 - レスポンスのために、データが CWND を超えてTCPパケットを送信できるようになったらすぐ送信できるようにしたい
 - データは TCP send buffer と BIO buffer にためられる
 - BIO buffer は TCP send buffer からあふれた分
   - poll して SOCKET_IS_READY になった段階で書、残り 6 bit をき込むことで BIOとしてめずに済む
   - それでもまだ poll が SOCKET_IS_READY になる閾値は　CWND より大きい
   - socket オプションの TCP_NOTSENT_LOWAT を 1 に設定
     - 0 だといろいろ問題が起きてしまう
   - これで CWND + 1 になったときにデータを送れるようになった
 - ただし send buffer が小さくなったことでの弊害もあり

### 感想
実をいうと、最初聞いたときはあんまりよくわからなかった。

あと HTTP2 もよくわかっていない。つらい。

## Fron IA-32 to AVX-512
 - http://www.slideshare.net/herumi/from-ia32-to-avx512
 - i386
   - 32bit汎用レジスタ eax,ebx,... 8つ
   - eax 下位 16bit が ax, ax の下位　8bit が al
 - modR/M
   - 先頭 2 bit を mod として使い、残り 6 bit を 2 つのオペランドとして指定できる
   - ```mod==00```ならレジスタとレジスタの操作になる
 - パーシャルレジスタストール
   - ax を操作した後に　eax を操作するとペナルティ。遅くなる
 - x64
   - レジスタは　16 個に
   - modR/M のために re プレフィクス
   - 32bit 操作をすると上位 32 bitはクリアされる
   - NOP命令が追加
 - AVX
   - 16 個の　256 bit SIMD レジスタ
   - 3 オペランド命令
   - VEXプレフィクス
 - コンパイラのバグでパーシャルレジスタストールが起きた事例
### 感想
のちのセッションでもあったが、Intel の Software Developer's Manual は目を通しておいたほうがよさそう。
この勉強会に来るまで存在も知らなかったので、またも不勉強が露呈した。
## Unix Domain Socket by 田中哲
 - http://www.a-k-r.org/d/2016-07/2016-07-02-unix-socket-api-problem.pdf
 - UnixDomainSocket ふるまいは多様（）
 - APIが腐っている
 - sun_len
 - ソケットアドレスの終端
   - NULL終端で判断する
   - 引数で渡されたサイズを使用する
   - etc
 - 表現方法が複数あるので混乱が起きる
 - APIデザインは重要
## コンパイラをつくった話 by 七誌 (@7shi)
 - https://onedrive.live.com/view.aspx?resid=FB45E1F8CE8B532E!82121&ithint=file%2cpptx&app=PowerPoint

### 感想
ここら辺はトイレに行っていて半分くらい聞けてなかった。

ASTをXMLで表現する、というのは仕事でやったことがあるが、あんまりやらないほうがいいのかも。
## L1キャッシュ @kumagi
 - Radix Sort
   - O(N) なソートアルゴリズム
   - 経験上一番早い by iwiwi
   - LSD と MSD
 - SoftWare Write Combining
   - CPU の書き込み先メモリアドレスを絞り、L1キャッシュに乗せられるよう    にする
   - Intel のマニュアルに書いてある
### 感想
この話は面白かったが、あまりついていけてない。資料が公開されいたら読みたかったがなさそう。
とりあえず Intel のマニュアルと、Radix ソートについては調べておきたい
## StackExchangeでみたシステムプログラミング案件 by @hogegashi
 - https://docs.google.com/presentation/d/1Y62OO574mcnaKItgAFIO49jCkZ4lOnUY0sMyUgAwQMs/edit#slide=id.p
 - StackExchange は面白い
 - 実行中にシステムコールを全く行わないUNIXコマンドはあるか？
 - システムコールなしでシグナルをどれだけ呼び出せるか？
### 感想
ここも案外知っているつもりで知らないことが多かった。
普通のコマンドではかならず```exit()```が呼ばれる、というのも、言われてみればそうだがあんまり意識したことはなかったし、結構盲点を突かれた感じ。

## 俺々OS用スケジューラの設計と実装 by @yitabashi
 - オレオレOSスケジューラをつくったという話

## REMarks by @mkasahara
 - 実行したコマンドを自動的に記録して、再度コマンドを実行する Makefile？ を生成する
 - LD_PRELOAD を使用して open を入れ替えて、開いたファイルを記録
 - LD_PRELOAD でライブラリを読み込んだときに、ライブラリが procfs を open をしていたので、```/proc``` 下を無視する必要があった
## Out-of-thin-air by @yamasa
 - メモリモデル作成の歴史
   - Double-checked loading の記事が発端
   - data race で undefined な挙動になるなら、そもそもそれを考えずに最適化してもいい（C,C＋＋）の場合
