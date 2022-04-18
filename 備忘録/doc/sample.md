## WSL2

1. `wsl`インストール
    * 管理者の PowerShell または Windows コマンド プロンプトに次のコマンドを入力し、コンピューターを再起動することによって、Linux 用 Windows サブシステム (WSL) を実行するために必要なすべてをインストールできる
```
wsl --install
```
- [Windows 10 用 Windows Subsystem for Linux のインストール ガイド](https://docs.microsoft.com/ja-jp/windows/wsl/install-win10) を参照

### 上記手順でインストールできない場合
1. Linux カーネル更新プログラム パッケージをダウンロードする
    * 最新のパッケージをダウンロード、実行
      * [x64 マシン用 WSL2 Linux カーネル更新プログラム パッケージ](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
2. WSL 2 を既定のバージョンとして設定する
    * PowerShell を開いて次のコマンドを実行し、新しい Linux ディストリビューションをインストールする際の既定のバージョンとして WSL 2 を設定
```
wsl --set-default-version 2
```

3. 選択した Linux ディストリビューションをインストールする
`Ubuntu 20.04 LTS`を選択

    * [Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)を入手
4. Ubuntu 20.04 LTSを起動後、ユーザー アカウントとパスワードを作成して完了

##### 参考 https://docs.microsoft.com/ja-jp/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

## Ubuntu設定

##### DNS設定の変更

1. /etc/wsl.conf を作成し、以下の内容を記載
    * WSLによる自動生成を停止
```
$ sudo vi /etc/wsl.conf
[network]
generateResolvConf = false
```
2. /etc/resolv.conf をバックアップ
    * バックアップの作成
```
$ sudo cp /etc/resolv.conf /etc/resolv.conf_bk
```
3. 現在の /etc/resolv.conf のリンクを解除
    * リンクの解除
```
$ sudo unlink /etc/resolv.conf
```
4. 新しく /etc/resolv.conf を作成
    * DNSの設定を追加
```
$ sudo vi /etc/resolv.conf
nameserver 172.20.10.111
nameserver 172.20.20.111
```
5. Ubuntuを再起動

6. Ubuntu 側でpingが通るか確認
```
$ ping 172.20.10.111
$ ping 172.20.20.111
```

#### PROXYの設定変更
1. .bashrc に以下を追加

```
$ sudo vi ~/.bashrc
export http_proxy=http://DCSVPRXSV99.minori-sol.local:8080
export https_proxy=${http_proxy}
```

2. root の /etc/apt/apt.conf を新規作成し、以下を追加
```
$ sudo vi /etc/apt/apt.conf
Acquire::http::proxy "http://DCSVPRXSV99.minori-sol.local:8080";
Acquire::https::proxy "http://DCSVPRXSV99.minori-sol.local:8080";
```
3. ~/.curlrc を新規作成し、以下を追加
```
$ sudo vi ~/.curlrc
proxy=http://DCSVPRXSV99.minori-sol.local:8080
```

#### gitに対してproxyの設定
```
$ git config --global http.proxy http://DCSVPRXSV99.minori-sol.local:8080
$ git config --global https.proxy http://DCSVPRXSV99.minori-sol.local:8080
```
* これにより `~/.gitconfig`に下記が追加される。
```
[http]
        proxy = http://DCSVPRXSV99.minori-sol.local:8080
[https]
        proxy = http://DCSVPRXSV99.minori-sol.local:8080
[url "https://"]
        insteadOf = git://
```

## WSL2内でclone
### 鍵作成
1. 名前とメールアドレスを設定
```
$ git config --global user.name "${userName}"
$ git config --global user.email "${mailAddress}"
```
2. SSH key
```
$ ssh-keygen -t rsa -C "${mailAddress}"
```
    * すべてEnterで進む
      * ユーザディレクトリ/.ssh/以下にids_rsa(秘密鍵), ids_rsa.pub(公開鍵)ができる

### Gitlabに鍵の設定
* GitLabのユーザー設定画面(https://192.168.8.80/-/profile)
* SSH Keys(https://192.168.8.80/-/profile/keys)
* Keyのテキストエリアに、`id_rsa.pub`のテキストをコピペする
* titleはデフォルトでメールアドレスが入る
* 「Add Key」ボタンで登録

### clone
* 以下コマンドでclone
```
$ git clone --recursive ssh://git@192.168.8.80:10022/yamaga/line-works-usage.git
```

## Python

1. pythonに必要ライブラリのインストール

```
$ sudo apt update
$ sudo apt install build-essential gfortran wget
$ sudo apt install sudo apt install libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libbz2-dev liblzma-dev zlib1g-dev uuid-dev libffi-dev libdb-dev tk-dev
```

2. [Python公式](https://www.python.org/downloads/source/)から任意の stable のソースコードをダウンロードし解凍
```
$ wget https://www.python.org/ftp/python/3.9.12/Python-3.9.12.tar.xz
$ tar xf Python-3.9.12.tar.xz
$ cd Python-3.9.12
```

3. ビルド
```
$ ./configure --prefix=$HOME/.local --with-ensurepip --enable-optimizations --with-lto
$ make -j4
$ make altinstall
```
以上でインストール完了

4. パスを通す
    * symlink を設定
```
$ cd ~/.local/bin
$ ln -s python3.9 python3
$ ln -s pip3.9 pip3
```

5. pipを最新バージョンに更新
```
$ pip3 install --upgrade pip
```

## PostgreSQL
* PostgreSQLは以下でインストールする
```
$ sudo apt install postgresql libpq-dev
```
### PosgreSQLのユーザーとDB作成

1. 新しいロール(ユーザー)の作成
* パスワードも設定するので、以下のコマンドを実行
* ユーザー名は`xsozxxxxvksikx`
* パスワードは`xxxxx`
* その他の権限は、任意(super userはNoでそれ以外はYes)

```
$ sudo -u postgres createuser --interactive --pwprompt
```

2. 新しいデータベースの作成
  * DB名は`x3mdxxxxsg5nx`

```
sudo -u postgres createdb x3mdxxxxsg5nx
```

### PostgreSQLの接続設定
#### WSL外から接続できるための設定(A5SQLから)
1. postgresql 設定ファイルの更新
  * 以下設定ファイルの`127.0.0.1/32`を`all`に変更
/etc/postgresql/12/main/pg_hba.conf

```
$ sudo vi /etc/postgresql/12/main/pg_hba.conf
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
```
↓
```
# IPv4 local connections:
host    all             all             all                     md5
```
* 以下設定ファイルの`listen_addresses`の設定がコメントになっているので、コメントを外す。
* `0.0.0.0`を設定することで、postgresql がすべての IP アドレスからの接続を待ち受けるようになる
```
$ sudo vi /etc/postgresql/12/main/postgresql.conf
- #listen_addresses = 'localhost'
+ listen_addresses = '0.0.0.0'
```

2. 再起動(設定反映)
```
$ sudo service postgresql restart
```

3. WSLのIPアドレスを確認
* WSL上で実行

```
$ ip a show dev eth0
inet ～の部分がIPアドレス
```

4. A5SQLから上記で作成したDBに接続する
* **サーバー名** `IPアドレス`
* **データベース名** `x3mdxxxxsg5nx`
* **ユーザーID** `xsozxxxxvksikx`
* **パスワード** `xxxxx`

### 起動/停止
```
$ sudo service postgresql start
$ sudo service postgresql stop
```

## Poetry
1. インストール
```
$ curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
$ poetry --version
```
2. envファイルをプロジェクト配下に作成する設定
```
poetry config --list
poetry config virtualenvs.in-project true
```
### プロジェクトの設定
1. Ubuntuからリポジトリ内に移動
2. 以下コマンドでPoetry仮想環境を作成(.venvの作成)
```
$ cd samplebot_attendance_management_bot-master
$ poetry install
```


## Visual Studio Code
1. [Visual Studio Code](https://code.visualstudio.com/download)からダウンロード
2. ウィザード通りインストールする
3. 拡張機能を追加
    * [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)

4. CA証明書を追加する
```
$ sudo apt install ca-certificates
```

5. WSL側からVScodeを起動  
**1回目**
    * 起動はWindows側からではなく、WSL(Linuxディストリビューション)側から行う
```
# 開きたいディレクトリに移動
$ cd samplebot_attendance_management_bot-master
# Stable版（通常版）のVScodeを使う場合
$ code .
# insiders版（プレビュー版）を使う場合
$ code-insiders .
```
* 初めて起動する場合は必要なパッケージの自動インストールに少し時間がかかる
* 左下にWSL: <ディストリビューション名>という表示が出ていればリモートでWSLに接続できている  
**2回目以降**
* vsCodeから`F1`キーを押して`Remote-WSL: New Window using Distro`を選択して、使いたいディストリビューションを選ぶことでRemote WSLになった状態のウィンドウが開く
