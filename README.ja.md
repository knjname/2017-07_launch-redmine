
# Docker上にRedmineをCentOS 7.3でVagrantを使ってたちあげるやつ

1. [VirtualBox](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html) と [Vagrant](https://www.vagrantup.com/downloads.html) をインストール。
2. `vagrant up`　を実行.
   ```console
   $ vagrant up
   ```
3. 初期化がはじまる。
4. `docker-disk-volume.vdi` (50GiB以下) というディスクファイルが作成されて、 `/opt/docker` にマウントされる。このファイルは消しちゃダメ。
5. 全ての初期化が終わったら http://localhost:18080 にRedmineが見えるはず. (`admin`/`admin123`)

## Vagrant使わずマニュアルでたちあげたい人

1. 自分でCentOS 7.3を立ち上げたら、[Vagrantfile](./Vagrantfile) の中の `# Package initialization.` あたりからのコマンドを参考にしてDockerおよびdocker-composeをインストールしてください。
2. [docker-compose.yml](./redmine-docker-template/docker-compose.yml) ファイルを `/opt/docker` などにおいて、 `docker-compose up` コマンドを実行しましょう。

## リンク

* https://github.com/sameersbn/docker-redmine

## License

MIT License
