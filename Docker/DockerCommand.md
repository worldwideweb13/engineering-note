

- 起動中のコンテナを表示
```
ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
- 起動していないコンテナも含めて全て表示
```
ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
dfeef1d4c85c   hello-world   "/hello"   5 seconds ago   Exited (0) 5 seconds ago             rmtest
```

- オプション
  - `--name`オプション. コンテナに名前をつけることができる。
  - `--rm` オプション コンテナを停止する際にコンテナを自動削除。消し忘れがなくなる.
  ```
  ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker run --name test --rm hello-world
  Hello from Docker!
  ```
  - `-it　ディレクトリ名` コンテナの中に入る　。下のコマンドではmycentosコンテナの`bin/bash`に入り、bashを起動 という意味
  ```
  ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker run -it --name mycentos centos:8 bin/bash
  Unable to find image 'centos:8' locally
  8: Pulling from library/centos
  a1d0c7532777: Pull complete
  [root@bc33fcdf4408 /]#
  ```
  - `exec`起動中のコンテナ内でコマンドを実行する. コンテナの中に入らずにコマンドを実行することが可能. 下の例ではmycentosコンテナのbashでインストールosの確認を行なっている
  ```
  ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker exec mycentos cat /etc/redhat-release
  CentOS Linux release 8.4.2105
  ```
  - `docker rm コンテナ指定`,`docker rmi イメージ指定` Dockerコンテナの削除、Dockerイメージの削除コマンド. `rmi`オプションでは、起動中のコンテナは削除できない（Dockerイメージは依存関係がある. 実在するコンテナにimageがないという状態にはならない）
  - `Docker build Dockerfileパス` でDockerfileからimageを作成
  - `docker vp passName copiedPassName` passNameをcopiedPassNameにコピーする.`docker cp ホストファイルパス コンテナファイルパス` `docker cp コンテナファイルパス ホストファイルパス`
