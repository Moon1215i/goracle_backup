<br/>
<p align="center">
<img src="img/img1.png" alt="Moon1215i_twitter">
</a>
</p>
<br/>

# goracle_backup

[README English](https://github.com/Moon1215i/goracle_backup/README.md)

## 概要
* `rsync`を使って、ゴラクルノードのホームディレクトリ内にある`.goracle`ファイルを、VPSからローカルマシンに転送できるコマンドを作成します
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
3. 同時に、ローカルからゴラクルノードへ、バックアップファイルを`.goracle`に転送するコマンドも作成します
4. このリポジトリは、`ssh-key`にも対応しています

## rsyncの機能について
`rsync`は、ファイル同期ツールで、主に異なる場所にあるファイル/ディレクトリを同期するために使用されます。rsyncは、ローカルマシンとリモートマシン間でファイルを同期し、ネットワークを通じてファイルを転送することができます。

rsyncの主な特徴は、変更された部分のみを転送できることです。つまり、ソースと宛先のファイルの差分を計算し、差分のある部分だけを転送することで、大量のデータを転送する際に非常に効率的に動作します。

また、rsyncには他にも以下のような利点があります。

* 転送途中で途切れた場合、途中から再開することができる。
* 複数のファイルを同期する場合、scpよりも速く転送できることがある。
* 転送中に進捗状況が表示されるため、転送状況を確認しやすい。

ゴラクルノードには、おそらくrsyncがインストールされています。`rsync --version`で確認できます。インストールされていない場合は、次のコマンドを実行してインストールしてください。
```sh
sudo apt install rsync
```

## スクリプトの実行

リポジトリを`git clone`し、`goracle_backup`ディレクトリに入り、`goracle_backup.sh`の実行権限を変更します。
<!-- ```sh
git clone https://github.com/Moon1215i/goracle_backup
cd goracle_backup
chmod +x goracle_backup.sh
```

もしくは -->

```
wget https://github.com/Moon1215i/goracle_backup.sh
chmod +x goracle_backup.sh
```

実行します
```sh
./goracle_backup.sh
```

英語か日本語を選択します。パスワードを求めらた場合は、入力します。

`IP Address : 12.34.56.78`は例えです。

```sh
GoraGang@Goracle:~$ ./goracle_backup.sh 

Select a language 言語を選択してください :

1. English
2. 日本語

Enter the number 数字を入力してください : 1

[sudo] password for GoraGang: 


                                       Your GORACLE Node                                          
-----------------------------------------------------------------------------------------------------
IP Address           : 154.26.158.39
User                 : GoraGang
Backup File          : .goracle
Local Directory      : ~/Documents/Goracle_node/Goracle_154.26.158.39/
SSH Port             : 53814
SSH key type         : ed25519
-----------------------------------------------------------------------------------------------------



                             GORACLE Node    =====>>    Local Machine                             
-----------------------------------------------------------------------------------------------------

mkdir -p ~/Documents/Goracle_node/Goracle_154.26.158.39/ && rsync -avz --progress -e 'ssh -i ~/.ssh/id_ed25519 -p 53814' GoraGang@154.26.158.39:.goracle ~/Documents/Goracle_node/Goracle_154.26.158.39/

-----------------------------------------------------------------------------------------------------
To download backup file from the GORACLE Node,run the following command in your local machine's terminal



                             GORACLE Node    <<=====    Local Machine                             
-----------------------------------------------------------------------------------------------------

rsync -avz --progress -e 'ssh -i ~/.ssh/id_ed25519 -p 53814' ~/Documents/Goracle_node/Goracle_154.26.158.39/.goracle GoraGang@154.26.158.39:.goracle

-----------------------------------------------------------------------------------------------------
To upload backup files from your local machine to the GORACLE Node,run the following command in your terminal on the local machine.

Note: Replace ~/.ssh/id_ed25519 with the appropriate path and filename of your private key.
```


## ローカルマシン（Linux,Mac,WSL2の場合）

Terminalを開いて、貼り付けて実行してください。



Note: 
* Linux（Ubuntu）,Mac,WSL2 (Windows Subsystem for Linux 2) ,Windows10及び11(Cygwin使用)で動作確認ができましファイルがある



## Author

* @11ppm
   
