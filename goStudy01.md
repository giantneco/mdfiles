Go 言語勉強会 第1回
==================
----
# 今回の範囲
おおよその基本部分をカバー
- 第1章 チュートリアル
- 第2章 プログラム構造
- 第3章 基本データ型
- 第4章 コンポジット型
- 第5章 関数
- 第6章 メソッド
---
# ファイルの構造
```go
// 最初にこのファイルがどのパッケージの一部であるかを示す
// package 宣言
package main

// fmt パッケージのインポート
import "fmt"

// 型の宣言
type newInt int32

// 定数or変数の宣言
const c = 10

// 関数の宣言
func main() {
  var f = c
  fmt.Printf("f is %T\n", f)
}
```
---
# 変数宣言
```go
var name type = expressoin
// 型の省略
// 型省略時は右辺の型になる
var name = expression
// 初期化式の省略
// 初期化式省略時は「ゼロ値」が初期値になる
var name type
// 省略変数宣言
name := experssion
// 同じ型の宣言はまとめられる
var name1, name2 type
```
- 宣言した変数の生存期間
  - 到達可能である間は変数は生存し続ける
  - ある関数のローカル変数がヒープかスタックに作られるかはコンパイラが判断する
---
# 名前
- ユニコードで文字とみなされている音のすべて
- アンダースコアで開始することができる
- 数字も使えるが先頭には使えない
- 予約語あり
- 大文字・小文字の区別あり
---
# 代入
```go
// 普通の代入
a = 1

// タプル代入
// この式は値のスワップになる
a, b = b, a
```
---
# 基本データ型
  - `int`, `int8`, `int16`, `int32`, `int64`
  - `uint`, `uint8`, `uint16`, `uint32`, `uint64`
  - `rune`, `byte`
  - `float`, `float32`, `float64`
  - `complex64`, `complex128`
  - `bool`
  - `string`
  - `uintptr`
異なる型同士の演算には明示的な型変換が必要
---
# 名前付き型
```go
type double float64
```
- `type`構文で名前付き型(_named type_)を定義可能
- 基底型(_underlying type_)と区別される
---
# ポインタ
アドレス化可能なもの、例えば変数に対してポインタを作ることができる
```go
v := 1
p := &v

// new 関数
p := new(int)

func f() *int {
    x := 10
    return &x
}
```
- 関数 `f` のローカル変数はコンパイラによってヒープ側に置かれる
---
# パッケージ
```go
package main

import (
     // 一意なインポートパス(_import path_)
     // でインポートするパッケージを決める
    "path/mypackage"
)

func main() {
    // 「パッケージ名.」でパッケージの内容を参照できる
    res := mypackage.function()
}
```
 - 1 つのファイルは １ つのパッケージに属している 
 - 1 パッケージは 1 つ以上のファイルからできている
 - パッケージの初期化
   - パッケージレベルの変数は依存関係を解決してくれる
   - 複雑な初期化が必要な時は`func init() {/* ... */}` を定義
 - インポートしたパッケージを使用しないのはエラーとなる
---
# 制御文
- `if 文`
- `for 文`
- `switch 文`
---
# `if 文`
```go
// Go 言語の if は初期化式を含めることができる
if x := f(0); x == 10 {
    fmt.Println("x is 10")
} else if x == 5 {
    fmt.Println("x is 10")
} else {
    fmt.Println(x)
}

// 初期化式を使わない場合
x := 10
if x == 10 {
    fmt.Println(x)
}
```
---
# `for 文`
```go
// 初期化式 + 条件式 ＋ 変化式
for i := 0; i < 10; i++ {
    /* */
}

// 条件式だけ
for i < 10 {
    /* */
}

// 条件式も書かなかった場合は無限ループになる
for {
    /* */
}
```
---
# `switch 文`
```go
switch coinflip() {
case "heads": // フォールスローはしない
    heads++
default: // default はどこに書いてもよい
    fmt.Println("landed on edge!")
case "tails":
    tails++
}

x := 100
switch { // オペランドは省略できる
case x > 10:
    fmt.Println("Large")
default:
    fmt.Println("Small")
}
```
---
# スコープ
- ユニバースブロック(_universe block_)
  －ソースコード全体
- レキシカルブロック(_lexical blocks_)
  - `{}` で囲まれた部分
  - `if`、`for`の初期化式部分も暗黙のスコープを持つ
---
# コンポジット型
- 配列
- スライス
- マップ
- 構造体
---
# 配列
```go
a := [3]int{1,2,3}
b := [...]int{1,2,3}

// 要素が比較可能なら同じ長さの配列は比較可能
fmt.Println(a == b) // "true"
```
- すべての要素が同じ型の固定長配列
- 配列アクセスは 0 オリジンのインデックスで行う
- ゼロ値は各要素がゼロ値の配列になる
---
# 配列操作
```
s := [6]int{0, 1, 2, 3, 4, 5}

// 要素へのアクセス
a := s[0]
// 要素への代入
s[0] = 1
// 要素へのポインタ
p := &s[0]
// すべての要素にアクセス
for i := range s {
    /* */
}
```
---
# スライス
```
s := []int{0, 1, 2, 3, 4, 5} // スライスリテラルによる宣言

// スライス演算子を使った宣言
t := s[0:2]
u := s[3:]
v := s[:3]
w := s[:]
fmt.Println(t, u, v, w)
// -> "[0 1] [3 4 5] [0 1 2] [0 1 2 3 4 5]"
```
- `スライス ≠ 配列`
- すべての要素が同じ型の可変長配列
- スライスは要素が比較できるものであっても比較できない
- スライスのゼロ値は `nil`
---
# スライス操作
```
s := []int{0, 1, 2, 3, 4, 5}

// 要素へのアクセス
a := s[0]
// 要素への代入
s[0] = 1
// 要素へのポインタ
p := &s[0]

// すべてのスライス要素にアクセス
for i := range s {
    /* */
}
// 要素追加
s = append(s, 6, 7)
// スライスの結合
s = append(s, ...s)
```
---
# マップ
```go
// map のデータ構造は隠蔽されているので、
// 組み込みの make 関数を使って初期化する
m := make(map[string]int)

// ゼロ値は`nil`なのでこれはエラーになってしまう
var a map[string]int
a["a"] = 1

// マップリテラルを使った場合
age := map[string]int {
    "alice":   31,
    "charlie": 34,
}
```
---
# マップ操作
```
m := make(map[string]int)

// 要素への代入
m["a"] = 1
// 要素へのアクセス
a := m["a"]
// 要素へのポインタ...はできない
p := &m["a"]

// すべての要素にアクセス
for key, value := range m {
    /* 実行するごとに順序は変わる */
}
```
---
# 構造体
```go
type Point {
   X float
   Y float
}
p0 := Point{1.0, 2.0}
p1 := Point{X: 1.0, Y: 2.0}
p2 := Point{} // 初期値を省略した場合フィールドはゼロ値になる

q0 := &Point{1.0, 2.0}
q1 := new(Point) // new(Point{1.0, 2.0})はできない
```
- 大文字から始まるフィールドは*パッケージ外*から見える
- 初期化時に
  - フィールド名指定なしの場合は一部だけ省略はできない
  - フィールド名指定ありの場合は一部だけ省略できる
---
# 構造体操作
```go
type Point {
   X float
   Y float
}
p := Point{1.0, 2.0}
q := &Point{1.0, 2.0}

// フィールドへの代入
p.X = 1
// フィールドへのアクセス
a := p.X
// ポインタの場合も同じドット記法を使う
b := q.Y
// フィールドへの代入
p.X = 1
// フィールドへのアクセス
a := p.X
// ポインタの場合も同じドット記法を使う
b := q.Y
```
---
# 構造体の埋め込み
- OO でいうコンポジション
```go
type Point2D {
   X float
   Y float
}
type Point3D {
   Point2D
   Z float
}

// 初期化
p = Point3D{Point2D{1.0, 2.0}, 3.0}
p.X = 1
a := p.X
```
---
# 関数
```go
func name(parameter-list) (result-list) {
   body
}
```
Go の関数は
 - ファーストクラスのオブジェクト
 - 再帰呼び出し
 - 無名関数
 - 複数返り値
 - 可変引数
   - スライスとして関数に渡される
---
# 関数の例
```go
func f(a int) (res int) {
    // result-list の変数への代入で返り値を設定
    res = a + 1
    return
}
// 多値の返り値
func g(a int) (int, int) {
    return a, a
}
// 返り値の変数なしかつ多値でない場合は () を省略可能
func h(a int) int {
    return a, a
}
// 返り値のない関数
func i() {
    return
}
```
---
# 関数のエラー
```go
func name(parameter-list) (result-list) {
   body
}
```
- `golang`で関数が失敗した場合には`error`インターフェースを返り値の一つにするのが慣例となっている
---
# 関数の遅延呼び出し
```go
var mu sync.Mutex
var m = make(map[string]int)

func lookup(key string) int {
    mu.Lock()
    defer mu.Unlock()
    retrun m[key]
}
```
- `defer`をつけて関数を呼び出すと、`defer`文がある関数を抜けるときに、指定した関数が必ず呼ばれる
- `defer`は FILO。後に書いた`defer`が先に実行される
- `panic`したでも呼び出される
---
# panic と recover
```go
func f(x int) {
	if x == 0 {
		panic("input is 0")
	}
}

func main() {
	defer func(){
		if r := recover(); r != nil {
			fmt.Println("catch panic")
		}
	}()
	f(0)
}
```
- 他の言語でいう例外に近い
- 例外と違い、`recover`したところから再開
- 外部に公開するAPIで`panic`を投げるべきではなく、あくまで内部だけで使うのが望ましい
---
# panic と recover の使用例
```go
func f() (v int) {
	defer func(){
		if r := recover(); r != nil {
			v = 1
		}
	}()
	panic("input is 0")
}
```
- 練習問題にあった、`return`を含んでないのに、ゼロ値ではない値を返す関数の例
---
# メソッド
```go
// Point 構造体のメソッド
func (p Point) Distanc(q Point) float64 {
    return math.Hypot(q.X-p.X, q.Y-p.Y)
}

p := Point{1,2}
q := Point(3,4)

// 呼び出すときはドット記法を使う
fmt.Println(p.Distance(q))
```
---
# ポインタに対するメソッド
```go
func (p *Point) Distanc(q Point) float64 {
    return math.Hypot(q.X-p.X, q.Y-p.Y)
}

p := &Point{1,2}
q := Point(3,4)
r := Point(5,6)

fmt.Println(p.Distance(q))
fmt.Println((&r).Distance(q))

// Pointレシーバーがアドレス化可能なら
// コンパイラの方で`&`を足してくれる
fmt.Println(r.Distance(q))
```
---
# `nil`に対するメソッド呼び出し
`nil`も正当なレシーバ値になっている
```go
func (list *IntList) Sum() int {
    if list == nil {
        return 0
    }
    /* */
}
```
---
# 構造体埋め込みに対するメソッド
```go
type Point2D {
   X float
   Y float
}
type Point3D {
   Point2D
   Z float
}
func (p Point2D) Distance(q Point2D) float64 {
    return math.Hypot(q.X-p.X, q.Y-p.Y)
}

p := Point3D(Point2D(1,2), 3)
q := Point3D(Point2D(4,5), 6)

fmt.Println(p.Distance(q.Point2D))
fmt.Println(p.Distance(q)) // こちらは NG
```
- 埋め込まれた高オズ隊のメソッドを呼び出すことが可能
- 一方で引数に関してのポリモーフィズムはない
---
# 質問タイム