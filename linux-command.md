# linux command

## sortコマンド
```
覚えておくと便利なオプション
-S
使用メモリ容量の上限を設定 e.g., sort -S 500M
-m
ソート済みのファイルマージするオプション e.g., sort -m hoge1.sorted hoge2.sorted hoge3.sored > hoge.sorted
-T
一時ファイルの保存先を変更する e.g., sort -T ./
-n
数値として比較
-r
逆順でソート（数値の場合，降順）
```

## 古い CentOS image iso
http://archive.kernel.org/centos-vault/6.5/isos/x86_64/

## Ubuntu version
```
$ lsb_release -a
```

## 国内IP制限 
https://inaba-serverdesign.jp/blog/20150209/ipset_iptables_country_centos7.html  
https://oxynotes.com/?p=6401  

```
国内IP制限 for iptables
http://multix.jp/delegated-apnic-acl/
DDNS
https://hnakamur.github.io/blog/2016/05/02/use-no-ip-dynamic-dns-on-ubuntu-16.04/
RocketChat
https://qiita.com/salmonosushi/items/2dc6491084d8295f45be
    docker pull mongo
    docker pull rocketchat/rocket.chat
    docker-compose.yml を書き換えるなど
git
$ git clone ssh://nagano@nagano7.kickmogu.com:22/home/nagano/Git/catalog-sales-results-batch.git
Docker
docker create --name kidsgit -h kidsgit -it -e "TZ=Asia/Tokyo" -p 13001:22 -v "/home/nagano/home_kidsgit/:/home2" dev/centos7:1.0
    adduser した後に /home2 に変更
    openssh-server, git 入れる
# docker create --name kidschat -h kidschat -it -e "TZ=Asia/Tokyo" -p 13000:3000 -v "/media/:/media" dev/centos7:1.0
＃＃＃＃＃＃＃＃＃＃＃＃＃＃＃＃
$ iptables -I DOCKER -i ext_if ! -s 8.8.8.8 -j DROP
http://docs.docker.jp/engine/userguide/networking/default_network/container-communication.html
docker.yml の ports を "127.0.0.1:3000:3000" と書けば良いらしい
# アタックに関する iptables の設定、以下が超詳しい
https://oxynotes.com/?p=6401
# 「通過はすべて破棄」にしておいたほうが良いかも
iptables -P FORWARD DROP
# IP Spoofing攻撃対策
iptables -A INPUT -i eth0 -s 127.0.0.1/8 -j DROP
iptables -A INPUT -i eth0 -s 10.0.0.0/8 -j DROP
iptables -A INPUT -i eth0 -s 172.16.0.0/12 -j DROP
iptables -A INPUT -i eth0 -s 192.168.0.0/16 -j DROP
iptables -A INPUT -i eth0 -s 192.168.0.0/24  -j DROP
    しくじると全く通信できなくなるので、時間があるときに
# Smurf攻撃対策+不要ログ破棄
iptables -A INPUT -d 255.255.255.255 -j DROP
iptables -A INPUT -d 224.0.0.1 -j DROP
iptables -A INPUT -d 192.168.0.255 -j DRO
    しくじると全く通信できなくなるので、時間があるときに
icmp_echo_ignore_broadcastsを1にすることでブロードキャスト宛のPingに応答しない
世界の国別 IPv4 割り当てリストを毎日ダウンロードして最新の状態に保つ 
```
## iptablesにログ収集させる
```
-A INPUT -p tcp --dport 80 -j LOG
まずは、先頭で世界中からアクセスされた様子を確認する
数日ログを取ったら、今度はフィルタ後に出力する
結果、減っていればフィルタは効いている事がわかる
```

# Apacheセキュリティ設定
https://qiita.com/bezeklik/items/1c4145652661cf5b2271  
https://qiita.com/shojimotio/items/41a74f314f3e47c018a5  


