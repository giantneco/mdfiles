# ML 勉強会
 - 2016/07/09
## ATSで捕捉されたリアルタイムOSのシステム状態	masterq
## Socket on SML#	κeen

SML#
@balckenedglod

SML#,
 最近 JSON サポート

ソケット
 ソケットアドレス
   複数のアドレスファミリ
 ソケット
   プログラムからはFD

## コンピュテーション式とprintfで作るlogging（仮）	もみあげ
## ML-userのためのCoq入門	tmiya_

Coq 入門

 対話的定理証明系
  not モデル検査機
  証明できるかは人間次第
 用途
  数学・計算機科学の定理証明
  プログラム仕様の検査
   高階述語論理で使用記述
   依存型でプログラム記述
  Coq → OCaml のコード生成
 依存型を用いてプログラミング可能
  構文はMLっぽい
  型推論は完全でない
  停止性は保証する必要がある。Coqはチューリング完全ではない
 証明は対話的に構成
  自動化するスクリプトもかける
 Curry-Howard 対応
  直観主義明大論理 <=> 型付きλ計算
  述語論理 <=> 依存型


Peano の自然数の定義

 Inductive nat : Set :=
   0 : nat
 | 1 : nat -> nat.

リストの定義

Inductive list {A : TYpe} : Type :=
...


簡単な例
map が length を保存する

 Goal forall (A B : Set) (f: A-> B)(xs" list A),
   length(map f xs) = length xs.
 Proof.
 intros; induction xs; siml; auto
 Qed.



Why3
 MLぽい中間言語
  事前・事後条件から Coq などへの証明課題を生成

論文： "Coq: The world's best macro assembler?"
 Coq 上で　x８６ 命令の定式化をした。マクロもある
 x86命令実行はマシン状態に関する　state monad で定義
 正規表現 -> DFA -> X86機械語、コンパイラを作って正しさを証明

Coqの学び方
 Coq'Art は古いし高い。そすすめしない
 ネット上にわかりやすい教材はたくさんある
 対話証明系なので動かしてみるのがいい
 自習用教材は名古屋大学の　Garrigue 先生が公開している教材がおすすめ

 そのさき
  TALP的なこと Pierrce の ソフトウェアの基礎
  Coq Winter School 2016


## 関数型言語処理系の検証（特にCakeML）のサーベイ	ろんだ
信用できる言語 Standard ML @fetburner

compcert [Leroy etc 2006]
 言語処理系懸賞のマイルストーン
  実用的なCコンパイラの検証
   ANSI C の大部分をサポート
 大部分をCoqで検証

ML処理系を検証する試み
  Lmabda Tamer [Clipala 2010]
  Pilsner [ Neis 2015]
  CakeML [ ]

CakeML
 実用的なStandard ML処理系の検証
  ブートストラップにも成功
   ARMｖ６、などのネイティブコードを出力
  HOL4 による執拗なまでの証明


対象言語
 Standard MLのサブセット
副作用
 参照
 例外
ヴァリアント
パターン
モジュール

なぜ Standard ML か？
 言語使用が厳密に定義されている

パーサーはPEG


## OCaml の線形代数ライブラリ SLAP の紹介	あっきー ＠ackey_65535

Sized Linear Algebra Package チュートリアル

## 型推論器と現実	インターネットの闇

OCamlの型推論アルゴリズム



## Macrodown -MLが使えるML-	bd_gfngfn

@bd_gfngfn
