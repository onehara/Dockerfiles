# Dockerfiles
[docker, nvidia-docker install:](https://qiita.com/spiderx_jp/items/32c421fd00c6ade19720#nvidia-docker-20-%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)

## cuda入りイメージはdockerhubから探す
　dockerhub登録後、`docker login`で入れる。  
 ```
 sudo docker login
 Username: hogehoge
 ```
・cuda使いたいならdevel版のimageを使う。   
　baseやruntimeだとnvccが通らない。  
ここではダウンロードとかはしなくて良い。  

##  Dockerfileを作ったら、ビルドしてイメージを作成
FROMでイメージ名指定すれば持ってこれる。  
```
sudo docker build -t hoge/yolov3_gpu -f Dockerfile .
```

## runでコンテナ作成
runでコンテナが作成出来る。あんまり連発すると後でコンテナ消すのが面倒。  
```sudo docker run --runtime=nvidia -it -v `pwd`/temp:/root/work/temp hoge/yolov3_gpu bash ```

## yolov3追加作業
ここを自動で出来るようにしたい  
```
・GPU=1, cuDNN=1にしてからmake
・cfgの設定（バッチサイズとか）変更
```

・exitでコンテナが停止する。内部データ等が削除されるわけではない。  
・処理を止めたくないならdettachしてログインを抜ける。  
　"control+P、Q"でdettach出来る。  
・dettach後や、起動中のコンテナに入りたい時はattachで入れる。  
  ```sudo docker attach docker-id```

