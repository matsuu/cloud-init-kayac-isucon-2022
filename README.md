# cloud-init-kayac-isucon-2022

## Overview

[kayac-isucon-2022](https://github.com/kayac/kayac-isucon-2022)とほぼ同じ環境を構築するためのcloud-configです。

## Requirements

* Ubuntu 20.04 LTSを用意してください。
* ストレージは4GBでは不足します。8GBあれば問題ないと思います。

## Usage

### Multipassでの利用方法

* [Multipass](https://multipass.run/)実行環境を用意します
* このリポジトリ内の `kayac-isucon-2022.cfg` を手元に用意します
* 以下を実行します
  ```sh
  multipass launch --name kayac-isucon-2022 --cpus 2 --disk 8G --mem 4G --cloud-init kayac-isucon-2022.cfg 20.04
  ```
  * cpus, disk, memoryは必要に応じて増減させてください
  * cloud-initは時間がかかるためタイムアウトとなるもののバックグラウンドで構築は行われています
* ログインします
  ```sh
  multipass shell kayac-isucon-2022
  ```
* 進捗確認は以下のコマンドで確認できます
  ```sh
  sudo tail -f /var/log/cloud-init-output.log
  ```

## Bench

* 構築が終わったらベンチマークを実行します
  ```sh
  sudo -i -u isucon
  cd bench
  ./bench
  ```

## 本来の設定と異なるところ

* ベンチマークをコンパイルするためgolangなど依存するソフトウェアをインストールしています

## FAQ

### 途中でエラーが発生した

スリープモードなどの影響で失敗した場合は以下で再試行ができます。

```sh
sudo /var/lib/cloud/instance/scripts/runcmd
```

### プログラムの動かし方がわからない

以下をご確認ください。

* [kayac-isucon-2022レギュレーション＆当日マニュアル](https://github.com/kayac/kayac-isucon-2022/blob/main/docs/README.md)
* [kayac-isucon-2022リポジトリ](https://github.com/kayac/kayac-isucon-2022)

### Multipassで動作確認ができない

以下のコマンドでIPアドレスの確認ができます。

```sh
multipass info kayac-isucon-2022
```

ブラウザから `http://表示されたIPアドレス/` にアクセスしてみてください。

### Multipassで作成した環境を削除したい

```sh
multipass stop kayac-isucon-2022
multipass delete kayac-isucon-2022
multipass purge
```
