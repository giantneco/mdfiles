# LLoT

## Language Update

### Java 高橋徹

標準パッケージおおきい
１０年に一度大きな変更

互換性のポリシー
 DEPRECATE はあるが、削除されたAPIはない
 とりわけ標準APIは変更していない

Classic VM １．３まで
HotSpot VM


JavaSE8 での言語使用アップデートの紹介
言語仕様
 λ式、InterfaceへStatic/Defaultメソッド
 タイプアノテーション

 ラムダ式
  インターフェースのインスタンスを生成

 インターフェースへの実装
  デフォルトメソッド
   メリット） 既存のインターフェースにメソッドを追加しても壊れない
          脆弱な基底クラスへの対策
 JavaFX
  かっこいいGUI

 Script言語とお友達に
  JavaScriptが標準搭載に jjs コマンドで JavaScript を実行

### PHP @hnw

近頃のPHP界隈の話

PHP7 速いよ！
 １０年ぶりのメジャーバージョンアップ
 ほかの言語ならマイナーバージョンアップ相当
 内部実装の大変更
 後方互換はかなり維持

何を高速化？
 PHP 基本型のデータ構造を見直し
  データサイズへらす キャッシュ効率向上 メモリの動的確保回数など
   メモリマネージャ効率化

特徴的な取り組み
 WordPressをベンチマーク対象にした
  これまでマイクロベンチしかなかった
  この高速化をしていいかという指針に
高速化チームに一定の裁量
 過去にできなかった大変更を実現できた

 PHP ７．１リリースへ
  目立った変更点
   型の強化（void, nullable, iterable)
   mt_rand()がほかの言語と同じ挙動になる
    MT_RAND_PHPを設定すれば以前の挙動に

エコシステム定着
 PHPにはエコシステムがなかった
 ここ数年でComposerの利用が定着

 参加者を増やしつつ破たんしない仕組み
   ユーザ名パッケージ名で登録
    早い者勝ちを防ぐ
  対応するGitHub/BitBucketのURLを登録する

開発支援環境の普及
 PHPStorm が増えている印象
DocCommentを利用して型を利用

ほかの言語の当たり前が入ってきている
 array/list を [] で書ける
 Trait
 etcetc

地方コミュニティが活発に
 意外と集客できている

### Perl

Perl 6

仕様の一部を満たす実装が出てきた

Rakudo Perl6

kinoutekiniha 2015/12にいったんフリーズ
実装を治すフェーズに
最適化やバグ取り中

Rakudoの実行環境
現時点で対応しているのは MoreVM のみ
JVM上では一部機能が欠けた状態
Perl６の土台となっていた Parrot はついに完全引退
JavaScript バックエンド

RakudoStar
 Rakudo本体にモジュールなどを同梱

Perl5
 ５．２４ 安定板

autoderef は廃止 postderef が導入

### Python @hirokiky

3.4 -> 3.5

Type Hinting が公式に入った
  Python 標準で型を明記できる
  Python自体には制約を与えない
   チェックツールでよしなにして

  ```
   def add(a: int, b: int) -> int:
       return a + b
  ```

  intである場合は int に紐づけられたメソッドをIDEがサジェストしてくれたりする

TypingModule

 typing.Optional

 Union、List,Iterable

 typing
  3.5 ではただのヒント
  3.2 からの後方互換を維持しているのはすごい
  3.2 からは pip install typing をすればいい

他
 async (async def, async for ) await構文
 行列計算演算子 @


### JavaScript @teppeis
ECMAScript

ES2015
  5年ぶりアップデート
   モダンな言語にある機能がいろいろはいった

 機能追加は２つだけだが、毎年アップデートされるようになったのが重要

  毎年６月に es20xx としてリリース

  async Functions

   ES Modules
    周辺仕様で大激論中

### Ruby @takahashim

2.4.0 preview 1 がリリース
 インストール
  ソースからビルド
  rbenv 用の preview を使う

2.4 の変更点
 基本的に地味
 派手なのは３．０に期待

 Fixnum と Bignum が Integer に統合
  普通に使う分には問題ないが、C拡張ライブラリが死ぬ

 String＃downcase,upcase,capitalize のUnicode対応

 後置 rescue の構文
  挙動の変更？

 Enumerable#sum, Array#sum
  2.4 から標準に
  浮動小数点数の情報落ちがないアルゴリズムに

 Regexp#match の導入

## キーボード

## Dynamic Typing 再考

サイボウズ
 JavaScript は Clojure Script で型付きにして運用

動的型付けとはなにか？
 動的に検査される
 性的に検査されない
 型が弱いわけではない

静的型付けVS動的型付け

### JavaScript

AltJS 乱世の生き残りは『型』
 まだ標準に入っていない
  TypeScript,Flowtype,Closure Script
 便利機能は本体に吸収された
 JavaScript での大規模開発が一般的に
 ブラウザではJS以外の選択肢がない

TypeScript 後置修飾
ClosureScript JSDoc
Flowtype 後置修飾 と JSDoc

型を標準に入れるという話も(かつて)合った
 Typing in ECMAScript

## Ruby

matz 型付け言語が嫌いなわけではない

ruby
 DRY
 duck typing

型はなくても動くので冗長＝＞DRYに反する

Ruby3 で静的な型チェックはやりたい。型は書きたくない
 型を書くのは人間には難しすぎる

２０２０に出ていればいいな

erlang という言語 dyalizer? 型検査するツール

## SmallTalk

# Kotlin vs Swift

## Kotlin

特徴
 簡単
 Interop
 Android
 安全 型安全 NULL安全

































# END
