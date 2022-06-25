

起動中のコンテナを表示
```
ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
起動していないコンテナも含めて全て表示
```
ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
dfeef1d4c85c   hello-world   "/hello"   5 seconds ago   Exited (0) 5 seconds ago             rmtest
```


`--name`オプション. コンテナに名前をつけることができる。
`--rm` オプション コンテナを停止する際にコンテナを自動削除。消し忘れがなくなる.
```
ogasawarasatoru@ogasawarasatoshinoMacBook-Pro ~ % docker run --name test --rm hello-world
Hello from Docker!
```
