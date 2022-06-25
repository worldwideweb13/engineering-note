Dockerの記述メモ

  
## Dockerの基礎理解

### DockerfileとDockerイメージ

<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 15 12 07" src="https://user-images.githubusercontent.com/75665390/175760933-53f37801-a769-4ee4-9276-bd08b615117b.png">

- DockerFileからDockerイメージを作成する際に実行するコマンドが`Docker build`. DocokerイメージからDockerコンテナを作成するコマンドが`Docker run`
- DockeHubではDockerイメージが公開されており、Dockerイメージを直接自分のプロジェクトにダウンロードして利用することも可能
  
### Dockerイメージ
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 15 21 45" src="https://user-images.githubusercontent.com/75665390/175761235-5be89af4-54a0-4bf7-8dc9-fe004024401e.png">

- Dockerイメージはレイヤー構造になっており、一番下にOSレイヤーがあり、その上に、apacheやHtppdなどのリナックスコマンドを載せていく、という構造になっている。イメージはコンテナを作成するための設計図のようなもの。
- 1つの設計図からは、必ず同じコンテナが生成される = PCの環境変数に左右されずに同じ開発環境がチーム内で共有される。

  
### Dockerタグに関しての諸注意
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 15 29 26" src="https://user-images.githubusercontent.com/75665390/175761468-7b8de0dd-78e1-40da-99c0-a46e0186fe76.png">
 
- Dockerイメージに各種ソフトのインストールコマンドを記述する際、必ずソフトのインストールバージョンを記述すること`イメージ名:タグ名`

### DockerCompose
- ymlファイルの設計図で、複数のコンテナをまとめて管理できるもの。つまりサーバー毎に分離したコンテナを,連携させて動かす上で必須の技術であり,dockercomposeを使って開発環境を稼働させる運用を敷いている企業がほとんど。
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 17 00 20" src="https://user-images.githubusercontent.com/75665390/175764370-7927fb62-6511-4698-ba62-0b623283ed65.png">
