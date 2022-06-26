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

### Volumeの永続化
- Dockerはパソコンのメモリ上の存在するもの.(仮想環境で構築したものと決定的に違うこと) コンテナが削除された場合、データも削除されてしまうため、DBなどの永続的に持たせたいデータ(volume)の処理に関しては対応を考えなければいけない。
- コンテナは停止/破棄可能(エフェメラル)な状態にすることが大切であり、各コンテナが固有のDBを持つことは望ましくない
- そこで最初に検討されるのが、volumeの参照先をPCのストレージにすること。(`docker run -v`) これを使うとホスト側のマシンのディククとコンテナのvolumeを共有することができるようになる。(コンテナが破棄されても、次回作成されたコンテナもvolumeはホストのディスクを参照するのでデータが再現される) 
-　フレームワーク利用時の設定ファイル(document rootなど)もvolumeを使い、設定ファイルをローカルPCのストレージに用意して、コンテナの設定ファイルフォルダが参照するように指定する
  - ※1 ymlに設定ファイルを読み込ませている例
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-26 21 57 43" src="https://user-images.githubusercontent.com/75665390/175815272-34bb3625-939d-44fb-8754-5b6f1633571b.png">

### Dockerの設計
- Dockerコンテナは極力、シンプルな構成で作成されるべきで１コンテナ、１プロセスにすべきである。
- そのため、サーバー構成も、(webサーバー、アプリケーションサーバー、WEBアプリケーションサーバーetc)のように実際のサーバー構成と同じようにコンテナも切り分けて作成される。　サーバー構成に関して[こちら](https://www.youtube.com/watch?v=jnFvDiR-chQ&t=6s)の動画参照
<img width="593" alt="スクリーンショット 2022-06-25 17 58 15" src="https://user-images.githubusercontent.com/75665390/175766219-cbe0c56c-649f-40ff-a27a-4c39a43189be.png">
  
### DockerCompose
- ymlファイルの設計図で、複数のコンテナをまとめて管理できるもの。つまりサーバー毎に分離したコンテナを,連携させて動かす上で必須の技術であり,dockercomposeを使って開発環境を稼働させる運用を敷いている企業がほとんど。
- ymlファイルには、DockerFileのパス（参照箇所）、imageの参照先などを親子関係で記述してあり,各コンテナのfileの読み出し→イメージ作成→コンテナ作成までを行うロードマップを記述している(多分)
- imageはDockerHubから指定(`name:version`の形式), buildはDockerファイルのパスを記述
- データの永続化(volumeの設定)は`volume:` でネストした相対パスで記述
- portsの設定はネストして`外部公開ポート:コンテナ内部ポート`で記述(画像 ※1 PORTの設定 参照). 画像の例の場合、8080で入ってきた処理は80に置き換える、という指定になる
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 17 00 20" src="https://user-images.githubusercontent.com/75665390/175764370-7927fb62-6511-4698-ba62-0b623283ed65.png">
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 17 21 58" src="https://user-images.githubusercontent.com/75665390/175765104-f9a31d53-8176-4a87-8bab-cc2a146897b0.png">

  - ※1 PORTの設定
<p align="center">
<img width="593" alt="スクリーンショット 2022-06-25 17 40 51" src="https://user-images.githubusercontent.com/75665390/175765654-1c20c1b1-943d-40c4-b975-5ed327c9c1ed.png">
  


 
