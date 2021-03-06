# はじめに

## ポテパンキャンプ課題資料ライセンス

[![&#x30AF;&#x30EA;&#x30A8;&#x30A4;&#x30C6;&#x30A3;&#x30D6;&#x30FB;&#x30B3;&#x30E2;&#x30F3;&#x30BA;&#x30FB;&#x30E9;&#x30A4;&#x30BB;&#x30F3;&#x30B9;](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)  
この ドキュメント は [クリエイティブ・コモンズ 表示 - 非営利 - 継承 4.0 国際 ライセンス](http://creativecommons.org/licenses/by-nc-sa/4.0/)の下に提供されています。

## 最初にやること

ここではまず最初にやってほしいことを並べておきます｡

（環境構築､solidusの設定などはリポジトリのトップページにある解説を参照してください）

まず下記の3つに招待してもらってください｡

_講師陣からのお願い：slack と gitbucket のアカウント名を一致させておいていただけると大変助かります。_

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

#### フォークした個人アカウントリポジトリを公開にする

設定＞リポジトリの詳細＞アクセスレベルでチェックをオフにして保存する。 （転職時に担当の方にプルリクを見てもらうためオープンにする必要があります）

### 開発環境

リポジトリをフォークしたら説明が出るはずなのでそちらを参考に､インストール､設定作業をしてください｡

### 環境設定で大切なこと

最初の環境構築時に大切なのは **「おかしいな」と思ったら、引き返せるところでやめること** です。

もっともハマるパターンは、環境設定の間違いをなんとかしようと意地になって、わからないことを色々試すことです。

根拠の怪しいネット記事を参考にしてOSのライブラリなどを直接変更する、などというケースです。

以下に泥沼にはまらないためのTIPSをあげておきます

* 打ったコマンドの内容を全て記録しておく
* エラーメッセージらしきものが出ていたら無視しないで読む
* この操作は元に戻せるのかどうか？ということを常に気にかけておく
* うっかりハマったら中止して、早めに質問を投げる

よく起こりがちなエラーについては、[ＦＡＱ](faq.md)を読むと解決方法が書かれてることがあります。
解決の参考にしてみてください。

蛇足ですが、環境構築が終わって実際のアプリケーション開発に入ったら、 **自力解決する力が大切** です。

git管理されているRailsのアプリ上だと、多少のことをやったとしても簡単に復帰できます。
どんどんハマって戦ってみて、経験値を伸ばしていってください。

### 開発

チケットを２番から順番にこなしていき､実装したタイミングでプルリクエストを立ててください｡

* 【重要】マージ先を共有レポジトリにしない
  * 自分のリポジトリのmasterブランチへマージをかけるようにしてください
* もしできれば･･
  * ｢説明｣のところに下記の情報があるとレビューで答えやすい感じです｡
    * チケット番号と概要
    * とくに見て欲しいポイントがあれば
    * 相談したいこと（とりあえず実装したけど､もっといい方法はないのか･･等）
    * 工夫した点
* `#potepancamp`チャネルに､作成したプルリクのアドレスを加えて､@here宛てにメンションしてください｡slack上のbotが自動でPRのレビュー待ちに加えていきます（botからの自動返信を必ず確認してください）

### つまったら

こちらを見るとヒントがあるかもしれません。

* [行き詰まったら](guidelines/getting_stuck.md)
* [ＦＡＱ](faq.md)

その上で解決できない疑問があれば、レビュー会場で質問するか `#question`チャネルに投げてください｡

なお、課題の実装に関する具体的な質問については、**`#question` ではお答えしていません。**

一度WIPとしてPRを立て、`#potepancamp` チャネルに投げていただければ、通常のPRと同じくレビュアーが見ていきます。

### 質問を立てる場合

これは開発現場でもOSSでもそうですが、 **バグの再現性** がもっとも重要です。

問題の起きた状況を回答者が再現できると、解決策を見つけやすいです

  * いままでうったコマンドの一覧や、書いたコード（講師がエラーを再現するためのコード）
  * エラーメッセージの内容
  * すでに試してダメだったこと、自分なりの仮説

こういう情報をいただけると､早めにいい回答が寄せやすいかなと思います｡
例えば「何もしてないのに画面がおかしくなりましたがどうすればいいですか？」という質問だけもらっても、状況がつかめずどうにも回答ができません。

とはいえ、文字ベースだと質問を立てられないくらいわからなくなってしまった時は､ キャンプ会場にて直接ぶつけてみてください❗
