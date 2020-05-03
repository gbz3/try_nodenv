# try_nodenv

## 環境構築(WSL)

- WSL インストール
- Ubuntu 18.04 LTS インストール
- VS Code に 'Remote - WSL', 'Remote - Development' インストール
- 左下の「><」リモートウインドウを開く  
  - ※初回はインストール終了を少し待つ
- ホームディレクトリを開く
- 'Ctrl + Shift + @' でターミナルを開く
- ~/.ssh に SSH鍵を配置

```bash
※0755 ~/.ssh
※0600 ~/.ssh/id_rsa
※0644 ~/.ssh/id_rsa.pub
```

- git 初期設定

```bash
$ git config --global user.name '<username>'
$ git config --global user.email '<email-address>'
$ git config --global code.editor 'code --wait'
$ git config --global merge.tool 'code --wait "$MERGED"'
$ git config --global push.default simple
$
```

- clone

```bash
$ mkdir git_repos
$ cd git_repos
$ git clone '<SSH version URL>'
$
```

## 環境構築(nodenv) @Ubuntu

- Clone nodenv into `~/.nodenv`.

```bash
$ git clone https://github.com/nodenv/nodenv.git ~/.nodenv
$
```

- PATH設定

```bash
$ echo 'export PATH="$HOME/.nodenv/bin:$PATH"' >> ~/.bashrc
$
```

- 環境設定

```bash
$ ~/.nodenv/bin/nodenv init
$ echo 'eval "$(nodenv init -)"' >>~/.bashrc
$
```

- nodenv 再ロード(シェルセッション再起動)
- node-build プラグインインストール

```bash
$ git clone https://github.com/nodenv/node-build.git ~/.nodenv/plugins/node-build
$
```

- シェル環境確認

```bash
$ curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash
Checking for `nodenv' in PATH: $HOME/.nodenv/bin/nodenv
Checking for nodenv shims in PATH: OK
Checking `nodenv install' support: $HOME/.nodenv/plugins/node-build/bin/nodenv-install (node-build 4.7.2-81-g02dc3633)
Counting installed Node versions: none
  There aren't any Node versions installed under `$HOME/.nodenv/versions'.
  You can install Node versions like so: nodenv install 2.2.4
Auditing installed plugins: OK
```

## 環境構築(Node.js) @Ubuntu

- インストール可能バージョンの確認/インストール

```bash
$ nodenv install --list
～省略～
10.14.0
10.14.1
10.14.2
～省略～
$ nodenv install 10.14.2
Downloading node-v10.14.2-linux-x64.tar.gz...
-> https://nodejs.org/dist/v10.14.2/node-v10.14.2-linux-x64.tar.gz
Installing node-v10.14.2-linux-x64...
Installed node-v10.14.2-linux-x64 to $HOME/.nodenv/versions/10.14.2
$ nodenv install 12.16.1
Downloading node-v12.16.1-linux-x64.tar.gz...
-> https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar.gz
Installing node-v12.16.1-linux-x64...
Installed node-v12.16.1-linux-x64 to /home/kashiba/.nodenv/versions/12.16.1
$ ls ~/.nodenv/versions
10.14.2  12.16.1
```

- shims リハッシュ

```bash
$ nodenv rehash
$
```

- グローバル指定前

```bash
$ node -v
nodenv: node: command not found

The `node' command exists in these Node versions:
  10.14.2

$ npm -v
nodenv: npm: command not found

The `npm' command exists in these Node versions:
  10.14.2

```

- グローバル環境設定

```bash
$ nodenv global 10.14.2
$ node -v
v10.14.2
$ npm -v
6.4.1
```

- ローカル環境設定

```bash
$ cd git_repos/try_nodenv/
$ nodenv local 10.14.2
$ cat .node-version
10.14.2
```
