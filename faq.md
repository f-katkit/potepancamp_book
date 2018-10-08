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

詳しくは[航海に必要な道具を揃える](prepare.md)を見てみましょう。

### bundle installで失敗する

brew installする時にバージョン指定を忘れていた場合、デフォルトでmysql8.0系が入ります。
そのせいでbundle installに失敗するケースがありますので、その対策を書いておきます。

まずは落ち着いてエラーメッセージを読んでみましょう。
もしmysql2 gemのところでエラーを吐いていたら、インストールしたmysqlバージョンが違っている可能性があります。

```
An error occurred while installing mysql2 (0.4.9), and Bundler cannot continue.
```

典型的には `MYSQL_SECURE_AUTH` という定数が見つからないと言うエラーメッセージが出ています。

まずmysqlのバージョンを確認しましょう。

```
$ brew info mysql
```

冒頭の数行の中に、brew installされているバージョンが並びます。
アスタリスク（*）がついている行を確認すると、現在のバージョン番号が読み取れます。

```
/usr/local/Cellar/mysql/5.7.19 (322 files, 233MB) *
```

5.7が入っていれば大丈夫ですので、この先に進まないでください。


＜mysqlバージョンが違った場合の対処法＞

* 必ずバージョンを確認した上でやるようにしてください

* DBを全削除しますので、**他の仕事などでmysqlを使っている場合、大事なデータが削除されます。** 注意してください。

```
brew services stop mysql # 起動していた場合止めておく（失敗した場合は無視して続行）
brew uninstall mysql # mysqlをアンインストールする
brew uninstall mysql@5.7 # もしこのバージョンも入っているようならいったん削除
sudo rm -rf /usr/local/var/mysql/ # mysqlの持っていたdbを全削除
brew install mysql@5.7 # mysql5.7を導入
brew link mysql@5.7 --force # フォースリンク
brew services start mysql
```

これでbunde installが通れば成功です。

### ローカルでサーバー起動中にファイルを編集してもブラウザに反映されない（またはエラーになる）

様々な原因が考えられますが、典型的にキャッシュが悪さをしていることがあります。
ハマりがちで原因が難しいものだけを挙げておきます。

* コントローラ等を編集した際に、 `unknown firstpos: NilClass` というエラーがでる
[eager_loadオプションをtrueにするとこのエラーが出るという報告](https://github.com/rails/rails/pull/32296)があります。
er図を出すなど特定の理由がない場合はデフォルト設定にあわせて、eager_loadを切っておくのがオススメです。
（サーバー起動時に全部のクラスをロードしないため、開発環境で起動が早くなると言うメリットもあります）

* サーバ再起動しても修正が全く反映されない
`rails c` や `rails s` をやり直しても変更が反映されない場合、起動を高速化するためのspring gemが悪さをしていることがあります。
Ruby on Rails Tutorialにも[出ていますが](https://railstutorial.jp/chapters/static_pages?version=4.2#aside-processes)、`$spring stop` コマンドでspringを止め、改めてrailsを再起動することで対応できます。

* CSSを変更してもスタイルが反映されない
ブラウザのキャッシュをクリア（スーパーリロード）すると反映されることがあります（chromeの場合、COMMAND+SHIFT+Rを押す)

## データベースの内容をリセットしたい

下記コマンドで、サンプルデータの再投入をためしてみてください

```text
bundle exec rake db:drop
bundle exec rails g spree:install
```

## solidusのバージョンを確認したい
Gemfile(Gemfile.lock)を見るのが早いですが、gemコマンドも使えます。

```
$ gem list | grep solidus # solidusのバージョンが出る
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
