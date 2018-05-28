# はじめに

ここではまず最初にやってほしいことを並べておきます｡

（環境構築､solidusの設定などはリポジトリのトップページにある解説を参照してください）

## 最初にやること

まず下記の3つに招待してもらってください｡

### 1. Slackのポテパングループに入る ※招待

### 2. 下記のチャネルに登録 ※招待

'\#question' '\#potepancamp'

### 3. bitbucketのポテパンリポジトリにアクセス ※招待

すべて終わったら･･

### bitbucketでとりあえずやること

#### リポジトリをフォーク

* リポジトリをクローンできない場合
  * git clone...の対象を自分にしていない（コピペするとき注意）
  * 公開鍵を設定できていない

どちらかが多いです（ありがちな失敗）

下記メールアドレスに対して権限をあたえてください （READでよい）

* motchang@gmail.com
* fursich0@gmail.com
* hachihachi.8og@gmail.com
* kujasho@gmail.com

#### フォークした個人アカウントリポジトリを公開にする

設定＞リポジトリの詳細＞アクセスレベルでチェックをオフにして保存する。 （転職時に担当の方にプルリクを見てもらうためオープンにする必要があります）

### 開発環境

リポジトリをフォークしたら説明が出るはずなのでそちらを参考に､インストール､設定作業をしてください｡

### 開発

チケットを２番から順番にこなしていき､実装したタイミングでプルリクエストを立ててください｡

* 【重要】マージ先を共有レポジトリにしない
  * 自分のリポジトリのmasterブランチへマージをかけるようにしてください
* レビュアーを指定
  * 対象は､`kouji okamoto` と `koji onishi` と `palm sakamoto` `atsushisaito`でお願いします｡
* もしできれば･･
  * ｢説明｣のところに下記の情報があるとレビューで答えやすい感じです｡
    * チケット番号と概要
    * とくに見て欲しいポイントがあれば
    * 相談したいこと（とりあえず実装したけど､もっといい方法はないのか･･等）
    * 工夫した点（ドヤ）
* `#potepancamp`チャネルに､作成したプルリクのアドレスを加えて､@kouji.okamotoと､@kojiにメンションしてください｡
* なるべく数日中に見ます｡週末が近いとキャンプで直接フィードバックをもらうことになる確率が高いので､お早めにドゾー｡

### つまったら

`#question`チャネルに投げてください｡

* 質問を立てる時になるべく留意して欲しいこととしては･･
  * 問題の起きた状況がわかりやすいと､回答者が状況を再現しやすい
  * 答えて欲しいことが明確な方が､回答者が的を絞りやすい
  * すでに試してダメだったことがあると､より少ないやり取りで欲しい答えを出せる

こんな感じだと､早めにいい回答が寄せやすいかなと思います｡

（いちおう簡単な方針をチャネルの過去ログに書いていますのでご参考に）

文字ベースの質問を立てにくいくらいつまってしまった時は､ キャンプ会場にて直接ぶつけてみてください❗

