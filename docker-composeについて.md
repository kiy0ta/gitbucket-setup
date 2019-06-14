### docker-compose について

- 基本的な書き方

```
docker container run -d -p 9000:8080 example/echo:latest

# これを docker-compose.yaml にすると以下のようになる

version: "3"
services:
  echo: # services要素でコンテナの名前の定義

    # 実行するコンテナの定義
    image: example/echo:latest
    ports:
      - 9000:8080

```

- 実行方法

```
docker-compose up -d

```

- Dockerfileとの違い
    - Dockerfileはイメージの構成を定義するもの

```
# 参考例

FROM golang:1.9

RUN mkdir /echo
COPY main.go /echo

CMD ["go", "run", "/echo/main.go"]

```

- image属性を指定するだけでなく、ビルドと出来上がったイメージの実行を一緒にできる
    - Dockerfileが存在するディレクトリの相対パスをbuild属性として指定

```
version: "3"
services:
  echo:
    # Dockerfileが同じディレクトリ内にある場合
    build: .
    ports:
      - 9000:8080

```