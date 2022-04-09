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




