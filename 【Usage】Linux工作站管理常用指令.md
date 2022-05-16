# Linux工作站管理常用指令
## 檔案管理
### 建立檔案
* 單一檔案
```
touch example.txt
```
* 資料夾
```
mkdir folder
```
### 刪除檔案
* 單一檔案
```
rm example.txt
```
* 非空資料夾
```
rm -f folder/
```
* 空資料夾
```
rm -d folder
```
### 解壓縮指令
* .tar
```
tar xvf FileName.tar
```
* .gzip
```
gzip -d FileName.gz
```
* .tar.gz
```
tar zxvf FileName.tar.gz
```
### 壓縮指令
* .tar
```
tar cvf FileName.tar DirName
```
* .gzip
```
gzip FileName
```
* .tar.gz
```
tar zcvf FileName.tar.gz DirName
```
### rpm下載及安裝
* Download file from URL on Linux using command line
```
wget URL
```
* Install RPM
```
rpm -ivh package.rpm
```
## 帳號管理
### 新增使用者
*
```
useradd your_name
passwd your_name
```
### 新增使用者至sudo群組
* 新增使用者至sudo群組
```
usermod -aG sudo your_name
```
* 切換root到該使用者群組
```
sudo su - your_name
```
* 測試該帳號是否能使用sudo功能
```
sudo ls -la /root
```
* 撤銷該使用者的sudo權限
```
sudo deluser your_name sudo
```
### 設定帳號使用期限
* 設定帳號使用期限
```
sudo useradd -e 2023-04-16 your_name
```
* 查詢帳號使用期限
```
sudo chage -l your_name
```
* 設定帳號過期之後真正會撤銷帳號的期限
```
ex: 帳號過期後45天真正撤銷帳號
sudo useradd -f 45 your_name
```
### 設定帳號使用者的初始shell
* 指定登入者的shell
```
sudo useradd -s /sbin/csh your_name
```
## 網路管理
### 允許(工作站主機)防火牆開啟特定port
* 檢查某port是否有開啟
```
firewall-cmd --zone=public --list-all
```
* 加入特定port(底下範例為port 1234)
```
firewall-cmd --zone=public --add-port=1234/tcp --permanent
```
* 重新讀取firewall設定
```
firewall-cmd --reload
```
* 檢查該port是否已加入允許的list
```
firewall-cmd --zone=public --list-all
```
## 主機資訊
### 查詢主機名稱
* 顯示主機名稱
```
hostname -s
```
* 顯示主機的DNS網域名稱
```
hostname -d
```
* 顯示主機別名(if any)
```
hostname -a
```
### 更改主機名稱
* 查詢主機設定
```
hostnamectl
```
* 更改主機名稱(範例改為: MyHost)
```
hostnamectl set-hostname MyHost
```
* 更改主機別名(參考hosts線上手冊)
```
In /etc/hosts:
man hosts
```
## YUM Lock
* Solve yum lock in CentOS 7
```
ps -ef | grep yum
kill -9 PID_NUMBER or pkill PackageKit
```
  * Reference: [“Another app is currently holding the yum lock”](https://www.thegeekdiary.com/yum-command-fails-with-another-app-is-currently-holding-the-yum-lock-in-centos-rhel-7/)





```


