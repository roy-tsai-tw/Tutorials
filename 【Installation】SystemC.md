# SystemC安裝指南  

## 0.安裝資料夾
* /usr/local/systemc-2.3.3
```
[root@localhost local]# ls
bin  etc  games  include  lib  lib64  libexec  sbin  share  src  systemc-2.3.3  systemc-2.3.3.tar.gz
```
## 1.下載SystemC 
* 本指南以SystemC-2.3.3為例，我下載的版本是SystemC 2.3.3 (Includes TLM)。下載完後移動到"/usr/local/"資料夾底下。  
```
https://www.accellera.org/downloads/standards/systemc
```
## 2.解壓縮檔案。
```
tar -zxvf systemc-2.3.3.tar.gz
```
## 3.Configure
```
cd systemc-2.3.3
mkdir objdir
cd objdir
../configure --prefix=/usr/local/systemc-2.3.3
```
## 4.Make the library
```
make
```
## 5.Install the library in your system
```
make install
```
* 接著會在terminal跑出類似底下的訊息:

```
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating src/systemc.pc
config.status: creating src/tlm.pc
config.status: creating src/sysc/Makefile
config.status: creating src/sysc/packages/boost/Makefile
config.status: creating src/sysc/packages/qt/Makefile
config.status: creating src/tlm_core/Makefile
config.status: creating src/tlm_utils/Makefile
config.status: creating examples/Makefile
config.status: creating examples/sysc/Makefile
config.status: creating examples/tlm/Makefile
config.status: creating examples/tlm/common/Makefile
config.status: creating docs/Makefile
config.status: creating docs/sysc/doxygen/Doxyfile
config.status: creating docs/tlm/doxygen/Doxyfile
config.status: executing depfiles commands
config.status: executing libtool commands
---------------------------------------------------------------------
Configuration summary of SystemC 2.3.3 for x86_64-unknown-linux-gnu
---------------------------------------------------------------------

 Directory setup (based on classic layout):
   Installation prefix (aka SYSTEMC_HOME):
      /usr/local/systemc-2.3.3
   Header files  : /include
   Libraries     : /lib-linux64
   Documentation : /docs
   Examples      : /examples

 Architecture    : linux64
 Compiler        : /usr/bin/g++ (C/C++)
 
 Build settings:
   Enable compiler optimizations  : yes
   Include debugging symbols      : no
   Coroutine package for processes: QuickThreads
   Enable VCD scopes by default   : yes
   Disable async_request_update   : no
   Phase callbacks (experimental) : no
 
---------------------------------------------------------------------
```

## 6.Create link
```
ln -s /usr/local/systemc-2.3.3/lib-linux64/libsystemc-2.3.3.so /usr/lib/libsystemc-2.3.3.so
```

## 7.解決library path problem
* Error Message: 
```
error while loading shared libraries: libsystemc-2.3.3.so: cannot open shared object file: No such file or directory
```
* The solution is to add a config file under /etc/ld.so.conf.d/ as follows:
```
gedit /etc/ld.so.conf.d/systemc.conf
```

* Add on the following to the file:
```
/usr/local/systemc-2.3.3/lib-linux/ 
/usr/local/systemc-2.3.3/lib-linux64/
```

* Then:
```
ldconfig
```

## Reference
* [SystemC Linux開發環境配置](https://stenlyho.blogspot.com/2008/10/systemc-linux.html)
* [ubuntu中安裝SystemC](https://www.twblogs.net/a/5b896a792b71775d1ce1ae26)
* [Setting up SystemC and Eclipse for C++ hardware simulation](https://karibe.co.ke/2014/02/setting-up-systemc-and-eclipse-for-c-hardware-simulation/)









