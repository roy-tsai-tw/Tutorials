# NVDLA Installation On CentOS7
This is an attempt to install NVDLA on CentOS7, which is used to run the NVDLA. 
## 下載Virtual Simulator
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
* Reference:[Git 基礎 - 取得一個 Git 倉儲](https://git-scm.com/book/zh-tw/v2/Git-%E5%9F%BA%E7%A4%8E-%E5%8F%96%E5%BE%97%E4%B8%80%E5%80%8B-Git-%E5%80%89%E5%84%B2)

## 安裝相關的tools和libraries
















