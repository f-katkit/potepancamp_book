# Dockerを使いこなそう

Dokcerは近年急速に普及しているコンテナ型仮想化技術です。

開発環境においては、手軽にコードベースで開発環境を共有するためにも利用されています。

ポテパンの課題ではDockerを利用した開発環境を準備しているので、課題を通してDockerを使った開発にも慣れておきましょう。

## Docker Composeの基本操作

複数のコンテナが連携している開発環境を構築するためにポテパンの課題ではDcoker Composeを利用します。
ここでは開発に利用するDocker Composeの基本操作を説明します。

### docker-composeの設定を参照する

下記のコマンドでプロジェクトで利用するdocker-composeの設定を参照することができます。
なお、この内容はプロジェクトルートディレクトリの `docker-compose.yml` で設定されているものです。

```bash
docker-compose config
```

### docker imageをビルドする

Dockerではコンテナイメージを利用してコンテナを起動します。
開発環境に必要なコンテナイメージをビルドするには下記のコマンドを利用します。
Dockerの公式リポジトリである [Dockerhub](https://hub.docker.com/) に登録されているコンテナイメージをそのまま利用するサービスはビルドされません

```bash
docker-compose build
```

### docker-composeを起動する

下記のコマンドで必要なコンテナを起動し開発環境を構築します

```bash
docker-compose up
```

後ろに `--build` オプションをつけると `docker-compose up`の前に `dokcer-compose build` を自動的に走らせることもできます

```bash
docker-compose up --build
```

### docker-composeで起動しているコンテナを確認する

```bash
docker-compose ps
```

このコマンドでdocker-composeで起動しているコンテナの情報を参照することができます
開発用のコンテナが正常に起動ができていれば、３つのコンテナが起動しています。それぞれ、`mysql` `rails` `redis` を担当しているコンテナです。

### railsを起動しているコンテナ内で特定のコマンドを実行する

コンテナ外から起動中のrailsコンテナ内でコマンドを実行するには下記のコマンドを利用します。

```bash
docker-compose exec potepanec [コマンド]
```


例
```bash
docker-compose exec potepanec bundle exec rubocop
docker-compose exec potepanec bundle install *****
```

### railsを起動しているコンテナ内のbashに入る

コンテナ外からでは操作がしずらいこともあるので、そういった場合はコンテナ内のbashを起動し、コンテナに入ることも可能です。

```bash
docker-compose exec potepanec /bin/bash
```

コンテナから出るには `exit` とコマンドを入力するか ctrl+d を入力します。

### 起動しているコンテナを停止する

`docker-compose up` を実行してログが標準出力中のターミナルでctrl+cを押すと、起動中のコンテナが停止します。
ターミナルがない場合は以下のコマンドを入力することで起動中のコンテナが停止します。

```bash
docker-compose stop
```

同時にイメージやボリュームを削除したい場合は以下の `down` を利用します。

```bash
docker-compose down --rmi all -v
```

### 全てのイメージ、ネットワーク、ボリュームを初期化する

imageやvolume network などをまとめて初期化したい場合は以下のコマンドを入力します

```bash
docker system prune --volumes
```

## Docker環境で開発している時の注意点

Dockerコンテナ経由で開発していると、ホスト端末環境上で開発している場合とは勝手が違う状況があります。当gitbook資料内で個別に注意が必要な手順は以下に解説します。

### ER図の作成
コンテナ経由でER図を作成しますが、コンテナ内にgraphvizをインストールする必要があります。

コンテナ外から以下コマンドを入力します。

```bash
docker-compose exec potepanec bundle exec apt-get install doxygen doxygen-gui graphviz

# ER図全体
docker-compose exec potepanec bundle exec erd --filename=tmp/erd

# ER図一部のみ
docker-compose exec potepanec bundle exec erd \
    --only='Spree::Taxonomy,Spree::Product,Spree::Taxon,Spree::Classification' \
    --filename=tmp/erd    
```

### ブレークポイントで停止しているコンテナへのattach

`binding.pry` でブレークポイントを仕掛けた時に、ホスト端末上のターミナルであれば、停止しているサーバーのターミナルからそのままデバッグが開始できますが、コンテナ上で動くサーバーにブレークポイントをしかけた場合、コンソールログを表示中のターミナルとは別のターミナルからコンテナにattachする必要があります。

```bash
# 別のターミナルから
docker attach potepanec_potepanec_1

# Enterを入力するとプロンプトが表示されます
```
デバッグから抜けるには `quit` を入力すればいいですが、コンテナから出る場合、 `exit` をしてしまうと、コンテナごと終了させてしまいます。
コンテナを終了させずにコンテナから出る場合には ctrl+p 入力後に ctrl+q を入力します。

### gemのソースコードを見る
Docker開発環境ではホスト端末のエディタでrailsコンテナ内でインストールされているgemのソースコードを `bundle open` で直接開くことはできません。
そのため以下のどちらかでソースコードを参照してください。

 A. 参照したいgemのソースをホスト側にコピーして参照する
    以下のコマンドで対象のgemを `tmp` 以下にコピーします。
    ```
    # solidus_coreをコピーする場合
      docker cp  \
        potepanec_potepanec_1:$(docker-compose exec potepanec \
                                bundle show solidus_core --paths | \
                                grep /potepanec/ |tr -d '\r\n') \
        tmp/
    ```

 B. コンテナ内でCUIエディタで `bundle open`を利用する
   vimやnano、emacsのようなCUIエディタをコンテナ内にインストールして `bundle open` を利用します。

## 参考資料

現在、Dockerは多くの開発現場で利用されている技術ですので、Railsの学習と共にDockerの操作も習得しておくのがオススメです。

* [Docker ドキュメント日本語化プロジェクト](http://docs.docker.jp/) [前佛さん](https://twitter.com/zembutsu)による邦訳ドキュメント

* [Docker Document(公式)](https://docs.docker.com/) 英語ですが公式なので当然ながら情報が早いです
