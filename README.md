# go-echo-railway

Go x echo x [Railway](https://railway.app/) のテンプレートです。

## ローカル開発

環境変数を用意する。生成された`.env`をカスタマイズできる。

```
cp .env.example .env
```

Docker イメージをビルドする。

```
make build-local
```

Docker コンテナを立ち上げる。

```
 make up
```

`localhost:${PORT}` （デフォルトのポートは 80）にアクセスすると`hello world`と表示される。

## make コマンド

Docker 関連のコマンドやテストなどのコマンドが用意されている。`Makefile`を閲覧するか、以下のコマンドから一覧を確認できる。

```
make help
```

## デプロイ

Railway にデプロイする方法を説明します。

### 1. [railway.app](https://railway.app/)へログイン

![スクリーンショット 2023-07-27 18 56 09](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/62a5fbab-5ef7-4db7-9496-68aa77a97dca)

### 2. プロジェクトの新規作成

![スクリーンショット 2023-07-27 18 58 52](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/6c314ed2-8c30-4d53-8c58-2c92714f5ac4)

「Deploy from GitHub repo」を選択し、リポジトリ名を入力する。

![スクリーンショット 2023-07-27 19 00 36](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/7fb7b400-d49a-4da7-86fc-96eaa24b34fb)

「Add variables」を選択する。

#### 2.1. 環境変数の設定

`.env.example`の値をベースに環境変数を設定する。
`APP_ENV`は `production` に変更する必要がある点に注意する。

「Suggested Variables」が表示される場合は、「Add All」をクリックして追加する。

![スクリーンショット 2023-07-27 19 03 28](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/374a027c-a21e-4ce2-9df4-410a3bcae34f)

#### 2.2. ドメインの追加

タブから「Settings」に移動し、「Domains」にて「Generate Domain」または「Custom Domain」のいずれかをクリックし、ドメインを追加する。

![スクリーンショット 2023-07-27 19 05 32](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/0c9cadee-2ba0-4324-8a5a-291401cee2c7)

作成されたドメインにアクセスし、「hello world」と表示されれば API サーバのデプロイは成功している。

以下のように表示された場合は、ドメインの反映処理中のためしばらく時間を置いてから再度アクセスする。

![スクリーンショット 2023-07-27 19 06 58](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/d0717cae-e3a0-48cb-977f-66811c188e25)

#### 2.3. データベースの追加

つづいて、データベースサーバの追加を行う。

この画面に遷移して、右上の「New」ボタンをクリックし、「Database」を選択する。

![スクリーンショット 2023-07-27 19 08 04](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/42ea4817-b8bf-4126-878f-5fbe53110510)

いくかのデータベースの候補が表示されるため、任意のデータベースを選択する。ここでは「MySQL」を選択する。

![スクリーンショット 2023-07-27 19 09 07](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/f613f64a-549b-477a-a6b8-acf1077ebe15)

しばらくされると、API サーバの横に MySQL が表示された。これで、データベースがプロジェクトに追加された。

![スクリーンショット 2023-07-27 19 10 57](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/5ebd8cf0-5c9a-4b4a-8752-8c2166096840)

#### 2.4. API サーバとデータベースを紐付ける

さいごに、API サーバの環境変数を修正し、データベースサーバと紐付けを行う。

まず、上の画面で MySQL をクリックし、表示される画面でタブから「Connect」に遷移する。
すると、以下の画面になるため、「Available Variables」から必要な情報をコピーし、「
2.1. 環境変数の設定」の画面で対応する環境変数にペーストする。

![スクリーンショット 2023-07-27 19 12 32](https://github.com/yuuumiravy/go-echo-railway/assets/73621966/fcb17440-9002-4b98-bedb-369365d46740)

必要な情報は次のとおりである。

- `MYSQLDATABASE` - `DB_DATABASE`
- `MYSQLHOST` - `DB_HOST`
- `MYSQLPASSWORD` - `DB_PASSWORD`
- `MYSQLPORT` - `DB_PORT`
- `MYSQLUSER` - `DB_USER`
