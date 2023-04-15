<br/>
<p align="center">
<img src="img/img1.png" width="400" alt="Moon1215i_twitter">
</a>
</p>
<br/>

# goracle_backup

[README English](https://github.com/Moon1215i/goracle_backup/README.md)
 
<br>
<br>

# 1. 概要
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
 
<br>
<br>

# 2. 機能
1. CSVファイルから英語と日本語のメッセージを読み込み、選択された言語に応じてメッセージを表示します
2. ゴラクルノードの`.goracle`を、ローカルに転送するコマンドを作成します
3. 同時に、ローカルからゴラクルノードへ、バックアップファイルを`.goracle`に転送するコマンドも作成します
4. このリポジトリは、`ssh-key`にも対応しています
 
<br>
<br>

# 3. rsyncの機能について
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
 
<br>
<br>

## 4. スクリプトの実行

<!--
リポジトリを`git clone`し、`goracle_backup`ディレクトリに入り、`goracle_backup.sh`の実行権限を変更します。
```sh
git clone https://github.com/Moon1215i/goracle_backup
cd goracle_backup
chmod +x goracle_backup.sh
```
もしくは -->
<br>

### 4-1
次のコマンドを実行し、Goracleノードのホームディレクトリに`goracle_backup.sh`ファイルをダウンロードし実行権限を変更します。
```
cd ~ && curl -O https://raw.githubusercontent.com/Moon1215i/goracle_backup/main/goracle_backup.sh
chmod +x goracle_backup.sh
```

<br>

### 4-2
シェルスクリプトを実行します
```sh
./goracle_backup.sh
```

英語か日本語を選択します。パスワードを求めらた場合は、入力します。

以下のようなプロンプトになります。

`IP Address : 12.34.56.78`は例えです。

```sh
GoraGang@Goracle:~$ ./goracle_backup.sh 

Select a language 言語を選択してください :

1. English
2. 日本語

Enter the number 数字を入力してください : 1



                                       Your GORACLE Node                                          
-----------------------------------------------------------------------------------------------------
IP Address           : 12.34.56.78
User                 : GoraGang
Backup File          : .goracle
Local Directory      : ~/Documents/Goracle_node/Goracle_12.34.56.78/
SSH Port             : 54865
SSH key type         : ed25519
-----------------------------------------------------------------------------------------------------




                             GORACLE Node    =====>>    Local Machine                             
-----------------------------------------------------------------------------------------------------

mkdir -p ~/Documents/Goracle_node/Goracle_12.34.56.78/ && rsync -avz --progress -e 'ssh -i ~/.ssh/id_ed25519 -p 54865' GoraGang@12.34.56.78:.goracle ~/Documents/Goracle_node/Goracle_12.34.56.78/

-----------------------------------------------------------------------------------------------------
To download backup file from the GORACLE Node,run the following command in your local machine's terminal




                             GORACLE Node    <<=====    Local Machine                             
-----------------------------------------------------------------------------------------------------

rsync -avz --progress -e 'ssh -i ~/.ssh/id_ed25519 -p 54865' ~/Documents/Goracle_node/Goracle_12.34.56.78/.goracle GoraGang@12.34.56.78:.goracle

-----------------------------------------------------------------------------------------------------
To upload backup files from your local machine to the GORACLE Node,run the following command in your terminal on the local machine.

Note: Replace ~/.ssh/id_ed25519 with the appropriate path and filename of your private key.
```

<br>

#### 4-3
上記の2つの`rsync`コマンドをコピーして、メモ帳にでも保存してください。
 
<br>
<br>

# 5. ローカルマシン（Linux,Mac,WSL2の場合）

Terminalを開いて、先ほどのコマンドを貼り付けて、実行してください。
 
<br>
<br>

Note: 
* Linux（Ubuntu）,Mac,WSL2 (Windows Subsystem for Linux 2) ,Windows10及び11(Cygwin使用)で動作確認ができましファイルがある
 
<br>
<br>

## Author

* @11ppm
   
