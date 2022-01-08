# Docker チートシート
## よく使う例
`docker build -t yokoikzk/hoge:latest .`
`docker run -d -p 8080:80 httpd`
`docker images`
`docker rmi [イメージID]`
`docker ps -a`
`docker rm [コンテナID]`
## イメージ
### イメージの作成
`docker build -t [イメージ名] [ディレクトリ]`
`docker build -t yokoikzk/hoge .`

### イメージの起動
`docker run -d -p [ホスト側port]:[コンテナ側port] [イメージ名]`
`docker run -d -p 8081:8080 yokoikzk/hoge`



| オプション | 説明 | 例 |
| -------- | -------- | -------- |
| -d     | バックグランド実行    | docker run -d centos|
| -p [ホスト側]:[コンテナ側]    | ポートフォワーディング    | docker run -d -p 8080:80 httpd     |
| -it     | Dockerのイメージ内にログイン    | docker run -it ubuntu     |


### イメージの確認
`docker images`

### イメージの削除
`docker rmi [イメージID]`

## コンテナ
### コンテナの確認
#### 動いてるコンテナの確認
`docker ps`

#### 停止しているコンテナの確認
`docker ps -a`

### コンテナの削除
`docker rm [コンテナID]`

## Dockerをsudoなしで実行する方法
1. dockerグループを作成  
`sudo groupadd docker`

2. ユーザーをdockerグループに追加  
`sudo usermod -aG docker $USER`

3. グループを変更  
`newgrp docker`

4. sudoがなくてもdockerコマンドが実行できることを確認  
`docker run hello-world`

参考:	[Manage Docker as a non-root user](https://docs.docker.com/engine/install/linux-postinstall/)
