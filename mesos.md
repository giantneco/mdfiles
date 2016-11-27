
# MESOS 勉強会

## 1. Mesos とは何か by 木内さん (クリエーションライン)

Apache mesos の紹介
 営業支援のエンジニ
 O'reilly Certified Apache Spark <- こういう資格あるのか

Apache Spark と深い関係、どちらもバークレーのAMPLabにて開発

DCOS デーシーオーエスと読む

スケーラビリティ
 １０，０００ノードまでの拡張性を前提に設計
  ジョブの自動再起動、繰り返し実行
  日時指定実行、実行回数制限をサポート
  ジョブ監視、異常終了時の自動再実行

リソースを束ねる方向を重点に置いている

HPC的なジョブスケジューラとは違う、YARNとも違う

DOCKERコンテナをネイティブサポート
 ジョブに応じて動的にじっこうかんきょうを切り替えられる

YARNはHADOOP用ジョブスケジューラ
 どちらかというと OpenPBS,Torque などとひかくするのがよい

Mesos Slave , Mesos Master = Zookerper , ジョブスケジューラ、 サービスディスカバリ、 APP の順でスタックされているｋ

Mesos マスタ上で動くフレームワークを拡張できる
自作フレームワークをつくれる

Mesos はクラスタのクラスタになることができる。クラスタを管理できる

Dockerとの統合をサポート

海外事例
 ｔｗｉｔｔｅｒ  １２００
 ａｉｒｂｎｂ ４０，０００コア

 使われ方が結構違う

 最近だとアップル、マイクロソフトも
  Ａｚｕｒｅで使えるようになっている、ただしＡｚｕｒｅだとＤＣ／ＯＳも選択可能に

理化学研究所のＦＡＮＴＯＭ５とかでも採用

## 2. Docker ホスティングサービス 'Arukas' での Mesos + Marathon の活用について by 山田 修司 さん(さくらインターネット)

＠ｕｚｙｅｘｅ

What's Arukas ?
 Docker のデプロイするサービス？
   ＤｏｃｋｅｒＨｕｂからＰＵＬＬしてきて簡単に構築

Zookerper == KVS?

Mesos Master, Mesos Slave

Framework = Scheduler + Executor

Marathon = a Mesos Framework

監視は ＤＡＴＡＤＯＧ

Ｑ ＭｅｓｏｓはどうやってＩＳＯＬＡＴＩＯＮを確保している？ リソース制御
 Ａ Ｍｅｓｏｓはしない。ＤＯＣＫＥＲ側で確保している。ｃｇｒｏｕｐなどを使用する

## 3. Mesos に GPU を食わせてみるテスト ～2016夏～ by 須藤さん (さくらインターネット)
## 4. Mesos Frameworkの作り方 by 上西さん (ノーチラス・テクノロジーズ)

Mesos Framework の作り方

Mesos distributed system kernels
 抽象化
 カーネルだけではなにもできない

memso framework はカーネルに対するユーザランドプログラム
 API叩いてどうにかする

 master から framework scheduler をたたく scheduler API
 framework scheduler が master をたたく scheduler driver API

Framework つくらないと mesos を使い切ったとはいえない
 Scheduler を継承してコールバックをたす
 Scheduler Driver API を呼び出す
 Executor を継承してETC
 Executor APIをたたく

## 5. IaaSの実装をフルスクラッチした人が思う、もうMesosで良いじゃんって話 by 山崎 泰宏さん (Axsh)


























ｅｎｄ
