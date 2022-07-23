# NVDLA Installation On CentOS7
This is an attempt to install NVDLA on CentOS7, which is used to run the NVDLA. 
## Virtual Simulator
### 下載Virtual Simulator
```
git clone https://github.com/nvdla/vp.git
cd vp
git submodule update --init --recursive
```
* One submodule could not be cloned.
* Solution: 
```
git clone https://github.com/rth7680/qemu-palcode
```
* Reference:
  * [Git 基礎 - 取得一個 Git 倉儲](https://git-scm.com/book/zh-tw/v2/Git-%E5%9F%BA%E7%A4%8E-%E5%8F%96%E5%BE%97%E4%B8%80%E5%80%8B-Git-%E5%80%89%E5%84%B2)
  * [“git submodule update --init --recursive” failed #480](https://github.com/riscv-collab/riscv-gnu-toolchain/issues/480)
  * 

## Dependencies
### 安裝必要的tools和libraries
```
sudo yum install cmake swig glib2-devel git pixman-devel boost-devel libattr-devel libpcap-devel 'perl(Data::Dumper)' 'perl(YAML)' 'perl(Capture::Tiny)' 'perl(XML::Simple)' java-1.7.0-openjdk-devel.x86_64 libtermcap-devel ncurses-devel libevent-devel readline-devel python-devel
```
### 安裝SystemC 2.3.0
* Please refer to [SystemC安裝指南]()





## Reference 
* [Virtual Platform On AWS FPGA](http://nvdla.org/vp_fpga.html)(Installation Steps for CentOS)
* 











