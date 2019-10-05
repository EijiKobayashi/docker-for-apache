# docker-for-apache

## docker-compose ビルド

```
# /docker/localhost ディレクトリに移動して
$ docker-compose build --no-cache
```

## docker-compose 起動

docker-compose up -d 実行後 http://localhost:3000/ でブラウズ

```
$ docker-compose up -d
```

## docker-compose シャットダウン

```
$ docker-compose down
```

## ディレクトリ構成

```
├─ docker/
│  └─ パッケージ各種
│
├─ docker/（Dockerファイル一式）
│  ├─ localhost/
│  │  ├─ mysql/ (MySQL関連)
│  │  ├─ php-apache/ (Apache関連)
│  │  └─ phpmyadmin/ (PHPMyAdmin関連)
│  └─ docker-compose.yml
│
├─ localhost/（ビルド前のソース）
│  └─ var/
│      └─ www
│          └─ html
└─ README.md
```
