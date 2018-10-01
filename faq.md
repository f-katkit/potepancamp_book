# ＦＡＱ

行き詰った場合は "[行き詰まったら](kimattara.md)" も参照してみてください｡ またここにない話でも､slackの過去ログを掘ると解決策があるかもしれません｡

## all.jsが無いと怒られる

下記のコマンドでデータを再導入するとよいでしょう

```ruby
bundle exec rake db:migrate:reset
bundle exec rails g spree:install # ここが失敗するとall.jsが導入されない
```

### テーブル構造を図示したい

`rails-erd` というer図を吐き出してくれる便利なgemがあり､すでにGemfileに登録されています｡

```ruby
brew install Graphviz
bundle exec erd
```

これで､er図がpdf出力されます｡\(productionに必要ないデータなので､gitにかからないようにしておきましょう\)

## データベースの内容をリセットしたい

下記コマンドで、サンプルデータの再投入をためしてみてください

```text
bundle exec rake db:migrate:reset
bundle exec rails db:seed
bundle exec rails spree_sample:load
```

## モデルやコントローラーをチューニングしたい （例 scopeを使いたい等）

solidusが持っているモデルやコントローラーをオーバーライドする方法はこちらによくまとまっています｡

[http://qiita.com/yuskamiya/items/32f383cb8d18ceb751d7](http://qiita.com/yuskamiya/items/32f383cb8d18ceb751d7)

solidusを分析する方法については､ "[ソースコードリーディングを進めるコツ](if_you_get_stuck.md)をまとめましたので､そちらも参照してみてください｡

## SSH設定について

リポジトリのアクセスを安全かつ便利に行うために､アカウント設定で公開鍵を登録しておきましょう｡

まだキーがない方は､

```bash
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

でキーを生成しましょう｡
