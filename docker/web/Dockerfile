
# nginxイメージの バージョン1.27をベースとして、Dockerイメージを作成する
FROM nginx:1.27

# 作成した設定ファイルをコンテナ内にコピー
# default.confの参照（https://readouble.com/laravel/11.x/ja/deployment.html）
COPY default.conf /etc/nginx/conf.d/default.conf