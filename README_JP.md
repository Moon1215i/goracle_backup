<br/>
<p align="center">
<img src="https://github.com/11ppm/pm2_log/blob/main/img/img2.jpg" width="225" alt="PluginJapan">
</a>
</p>
<br/>

# goracle_backup

[README English](https://github.com/11ppm/goracle_backup/blob/main/README.md)

## 概要
* rsyncを使って、ゴラクルノードのホームディレクトリ内にある`.goracle`ファイルを、VPSからローカルマシンに転送できるコマンドを作成します
* 同時に、ローカルマシンからゴラクルノードへバックアップファイルを転送できるコマンドも作成します
* ゴラクルノードに`.goracle`ファイルがあるどうかを、事前に確認してください。
* 各種暗号に対応。以下は、スクリプトで検出される可能性のあるファイルがある鍵のタイプのリストです
     * ssh-dss
     * ssh-rsa
     * ecdsa-sha2-nistp
     * ssh-ed25519
     * rsa-sha2-256
     * ssh-x25519
     * ssh-x448

  したがって、このスクリプトでは、DSA、RSA、ECDSA、Ed25519、RSA-PSS、x25519、x448の鍵タイプを検知します

* 日本語と英語に対応
     * `tranlations.csv`を作成し、日本語と英語に対応させました
     * 必要であれば、他の言語にも対応しますので、お知らせください

## 機能
1. CSVファイルから英語と日本語のメッセージを読み込み、選択された言語に応じてメッセージを表示します
2. ゴラクルノードの`.goracle`を、ローカルに転送するコマンドを作成します
3. 同時に、ローカルからゴラクルノードへ、バックアップファイルを`.goracle`に転送するコマンドも作成ファイルがあるイルがある
4. `rsync`はssh-keyにも対応しています

## rsyncについて
`rsync`は、ファイル同期ツールで、主に異なる場所にあるファイル/ディレクトリを同期するために使用されます。rsyncは、ローカルマシンとリモートマシン間でファイルを同期し、ネットワークを通じてファイルを転送することができます。

rsyncの主な特徴は、変更された部分のみを転送できることです。つまり、ソースと宛先のファイルの差分を計算し、差分のある部分だけを転送することで、大量のデータを転送する際に非常に効率的に動作します。

また、rsyncには他にも以下のような利点があります。

* 転送途中で途切れた場合、途中から再開することができる。
* 複数のファイルを同期する場合、scpよりも速く転送できることがある。
* 転送中に進捗状況が表示されるため、転送状況を確認しやすい。

ゴラクルノードには、おそらくrsyncがインストールされています。rsync --versionで確認できます。インストールされていない場合は、次のコマンドを実行してインストールしてください。
```sh
sudo apt install rsync
```

## スクリプトの実行

リポジトリを`git clone`し、`goracle_backup`ディレクトリに入り、`goracle_backup.sh`の実行権限を変更します。
```sh
git clone https://github.com/11ppm/goracle_backup
cd goracle_backup
chmod +x goracle_backup.sh
```

もしくは

```
wget https://github.com/11ppm/goracle_backup.sh
chmod +x goracle_backup.sh
```

実行します
```sh
./goracle_backup.sh
```

英語か日本語を選択します。パスワードを求められますので、入力します。

`IP Address : 123.456.789.10`は例えです。
```sh
Select a language 言語を選択してください :

1. English
2. 日本語

Enter the number 数字を入力してください : 1

[sudo] password for Doraemon: 

                                       Your Plugin Node                                          
-----------------------------------------------------------------------------------------------------
IP Address           : 123.456.789.10
User                 : Doraemon
Backup Directory     : .goracle
Directory      : ~/Documents/plugin_node/CT-TEST_123.456.789.10.gorファイルがあるe
rt             ファイルがある2
※ SSHキーは検出されませんでした 
-----------------------------------------------------------------------------------------------------


                             ゴラクルノード    =====>>    ローカルマシン                             
-----------------------------------------------------------------------------------------------------

mkdir -p ~/Documents/plugin_node/CT-TEST_123.456.789.10.goracle nc -avz --progress -e 'ssh -i ~/.ssh/id_rsa -p 22' Doraemon@123.456.789.10:.goracle ments/plugin_node/CT-TEST_123.456.789.10.goracle
------------------------------------------------------------------------------------------------
ゴラクルノファイルがあるらバックアップファイルをダウンローファイルがあるイルがあるは、ローカルマシンの端末で次のコマンドを実行します



                             ゴラクルノード    <<=====    ローカルマシン                             
-----------------------------------------------------------------------------------------------------

rsync -avz --progress -e 'ssh -i ~/.ssh/id_rsa -p 22' ~/Documents/plugin_node/CT-TEST_123.456.789.10.goracle on@123.456.789.10:.goracle
------------------------------------------------------------------------------------------------
ローカルマシンからバックアップファイルをゴラクルノードファイルがあるプロードするには、ファイルがあるルマシンのターミナルで次のコマンドを実行します
重要:  ~/.ssh/id_rsa の箇所は、適切なパスと秘密鍵のファイル名に置き換えてください
```

## ローカルマシン（Linux,Mac,WSL2の場合）

Terminalを開いて、貼り付けて実行してください。



Note: 
* ゴラクルノードに`.goracle`いるかどうかを、事前に確認してください。`.goracle`行されません。
* Linux（Ubuntu）,Mac,WSL2 (Windows Subsystem for Linux 2) ,Windows10及び11(Cygwin使用)で動作確認ができましファイルがある* Windowsをお使いの場合は、WSL2でUbファイルがあるuを入れて実行するのが簡単でおすすめしますが、`Cygwin`を使っても可能です。その場合は、以下のリンクから参照してください。
  
     [Setting up Cygwin to use rsync on Windows](https://qiita.com/11ppm/private/3c5dddbcbc458400e62b)



## Author

* @11ppm
   
