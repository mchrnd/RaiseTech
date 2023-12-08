## 第三回課題報告

アプリケーションの起動：bin/cloud9_dev

実行後アプリケーション [URL](https://8002d3738f19443dabb9c0ec18bf66c6.vfs.cloud9.ap-northeast-1.amazonaws.com/)

### APサーバー

Puma version: 5.6.5

```
$ rails s
=> Booting Puma
=> Rails 7.0.4 application starting in development 
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Puma version: 5.6.5 (ruby 3.1.2-p20) ("Birdie's Version")
~以下略
```

```
# 稼働プロセスを確認
$ ps aux | grep puma
ec2-user 15260  5.4 12.1 980672 118616 pts/1   Sl+  09:54   0:01 puma 5.6.5 (tcp://localhost:8080) [raisetech-live8-sample
ec2-user 15552  0.0  0.0 119428   952 pts/4    S+   09:55   0:00 grep --color=auto puma
# サーバー停止
$ kill -9 15260
# ページエラーに、あわせてアプリケーションが停止されていてた
terminated by SIGKILL
# 再開
rails s
```

### DBサーバー

Mysqlログイン後status確認より
使用バージョン
mysql  Ver 8.0.35 for Linux on x86_64 (MySQL Community Server - GPL)
https://26gram.com/start-stop-mysql　参考

```
# Mysqlの起動
sudo service mysqld start
# Mysqlの停止
$ sudo service mysqld stop
# MySQLの再起動
$ sudo service mysqld restart
# Mysqlの状態確認
$ sudo service mysqld status
```

停止時エラーメッセージ  
ActiveRecord::ConnectionNotEstablished in FruitsController#index

### 構成管理ツール

ツール：Bundler version 2.3.14  
使用するGemのバージョン管理ができる  
GemfileにGemの依存関係が記述されている  

## 感想

- 作業工程を講座で実行する流れで分からない部分を調べながら行っていたらだいぶかかってしまったが、その分理解は進んだと思う。
database.ymlなど、最初に自力で調べながら挑戦したときにはわからずにいた部分も改めて手順通り行った際に調べてどの時点で生成されるものなのか等理解度をあげられてよかった。
アプリケーション起動後、APサーバーについて調べるなかで「ps aux | grep puma」のようなコマンドの記述方法も発見だった。アプリケーション起動中に別の窓で操作を行うのも、はじめはこれで大丈夫なのか、起動中のアプリケーションへの影響はどうなのか、など起動までの構成とは違い少し緊張した。

- yarnのインストールできず長考
    一度はyarn -vでインストールの確認ができた後日改めて確認すると消えている？
    また再インストールさせると失敗している？
    
    ```
    # 試したコードと結果
    npm update -g npm
    $ npm install yarn@1.22.19
    up to date, audited 5 packages in 2s
    found 0 vulnerabiliti
    ```
    
    [公式ドキュメント-インストール](https://chore-update--yarnpkg.netlify.app/ja/docs/install#linux-tab)  
    [参考サイト](https://yularis.com/nvm-permission-error/)で紹介されている通り、一度Nodeをアンインストールしてみてから再度試したら成功した。