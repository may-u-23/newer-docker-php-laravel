# 前提
- より新しいバージョンを使用する(最終更新: 2020-12-12)

| - | Version | Release | Bug fix | Security fix | Remarks |
|:---:|:---:|:---:|:---:|:---:|:---:|
| PHP | 8.0.0RC5 (cli) | (8: 2020-11-26) | - | - | 正式リリース版の公式イメージ無しのため代替インストール |
| Laravel | 8.18.1 | (8: 2020-09-08) | 2021-04-06 | 2021-09-08 | PHP>= 7.3 |
| MySQL | 8.0.22 | - | - | - | - |
| nginx | 1.19.5 | - | - | - | - |

# 環境情報
```
❯ sw_vers
ProductName:	Mac OS X
ProductVersion:	10.15.7
BuildVersion:	19H15

❯ docker --version
Docker version 19.03.13, build 4484c46d9d

❯ docker-compose --version
docker-compose version 1.27.4, build 40524192
```

# 構成
```
.
├── infra
│   ├── php
│   │   ├── Dockerfile
│   │   └── php.ini # PHPの設定ファイル
│   │
│   └── nginx
│       └── default.conf # nginxの設定ファイル
│
├── web # Laravelをインストールするディレクトリ
│
└── docker-compose.yml
```

# 基本操作
## ビルド&Up
```
❯  docker-compose up -d --build
```
## Down
```
❯  docker-compose down
```

## 起動確認
```
❯ docker-compose ps
             Name                           Command               State           Ports        
-----------------------------------------------------------------------------------------------
newer-docker-php-laravel_app_1   docker-php-entrypoint php-fpm    Up      9000/tcp             
newer-docker-php-laravel_db_1    docker-entrypoint.sh mysqld      Up      3306/tcp, 33060/tcp  
newer-docker-php-laravel_web_1   /docker-entrypoint.sh ngin ...   Up      0.0.0.0:10080->80/tcp
```

## バックエンドコンテナ
### コンテナに入る
```
❯  docker-compose exec app bash
root@hoge:/work# 
```

### コンテナから出る
```
root@hoge:/work# exit
```

## 滅びの呪文
コンテナの停止、ネットワーク・名前付きボリューム・コンテナイメージ、未定義コンテナを削除
```
docker-compose down --rmi all --volumes --remove-orphans
```

# 参考
- [【超入門】20分でLaravel開発環境を爆速構築するDockerハンズオン - Qiita](https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4)