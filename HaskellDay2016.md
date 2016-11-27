# Haskell Day 2016

## Haskell Relational RecordComposable , TYpesafe SQL Building
- https://htmlpreview.github.io/?https://github.com/khibino/haskell-relational-record/blob/master/doc/slide/Haskell-Day-201609/HRR.html
- Kei Hibino

Haskell で式を書くと SQL に変換される

Concepts
 式を組み立ててその時に型チェック
 コンパイル時にスキーマ情報を￥読み取って型チェックに使いたい

## Introduction to Web Development with Spock
  lotz

Spock は Haskell の軽量フレームワーク。RubyのSinatoraにインスパイアされている

## Introduction to Stack's Docker Integration
@igrep

stack docker integration
 build production environment

stack docker integration
 docker command wrapping
 Set up GHC,and so on

how to use
 stack.yaml
```
dockder:
  enable: true
```

Case study

 - tiny mock srv er
 -
   - must run on old environment

 - use spock

## HTTP2 with Warp

Warp - High Performance HTTP server  Library in haskell

## SAT/SMT

SAT

SMT
 satiisfiability Modulo Th



## Into the core squeezing Haskell into nine constructors
 Simon Peyton Jones Microsoft Research

Simon Peyton Jones Haskell の父

関数豪税を中間言語に落とすと、型注釈がうまくいかない
```
compose (b->c) -> (a->b) -> a -> c
```
上の例だと、a,b,c に型注釈をつけられない
あくまで束縛は （(b->c) に対して行われている

そこで systemF

型の情報も引数として関数に渡す形にする


ghc -c Foo.hs -dshow-passes
ghc -c Foo.hs -ddump-simpl

users can write more RULES

```
{-# RULE
  "foldr/builld" forall k z g.
     foldr k z (build g) = g k z
#-}
```
compiler generete rewrite rules

$ mark <- genereted by compiler
