# Internet Problems
## Problem 1. Could not connect to the AI-related SW.
* BCC
* AI Food
  * First, login the corresponding server.
  * Next, check if the corresponding ip port is turned on using the command "netstat" as shown below.
```
msoc@HPC6:~$ netstat
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp       16      0 192.168.1.60:36906      HPC2:netbios-ssn        ESTABLISHED
tcp        0    112 192.168.1.60:ssh        192.168.1.1:64376       ESTABLISHED
tcp        0      0 localhost:postgresql    localhost:57112         ESTABLISHED
tcp        0      0 192.168.1.60:ssh        192.168.1.1:64377       ESTABLISHED
tcp        0      0 192.168.1.60:41559      relay-5ba7ea60.net:http ESTABLISHED
tcp        0      0 localhost:57112         localhost:postgresql    ESTABLISHED
tcp6       0      0 192.168.1.60:8086       192.168.1.1:63494       ESTABLISHED
tcp6       0      0 192.168.1.60:8086       192.168.1.1:53527       ESTABLISHED
tcp6       0      0 192.168.1.60:8086       192.168.1.1:43520       ESTABLISHED
udp        0      0 localhost:50792         localhost:50792         ESTABLISHED
Active UNIX domain sockets (w/o servers)
Proto RefCnt Flags       Type       State         I-Node   Path
unix  2      [ ]         DGRAM                    36435    /run/user/1000/systemd/notify
unix  2      [ ]         DGRAM                    19622    /run/systemd/cgroups-agent
unix  2      [ ]         DGRAM                    19627    /run/systemd/journal/syslog
unix  8      [ ]         DGRAM                    19633    /run/systemd/journal/socket
unix  19     [ ]         DGRAM                    19634    /run/systemd/journal/dev-log
unix  3      [ ]         DGRAM                    19621    /run/systemd/notify
unix  2      [ ]         DGRAM                    22002    @00016
unix  3      [ ]         STREAM     CONNECTED     200477   @/tmp/dbus-ASTf8lkSLc
unix  3      [ ]         STREAM     CONNECTED     23993
unix  3      [ ]         STREAM     CONNECTED     202609
unix  3      [ ]         STREAM     CONNECTED     199665
unix  3      [ ]         STREAM     CONNECTED     199567   /var/run/dbus/system_bus_socket
unix  3      [ ]         STREAM     CONNECTED     202310   /run/systemd/journal/stdout
unix  3      [ ]         STREAM     CONNECTED     204898   /run/systemd/journal/stdout
unix  3      [ ]         STREAM     CONNECTED     199539   @/tmp/.X11-unix/X0
```
   * Or you can use the command "sudo nmap -sT -sU localhost" directly.
```
msoc@HPC6:~$ sudo nmap -sT -sU localhost

Starting Nmap 7.01 ( https://nmap.org ) at 2022-04-07 15:23 CST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00025s latency).
Not shown: 1988 closed ports
PORT     STATE         SERVICE
22/tcp   open          ssh
80/tcp   open          http
111/tcp  open          rpcbind
443/tcp  open          https
631/tcp  open          ipp
2049/tcp open          nfs
5432/tcp open          postgresql
8086/tcp open          d-s-n
111/udp  open          rpcbind
631/udp  open|filtered ipp
2049/udp open          nfs
5353/udp open|filtered zeroconf

Nmap done: 1 IP address (1 host up) scanned in 2.84 seconds
```


