# Vagrant + Ansible によるプロビジョニング・テンプレート集

Vagrant で作成する仮想環境に Ansible でプロビジョニングするテンプレート集です。
最初は CakePHP3 で作成しました。

ロール別のプロビジョニングは省略し関係するファイルを極力少なくしてプロビジョニングのカスタマイズをしやすいようにしてあります。

## CakePHP3

このテンプレートでは、CentOS7.4 に最新の Apache2 + MySQL5.6 + PHP7.2 + Composer + phpMyAdminの環境が構築されます。Database作成は手動。CakePHP3のインストールはwwwフォルダのシェルを実行します。

すでにプロジェクトが存在する場合は /vagrant/www/html にドキュメントルートがあるのでここで git clone し、 Database のユーザーやDBを手動で設定すればそこから開発をスタートとなります。

IPアドレスは 192.168.33.10 に固定されています。変更する場合は事前に Vagrantfile を編集ください。

## phpMyAdmin

IPアドレスは 192.168.33.10/phpMyAdmin に設定されています。変更する場合は、provisioning/tasks/templates/phpMyAdmin.conf の設定を変更してください。

# インストール方法

Vagrant, VirtualBOX, Ansible をホストPCに事前にインストールしてください。
Ansibleは以下の2系のバージョンになっている事を確認ください。

```
$ ansible --version
ansible 2.5.4
```

ホストPCの環境が整って入れば以下2行でプロビジョニング完了です。

```
vagrant up
vagrant provision
## 上記2行で Apache2, MySQL5.6, PHP7.2, Composer のローカル環境が構築されます。
vagrant ssh
cd /vagrant/www
## Composer による CakePHP のインストールをする場合は以下です。
sh ./install.sh
```

# ドキュメントルート・パスワード等

ドキュメントルートは /vagrant/www/html です。

MySQLのrootパスワードはrootです。

データベースは自動作成しないので自身で作成してください。

IPアドレスは 192.168.33.10 になっています。

# 環境変数について

このプロビジョニングでは取り扱いません。以下参考に各自で記述ください。
httpd だけに必要な変数は、httpd.conf の最後の行追記します。
コマンドラインから実行する場合は /etc/profile に記述してください。
migration や CI で利用する場合は profile 記述します。

例: sudo vi  /etc/profile
```
export RDS_HOSTNAME=127.0.0.1
export RDS_USERNAME=mydb
export RDS_PASSWORD=mydb
export RDS_DB_NAME=mydb
```


