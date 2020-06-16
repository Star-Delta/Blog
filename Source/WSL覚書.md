# WSL覚書
###### Create 2020-06-16 01:34:32
この記事には、自分がWSLを触ってやったこと・ハマったことを書く。  
基本的にLinuxなど含め初心者なので、めちゃくちゃなことを書いてると思う。  
肥大化したらページの分割を考える。

# 環境
気分で追記するかも
- HW:Surface Pro3
- OS:Kali Linux

# やったこと
何かやったら追記していく
## Windows側で行う下準備
### Windows Update
普段からやろうね
### WSLの有効化
[設定]→[Windowsの機能]を検索→[Windows Subsystem for Linux]にチェックを入れる→再起動  
→これをやっておかないとWSL起動時に以下のエラーが出る
```shell
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
```

ついでにupgrade
```shell
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

## rootのパスワード変更
Debian系のLinuxはsudoの利用を推奨しているらしい。
でもそんなの関係ねぇって人は変更しましょう。
`$ sudo password root`
今回は、変更しないことに。

## vimの準備
viが古かったのでupgarade  
full-upgradeで最新になってると思ったんやけどな…
```shell
$ sudo apt upgrade vim
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  libfreetype6 libglib2.0-0 libglib2.0-data libgraphite2-3 libharfbuzz0b libicu-le-hb0 libicu60 libpng16-16
  shared-mime-info xdg-user-dirs
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  libgpm2 vim vim-runtime
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 7,090 kB of archives.
After this operation, 33.3 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://ftp-srv2.kddilabs.jp/Linux/packages/kali/kali kali-rolling/main amd64 libgpm2 amd64 1.20.7-5 [35.1 kB]
Get:2 http://ftp-srv2.kddilabs.jp/Linux/packages/kali/kali kali-rolling/main amd64 vim-runtime all 2:8.1.0875-1 [5,77
5 kB]
Get:3 http://ftp-srv2.kddilabs.jp/Linux/packages/kali/kali kali-rolling/main amd64 vim amd64 2:8.1.0875-1 [1,280 kB]
Fetched 7,090 kB in 1min 13s (97.1 kB/s)
Selecting previously unselected package libgpm2:amd64.
(Reading database ... 17510 files and directories currently installed.)
Preparing to unpack .../libgpm2_1.20.7-5_amd64.deb ...
Unpacking libgpm2:amd64 (1.20.7-5) ...
Selecting previously unselected package vim-runtime.
Preparing to unpack .../vim-runtime_2%3a8.1.0875-1_all.deb ...
Adding 'diversion of /usr/share/vim/vim81/doc/help.txt to /usr/share/vim/vim81/doc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim81/doc/tags to /usr/share/vim/vim81/doc/tags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:8.1.0875-1) ...
Selecting previously unselected package vim.
Preparing to unpack .../vim_2%3a8.1.0875-1_amd64.deb ...
Unpacking vim (2:8.1.0875-1) ...
Setting up libgpm2:amd64 (1.20.7-5) ...
Processing triggers for libc-bin (2.28-2) ...
Setting up vim-runtime (2:8.1.0875-1) ...
Setting up vim (2:8.1.0875-1) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdiff) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in auto mode
```

.vimrcを作成。  
```shell
$ touch .vimrc
```

中身は[こんな感じ](https://github.com/Star-Delta/vimrc/blob/master/.vimrc)