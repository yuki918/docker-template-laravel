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

```bash
git clone https://github.com/yuki918/docker-template-laravel.git
cd docker-template-laravel
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

### 3. Laravelを最新バージョンへ

```bash
# コンテナへ入る
docker compose exec php bash

# 全てのファイルの削除
rm -rf *

# Laravelのインストール
composer create-project --prefer-dist "laravel/laravel=" .
```

下記で閲覧できれば、構築完了です。<br>
http://localhost:8080