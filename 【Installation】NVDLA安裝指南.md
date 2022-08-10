# NVDLA Installation On CentOS7
This is an attempt to install NVDLA on CentOS7, which is used to run the NVDLA. 
## Virtual Simulator
### 1.下載Virtual Simulator
```
git clone https://github.com/nvdla/vp.git
cd vp
git submodule update --init --recursive
```
* One submodule could not be cloned.
  ```
  Clone of 'git://github.com/rth7680/qemu-palcode.git' into submodule path 'roms/qemu-palcode' failed
  Failed to recurse into submodule path 'libs/qbox'
  ```
  * Solution: 
  ```
  [vp] cd libs/qbox/roms
  [roms] git clone https://github.com/rth7680/qemu-palcode
  [roms] cd ..
  [qbox]git submodule update --init --recursive
  ```
  * Reference:
    * [Git 基礎 - 取得一個 Git 倉儲](https://git-scm.com/book/zh-tw/v2/Git-%E5%9F%BA%E7%A4%8E-%E5%8F%96%E5%BE%97%E4%B8%80%E5%80%8B-Git-%E5%80%89%E5%84%B2)
    * [“git submodule update --init --recursive” failed #480](https://github.com/riscv-collab/riscv-gnu-toolchain/issues/480)
    * [Build kernel and boot with QEMU - emutyworks/DevTerm-R01 Wiki](https://github-wiki-see.page/m/emutyworks/DevTerm-R01/wiki/Build-kernel-and-boot-with-QEMU)
    * [Git: git clone --recursive不完整解决方案](https://blog.csdn.net/felaim/article/details/105690980)

## Dependencies
### 1.安裝必要的tools和libraries
```
sudo yum install cmake swig glib2-devel git pixman-devel boost-devel libattr-devel libpcap-devel 'perl(Data::Dumper)' 'perl(YAML)' 'perl(Capture::Tiny)' 'perl(XML::Simple)' java-1.7.0-openjdk-devel.x86_64 libtermcap-devel ncurses-devel libevent-devel readline-devel python-devel
```
### 2.安裝SystemC 2.3.0
* Please refer to [SystemC安裝指南](https://github.com/Roy-Tsai-myaccount/Tutorials/blob/main/%E3%80%90Installation%E3%80%91SystemC.md)
### 3.安裝Lua 5.3.2
```
curl -R -O http://www.lua.org/ftp/lua-5.3.2.tar.gz
tar zxf lua-5.3.2.tar.gz
cd lua-5.3.2
make linux CFLAGS="-fPIC -DLUA_USE_LINUX" test
sudo make install
```
* Problems:
  * Error messages:  
  ```
  lua.c:80:31: fatal error: readline/readline.h: No such file or directory
  ```
  * Solution:
  ```
  yum install readline-devel
  ```
  * Reference: [解决编译错误：“readline/readline.h: No such file or directory”](https://nanxiao.me/readline-readline-h-no-such-file-or-directory/)
  
### 4.安裝Perl
```
wget -O YAML-1.24.tar.gz http://search.cpan.org/CPAN/authors/id/T/TI/TINITA/YAML-1.24.tar.gz
tar -xzvf YAML-1.24.tar.gz
cd YAML-1.24
perl Makefile.PL
make
sudo make install
wget -O IO-Tee-0.65.tar.gz http://search.cpan.org/CPAN/authors/id/N/NE/NEILB/IO-Tee-0.65.tar.gz
tar -xzvf IO-Tee-0.65.tar.gz
cd IO-Tee-0.65
perl Makefile.PL
make
sudo make install
```
* Problems:
  * Error messages:
  ```
  [xx@xx]$ perl Makefile.PL
  Can't locate ExtUtils/MakeMaker.pm in @INC (@INC contains: /usr/local/lib64/perl5 /usr/local/share/perl5  /usr/lib64/perl5/vendor_perl 
  /usr/share/perl5/vendor_perl /usr/lib64/perl5 /usr/share/perl5 .) at Makefile.PL line 7.
  BEGIN failed--compilation aborted at Makefile.PL line 7.
  ```
  * Solution: 
  ```
  yum install perl-CPAN
  ```
  * Reference: [編譯安裝時出現Can't locate ExtUtils/MakeMaker.pm](https://blog.xuite.net/tailsice/twblog/204924951-%E7%B7%A8%E8%AD%AF%E5%AE%89%E8%A3%9D%E6%99%82%E5%87%BA%E7%8F%BECan't+locate+ExtUtils%2FMakeMaker.pm#)


### 5.下載和產生NVDLA CMOD和VMOD
```
git clone https://github.com/nvdla/hw.git
cd hw
git reset --hard <HW verion index>    # HW versison must be matched with virtual simulator, refer to section 'HW verion index' of README.md in nvdla/vp
make
tools/bin/tmake -build cmod_top -build vmod
```

### 6.安裝Virtual Platform
* 注意: 文檔裡面有寫vp/built/這個資料夾，可能是早期的版本才有。目前的版本是在/vp/src/資料夾。
```
cmake -DCMAKE_INSTALL_PREFIX=build -DSYSTEMC_PREFIX=/usr/local/systemc-2.3.0/ -DNVDLA_HW_PREFIX=/home/roy/NVDLA/hw -DNVDLA_HW_PROJECT=nv_full

```
* Problems
  * Boost not found.
  ```
    [vp]$ cmake -DCMAKE_INSTALL_PREFIX=build -DSYSTEMC_PREFIX=/usr/local/systemc-2.3.0/ -DNVDLA_HW_PREFIX=/home/roy/NVDLA/hw -DNVDLA_HW_PROJECT=nv_full
    -- Searching for SystemC
    -- SystemC version = 2.3.0
    -- SystemC library = /usr/local/systemc-2.3.0/lib-linux64/libsystemc.so
    -- Searching for TLM
    running ls /usr/local/systemc-2.3.0/include/tlm.h 2>&1
    /usr/local/systemc-2.3.0/include/tlm.h
    -- TLM library = /usr/local/systemc-2.3.0/include/tlm.h
    -- Searching for NVDLA CMOD
    -- NVDLA HW VERSION = nvdla_os_initial
    -- NVDLA CMOD include directory = /home/roy/NVDLA/hw/outdir/nv_full/cmod/release/include
    -- NVDLA CMOD library directory = /home/roy/NVDLA/hw/outdir/nv_full/cmod/release/lib
    -- NVDLA CMOD library = /home/roy/NVDLA/hw/outdir/nv_full/cmod/release/lib/libnvdla_cmod.so
    -- Searching for SystemC
    -- SystemC version = 2.3.0
    -- SystemC library = /usr/local/systemc-2.3.0/lib-linux64/libsystemc.so
    -- Searching for TLM
    running ls /usr/local/systemc-2.3.0/include/tlm.h 2>&1
    /usr/local/systemc-2.3.0/include/tlm.h
    -- TLM library = /usr/local/systemc-2.3.0/include/tlm.h
    -- Could NOT find Boost
    CMake Error at libs/greenlib/CMakeLists.txt:44 (message):
      Boost library not found.
      
      
    -- Configuring incomplete, errors occurred!
    See also "/home/roy/NVDLA/vp/CMakeFiles/CMakeOutput.log".
  ```
  * Solution:  sudo yum install boost-devel
  * Python not found.
  ```
      running ls /usr/local/systemc-2.3.0/include/tlm.h 2>&1
    /usr/local/systemc-2.3.0/include/tlm.h
    -- TLM library = /usr/local/systemc-2.3.0/include/tlm.h
    -- Boost version: 1.53.0
    CMake Error at /usr/share/cmake/Modules/FindPackageHandleStandardArgs.cmake:108 (message):
      Could NOT find PythonLibs (missing: PYTHON_LIBRARIES PYTHON_INCLUDE_DIRS)
    Call Stack (most recent call first):
      /usr/share/cmake/Modules/FindPackageHandleStandardArgs.cmake:315 (_FPHSA_FAILURE_MESSAGE)
      /usr/share/cmake/Modules/FindPythonLibs.cmake:197 (FIND_PACKAGE_HANDLE_STANDARD_ARGS)
      libs/greenlib/CMakeLists.txt:52 (find_package)


    -- Configuring incomplete, errors occurred!
    See also "/home/roy/NVDLA/vp/CMakeFiles/CMakeOutput.log".
  ```
  * Solution: sudo yum install python-devel

```
make
```
* Problems: 
  * zlib not installed 
    ```
    [  4%] Creating directories for 'qbox'
    [  5%] No download step for 'qbox'
    [  7%] No update step for 'qbox'
    [  8%] No force-build step for 'qbox'
    [  8%] No patch step for 'qbox'
    [ 10%] Performing configure step for 'qbox'

    ERROR: zlib check failed
           Make sure to have the zlib libs and headers installed.

    make[2]: *** [libs/qbox.build/stampdir/qbox-configure] Error1
    make[1]: *** [CMakeFiles/qbox.dir/all] Error 2
    make: *** [all] Error 2

    ```
    * Solution: sudo yum install zlib-devel
  * ERROR: glib-2.22 gthread-2.0 is required to compile QEMU
    * Solution:  yum install glib2-devel
  * 
```
make install
```
### Running Virtual Platform
```
export SC_SIGNAL_WRITE_CHECK=DISABLE
./build/bin/aarch64_toplevel -c conf/aarch64_nvdla.lua
```
* Problems:
  * Error message:
  ```
  [vp]$ ./build/bin/aarch64_toplevel -c conf/aarch64_nvdla.lua

             SystemC 2.3.0-ASI --- Jul 24 2022 01:36:02
        Copyright (c) 1996-2012 by all Contributors,
        ALL RIGHTS RESERVED

  No sc_log specified, will use the default setting
  verbosity_level = SC_MEDIUM
  DMI mode enable
  RAM base address: 0xc0000000
  bridge: tlm2c_elaborate..
  toplevel: -device virtio-9p-device,fsdev=r,mount_tag=r: 'virtio-9p-device' is not a valid device model name
  ```
  * Solution: The qemu-virtio dependices are not installed. Install two 9p virtio dependices.
  ``` 
  sudo yum install -y libcap-devel
  sudo yum install -y libattr-devel
  ```

```
Welcome to Buildroot
buildroot login: root
Password:

Running Examples: 
Example 1:
Enter:
# mount -t 9p -o trans=virtio r /mnt
# cd /mnt/tests/hello
# ./aarch64_hello

Output:
Hello World!

Example 2:
Enter:
# cd nvdla_bdma_mmio/
# ./aarch64_nvdla_bdma_mmio

Output:
Start programming...
Write reg 0x00004004, value 0x00000000
Write reg 0x00004000, value 0xc0000000
Write reg 0x0000400c, value 0x00000000
Write reg 0x00004008, value 0xc00017c0
Write reg 0x0000402c, value 0x00000800
Write reg 0x00004020, value 0x00000100
Write reg 0x00004028, value 0x00000800
Write reg 0x0000401c, value 0x00000100
Write reg 0x00004024, value 0x00000000
Write reg 0x00004018, value 0x00000007
Write reg 0x00004010, value 0x00000007
Write reg 0x00004014, value 0x00000003
Write reg 0x00004030, value 0x00000001
Write reg 0x00004034, value 0x00000001
Finish programming...

Get BDMA interrupt ...
```

## Reference 
* [Virtual Platform On AWS FPGA](http://nvdla.org/vp_fpga.html)(Installation Steps for CentOS)
* 











