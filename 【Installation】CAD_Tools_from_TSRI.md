# CAD Tool Installation Problems & Solutions
* Please follow the steps from TSRI to install those EDA tools. I only list some problems and solutions I've faced before.


## EDA Tools: Command Not Found 

### Conformal LEC
* Solution: 
  * Change the following command in /usr/cad/cadence/CIC/confrml.cshrc file:  
```
set bin_prefix 	= "tools/bin"

           to
              
              
set bin_prefix 	= "bin"
```
  * You may also need to install another tool called lsb:
```
sudo yum install -y redhat-lsb
```
  * Reference:[CentOS 7 命令lsb_release: command not found解决方案](https://blog.csdn.net/xufengzhu/article/details/73330741)
