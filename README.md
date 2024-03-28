shsipsimulatorをVNC上で実行するためのDockerfile

ターミナルで下記のコマンドを実行してビルドしてください

```bash
docker build -t shipsimulator-vnc:humble humble/.
```

その後ビルドしたDockerコンテナに接続吸うために以下のコマンドを実行して
[localhost:6080](http://127.0.0.1:6080/)にアクセスしてください

```
docker run -p 6080:80 --shm-size=512m shipsimulator-vnc:humble
```

