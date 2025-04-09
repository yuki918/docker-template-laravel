# Dockerを使ってLaravelの開発環境を構築するテンプレート

このリポジトリは、Laravelのローカル開発環境を素早く構築するためのDocker Composeテンプレートです。

## 構成

- PHP 8.2
- Nginx 1.27
- MySQL 8.3

## ディレクトリ構造


```
【ルートディレクトリ】
├─ docker
│   └─ db
│   └─ php
│   └─ web
├─ src
│   └─ 【Laravelのパッケージ】
└─ docker-compose.yml
```

## セットアップ手順

### 1. リポジトリをクローン

本リポジトリは[テンプレート化](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-template-repository)しているため、再利用することが可能です。  
[こちら](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)の手順にしたがって、リポジトリを作成してください。  
作成したリポジトリをクローンします。

```bash
git clone https://github.com/yuki918/new-laravel-project.git
cd new-laravel-project
```

### 2. コンテナを起動

```bash
# dockerとLaravelの.envファイルの編集
cp .env.example .env
cp src/.env.example src/.env

# コンテナを起動する
docker compose up -d --build
```

#### dockerの.envファイル編集

```
DB_ROOT_PASSWORD=password
DB_USER=任意のユーザー名
DB_PASSWORD=任意のパスワード
DB_DATABASE=任意のデータベース名
```

#### Laravelの.envファイル編集

コピーした.envファイルのデータベースの情報の修正
```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=dockerの.envファイルのDB_DATABASE
DB_USERNAME=dockerの.envファイルのDB_USER
DB_PASSWORD=dockerの.envファイルのDB_PASSWORD
```

### 3. Laravelの設定

```bash
# コンテナへ入る
docker compose exec php bash

# ライブラリのインストール
composer install

# 権限の変更
chmod -R 775 storage storage
chmod -R 775 storage bootstrap/cache

# アプリケーションキーを生成
php artisan key:generate

# マイグレーションの実行
php artisan migrate 

# 最新のLaravelで構築したい場合は、ファイルをすべて削除して、もう一度Laravelを入れなおす
rm -rf *
composer create-project --prefer-dist "laravel/laravel=" .
```

下記で閲覧できれば、構築完了です。<br>
http://localhost:8080