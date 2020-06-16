# WSL覚書
###### Create 2020-06-16 01:34:32,Update 2020-06-16 11:05:17
この記事には、自分がWSLを触ってやったこと・ハマったことを書く。  
基本的にLinuxなど含め初心者なので、めちゃくちゃなことを書いてると思う。  
肥大化したらページの分割を考える。

# 環境
気分で追記するかも
- HW:Surface Pro3
- OS:Kali Linux

# 手順
何かやったら追記していく
## Windows側で行う下準備
### Windows Update
普段からやろうね
### WSLの有効化
[設定]→[Windowsの機能]を検索→[Windows Subsystem for Linux]にチェックを入れる→再起動  
→これをやっておかないとWSL起動時に以下のエラーが出る
```bash
Installation Failed!
Error: 0x8007019e
Press any key to continue...
```
### Linuxのインストール
[Microsoft Store]→[kali linux]を検索→Install<br>

## OSのInstall他
### [Kali Linux]の起動
```shell
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: Hoge
adduser: Please enter a username matching the regular expression configured #初期設定のネーミングルールに違反
via the NAME_REGEX configuration variable.  Use the `--force-badname`       #ルールは変えられる模様
option to relax this check or reconfigure NAME_REGEX.                       #
Enter new UNIX username: hoge
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Installation successful!
```

### aptのリポジトリが古いので更新
```shell
$ apt help
～省略～
Most used commands:
～省略～
  update - update list of available packages
～省略～

$ sudo apt update
We trust you have received the usual lecture from the local System  #あなたはシステム管理者から通常の講習を受けたはずです。

Administrator. It usually boils down to these three things:         #これは通常、以下の3点に要約されます:

    #1) Respect the privacy of others.                              #    #1) 他人のプライバシーを尊重すること。
    #2) Think before you type.                                      #    #2) タイプする前に考えること。
    #3) With great power comes great responsibility.                #    #3) 大いなる力には大いなる責任が伴うこと。

Get:1 http://ftp.ne.jp/Linux/packages/kali/kali kali-rolling InRelease [30.5 kB]
Get:2 http://ftp.ne.jp/Linux/packages/kali/kali kali-rolling/main amd64 Packages [17.2 MB]
Get:3 http://ftp.ne.jp/Linux/packages/kali/kali kali-rolling/non-free amd64 Packages [187 kB]
Get:4 http://ftp.ne.jp/Linux/packages/kali/kali kali-rolling/contrib amd64 Packages [105 kB]
Fetched 17.5 MB in 4s (4,095 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
144 packages can be upgraded. Run 'apt list --upgradable' to see them.
	</pre>
	<br>
	ついでにupgrade<br>
	<pre class="prettyprint linenums lang-bsh">
$ apt help
～省略～
Most used commands:
～省略～
  upgrade - upgrade the system by installing/upgrading packages
  full-upgrade - upgrade the system by removing/installing/upgrading packages
～省略～

$ sudo apt full-upgrade
～省略～
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
```