# hdparam
```
yum -y install hdparm
```

## show status
```
hdparm -C /dev/sda  
    現在の IDE 電源モード状況を調べる。  
        unkown      ドライブはこのコマンドをサポートしない  
        active/idel 通常の動作  
        standby     低電力モード、ドライブはスピンダウンしている  
        sleeping    最小電力モード、ドライブは完全に停止している  
```
```
$ hdparm -C /dev/sda
/dev/sda:
 drive state is:  active/idle
```
## settings
念のため、5秒間アクセスが無かったらスタンバイに入る設定を行う
```
$ hdparm -S 1 /dev/sda
```
OS再起動するたびに設定が消えるので、/etc/rc.localにでも記載しておく。  
```
以下のようなシェルを作って停止させる
    1. アンマウント
    2. -C で状態確認、sleepingではない場合は-Y
    3. -C で状態確認、sleepingなら電源断完了
```
OS 側がアンマウントしていても，HDD 内部のキャッシュ内容がフラッシュされていない可能性があるらしいので強制的にフラッシュする。  
```
$ sdparm --command=sync /dev/sdc 
```
