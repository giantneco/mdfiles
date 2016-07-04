# システムプログラミング会

## LLD NEW LINKER

windows 上でリンクできるようにしたい
 もともとのモチベーション

コンパイラとかデバッガとか移植しないといけない

オープンソースなのでUNIXに移植しよう

GNU でないといけないのはリンカぐらいしかない
 BSDは移行したい
 BUILD WORLD とかは動く

MIPSに対応
 MIPS は ELF なんだけど MIPSのELF になっている
   一部リトルエンディアンで一部ビックエンディアンとか
 GNU リンカーのソースコードを見ないとわからない状態

  icf
    identify content folding
    ふつうは名前でまとめるが、このオプションをつけるとコンテンツをまとめてフォールディングする

    基本的ンはグループ分けして内容が違ったら分割、リロケーションがさしている先が同じだったらまとめる
     平衡に達したらマージ可能なグループになる

余計なことをしないことを主眼においている

LLDではかなり変えていて、ファイル渡す順序によらずシンボルを解決している

ファイルサイズはかなり小さくできている。
 C＋＋で10,000ぐらい。

リンク時の名前解決
 ハッシュ使用
 少なくとも１回はハッシュを使う 名前解決のため
  ハッシュに名前を入れるのも結構時間がかかる
   C++だと関数が５０バイトくらいなっていたり
 名前の変更がポインタの変更になっている

 別のファイルを読んだときに、すでにハッシュキーがあったらのそさす先を書き換えて内容を変えたことにする

  ld で wrap オプションを渡すと、malloc は __wrap_mallock にリンカされる。
  もとのmallocは __real_mallocで参照可能になる

LLVM
 Link Time Optimization (LTO)
 グローバルなビューをリンカはもっている。
  LLVMはバイトコードをもっているので、リンカが名前解決をするときに
  そのバイトコードを使ってネイティブコードに落とす （よくわからん）

今後の目標。 FreeBSDで普通に使う。カーネルのビルド。

ハッシュ関数
 早くするために何かしているか？
  －＞普通のハッシュ関数を使っている
   はやくしたらというアイディアはある
    キーはぬるたーみねーテッドなものなので、STRLENで結構時間を食っている
     長さを渡してあげれば？

## Kati

http://shinh.skr.jp/slide/kati_sp/031.html

ビルドシステム

 Android Platform
  アプリ開発者というよりデバイス開発者向け
  結構でかい
  普通にmakeをつかっている

Android.mk
 GNU makeのチューリング完全性を悪用して謎DSLをつかっている

## 原語処理系の話

＠Lind_pp

LLVMとC＋＋でコンパイラフロントエンドつくった

プログラミング言語 Dachs

## なんかトレースする話

https://speakerdeck.com/naruse/nankatoresusuruhanasi

perf top <- 楽しい

## Unix Domain Socket

UnixDomainSocket ふるまいは多様（）
APIが腐っている

## L1キャッシュ

Radix Sort

O(N) なソートアルゴリズム
 iwiwi 経験上一番早い

 SoftWare Write Combining
  CPU の書き込み先メモリアドレスを絞り、L1キャッシュに乗せられるようにする
  Intel のマニュアルに書いてある

Radix Sort with SWWC

## StackExchangeでみたシステムプログラミング案件

## オレオレOS

オレオレOSスケジューラ

## Rem

## Out-of-thin-air

メモリモデル咲く知恵の歴史
 Double-checked loading の記事が発端

data race で undefined な挙動になるなら、そもそもそれを考えずに最適化してもいい
 （C,C＋＋）の場合
