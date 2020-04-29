Compact Python container sample
=====


distroless を使って Python の実行コンテナをコンパクトにするサンプル  


## 概要

src ディレクトリ配下と requirements.txt がコンテナ内にコピーされます  
ビルドコンテナ内で pip install など必要な依存パッケージを取得し  
実行に必要なものだけが入ったコンテナが最終的にできあがります。  


## 開発環境構築

```sh
# 実行環境構築
pipenv --python 3.7

# 依存ファイルの読み込み
pipenv install --skip-lock

# 依存ファイルのロック
pipenv run pip freeze > requirements.txt
```


## コンテナビルド

```sh
docker build -t dev.local/sample-distroless-python-server .
```


## 実行

```sh
docker run \
    --rm \
    --env PORT:8080 \
    --publish 8080:8080 \
    dev.local/sample-distroless-python-server
```

- 動作確認
```sh
curl localhost:8080
# Hello, World!
```


## コンテナサイズの比較

```sh
docker images
REPOSITORY                                  TAG                 IMAGE ID            CREATED             SIZE
dev.local/sample-distroless-python-server   latest              5fef286ac5c3        4 minutes ago       55.9MB
python                                      3.7-slim            59ade49ea505        5 days ago          179MB
gcr.io/distroless/python3-debian10          latest              204625986be9        50 years ago        52.2MB
```

