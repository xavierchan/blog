---
title: Linux
date: 2018-04-13 11:41:26
tags:
categories:
---

### 操作系统的历史

UNIX -> BSD -> GNU -> Linux

### 操作系统信息

    uname -a

### du - 磁盘使用统计(display disk usage statistics)

### df - 磁盘剩余空间(display free disk space)

### fdisk - (DOS partition maintenance program)

### ps - 进程的快照(Process Status)

    ps

### 进程

```shell
top
```

### 查看CPU

```shell
lscpu
```

### 网络状态

```shell
netstat

```

### 权限控制

```shell
chmod 777 yeah.py # 为文件修改权限
chmod -R 700 /opt/oracle/ # 为目录下所有文件修改权限
```

### 光标移动

ctr+a：移动光标到命令行开始处（紧接命令提示符号）
ctr+e：移动光标到命令行行尾
ctr+k：删除光标到命令行行尾
ctr+u：删除光标到命令行开始处
ctr+h  往后删除一字符      ctr+d 往前删除一字符
ctr+b  光标往前            ctr+f 往后
ctr+u   删除到最前         ctr+K删除到最后
ctr+a  光标到最前          ctr+e 光标到最后
ctr+p   往上一条历史命令   ctr+n  往下一条命令

### 文件操作

```bash
scp -i <identity> -P<port> <src\_file> root@<ip>:<dest\_path> # 安全拷贝
```

### 权限查看

```shell
$ groupadd elsearch # 添加组
$ useradd elsearch -g elsearch -p elasticsearch # 添加用户

$ cat /etc/passwd # 可以查看所有用户的列表
$ w # 可以查看当前活跃的用户列表
$ cat /etc/group # 查看用户组
用户组（Group）、用户组口令、GID及该用户组所包含的用户（User）
daemon:x:2:root,bin,daemon
```

### 查找命令

    find <path> -name <name> or -name <name>

### 查看存储大小

```shell
du -h --max-depth=1 ./
```

### 根据端口查进程

```shell
lsof -i:<port>
    kill
```

### 测试远端服务是否可用

```shell
telnet <ip> <port>
```

### 安全拷贝

    scp [option] source_target dest_target
    eg. scp -i file -P 3780 a.tar.gz root@127.0.0.1:/var

### 配置ssh服务

    sudo apt-get update
    sudo apt-get install openssh-server
    ps -e | grep ssh # sshd 为 服务端，ssh-client 为客户端

## ufw

    ubuntu的防火墙服务
    sudo ufw allow 3307 # 直接开启端口

检查是否安装mysql
rpm -qa|grep mysql

### 常用系统默认端口

|端口|服务|说明|
|:-:|:-:|:-:|
|0|Reserved|通常用于分析操作系统。这一方法能够工作是因为在一些系统中“0”是无效端口，当你试图使用通常的闭合端口连接它时将产生不同的结果。一种典型的扫描，使用IP地址为0.0.0.0，设置ACK位并在以太网层广播。|
|1|tcpmux|这显示有人在寻找SGI Irix机器。Irix是实现tcpmux的主要提供者，默认情况下tcpmux在这种系统中被打开。Irix机器在发布是含有几个默认的无密码的帐户，如：IP、GUEST UUCP、NUUCP、DEMOS 、TUTOR、DIAG、OUTOFBOX等。许多管理员在安装后忘记删除这些帐户。因此HACKER在INTERNET上搜索tcpmux并利用这些帐户。|
|7|Echo|能看到许多人搜索Fraggle放大器时，发送到X.X.X.0和X.X.X.255的信息。|
|19|Character Generator|这是一种仅仅发送字符的服务。UDP版本将会在收到UDP包后回应含有垃圾字符的包。TCP连接时会发送含有垃圾字符的数据流直到连接关闭。HACKER利用IP欺骗可以发动DoS攻击。伪造两个chargen服务器之间的UDP包。同样Fraggle DoS攻击向目标地址的这个端口广播一个带有伪造受害者IP的数据包，受害者为了回应这些数据而过载。|
|21|FTP|FTP服务器所开放的端口，用于上传、下载。最常见的攻击者用于寻找打开anonymous的FTP服务器的方法。这些服务器带有可读写的目录。木马Doly Trojan、Fore、Invisible FTP、WebEx、WinCrash和Blade Runner所开放的端口。|
|22|Ssh|PcAnywhere建立的TCP和这一端口的连接可能是为了寻找ssh。这一服务有许多弱点，如果配置成特定的模式，许多使用RSAREF库的版本就会有不少的漏洞存在。|
|23|Telnet|远程登录，入侵者在搜索远程登录UNIX的服务。大多数情况下扫描这一端口是为了找到机器运行的操作系统。还有使用其他技术，入侵者也会找到密码。木马Tiny Telnet Server就开放这个端口。|
|25|SMTP|SMTP服务器所开放的端口，用于发送邮件。入侵者寻找SMTP服务器是为了传递他们的SPAM。入侵者的帐户被关闭，他们需要连接到高带宽的E-MAIL服务器上，将简单的信息传递到不同的地址。木马Antigen、Email Password Sender、Haebu Coceda、Shtrilitz Stealth、WinPC、WinSpy都开放这个端口。|
|31|MSG Authentication|木马Master Paradise、Hackers Paradise开放此端口。|
|42|WINS Replication|WINS复制|
|53|Domain Name Server（DNS）|DNS服务器所开放的端口，入侵者可能是试图进行区域传递（TCP），欺骗DNS（UDP）或隐藏其他的通信。因此_blank">防火墙常常过滤或记录此端口。|
|67|Bootstrap Protocol Server|通过DSL和Cable modem的_blank">防火墙常会看见大量发送到广播地址255.255.255.255的数据。这些机器在向DHCP服务器请求一个地址。HACKER常进入它们，分配一个地址把自己作为局部路由器而发起大量中间人（man-in-middle）攻击。客户端向68端口广播请求配置，服务器向67端口广播回应请求。这种回应使用广播是因为客户端还不知道可以发送的IP地址。|
|69|Trival File Transfer|许多服务器与bootp一起提供这项服务，便于从系统下载启动代码。但是它们常常由于错误配置而使入侵者能从系统中窃取任何 文件。它们也可用于系统写入文件。|
|79|Finger Server|入侵者用于获得用户信息，查询操作系统，探测已知的缓冲区溢出错误，回应从自己机器到其他机器Finger扫描。|
|80|HTTP|用于网页浏览。木马Executor开放此端口。
|99|Metagram Relay|后门程序ncx99开放此端口。|
|102|Message transfer agent(MTA)-X.400 over TCP/IP|消息传输代理。|
|109|Post Office Protocol -Version3|POP3服务器开放此端口，用于接收邮件，客户端访问服务器端的邮件服务。POP3服务有许多公认的弱点。关于用户名和密码交 换缓冲区溢出的弱点至少有20个，这意味着入侵者可以在真正登陆前进入系统。成功登陆后还有其他缓冲区溢出错误。|
|110|SUN公司的RPC服务所有端口|常见RPC服务有rpc.mountd、NFS、rpc.statd、rpc.csmd、rpc.ttybd、amd等|
|113|Authentication Service|这是一个许多计算机上运行的协议，用于鉴别TCP连接的用户。使用标准的这种服务可以获得许多计算机的信息。但是它可作为许多服务的记录器，尤其是FTP、POP、IMAP、SMTP和IRC等服务。通常如果有许多客户通过_blank">防火墙访问这些服务，将会看到许多这个端口的连接请求。记住，如果阻断这个端口客户端会感觉到在_blank">防火墙另一边与E-MAIL服务器的缓慢连接。许多_blank">防火墙支持TCP连接的阻断过程中发回RST。这将会停止缓慢的连接。|
|119|Network News Transfer Protocol| NEWS新闻组传输协议，承载USENET通信。这个端口的连接通常是人们在寻找USENET服务器。多数ISP限制，只有他们的客户才能访问他们的新闻组服务器。打开新闻组服务器将允许发/读任何人的帖子，访问被限制的新闻组服务器，匿名发帖或发送SPAM。
|135|Location Service| Microsoft在这个端口运行DCE RPC end-point mapper为它的DCOM服务。这与UNIX 111端口的功能很相似。使用DCOM和RPC的服务利用计算机上的end-point mapper注册它们的位置。远端客户连接到计算机时，它们查找end-point mapper找到服务的位置。HACKER扫描计算机的这个端口是为了找到这个计算机上运行Exchange Server吗？什么版本？还有些DOS攻击直接针对这个端口。
|137、138、139|NETBIOS Name Service| 其中137、138是UDP端口，当通过网上邻居传输文件时用这个端口。而139端口：通过这个端口进入的连接试图获得NetBIOS/SMB服务。这个协议被用于windows文件和打印机共享和SAMBA。还有WINS Regisrtation也用它。
|143|Interim Mail Access Protocol v2| 和POP3的安全问题一样，许多IMAP服务器存在有缓冲区溢出漏洞。记住：一种LINUX蠕虫（admv0rm）会通过这个端口繁殖，因此许多这个端口的扫描来自不知情的已经被感染的用户。当REDHAT在他们的LINUX发布版本中默认允许IMAP后，这些漏洞变的很流行。这一端口还被用于IMAP2，但并不流行。
|161|SNMP| SNMP允许远程管理设备。所有配置和运行信息的储存在数据库中，通过SNMP可获得这些信息。许多管理员的错误配置将被暴露在Internet。Cackers将试图使用默认的密码public、private访问系统。他们可能会试验所有可能的组合。SNMP包可能会被错误的指向用户的网络。
|177|X Display Manager Control Protocol| 许多入侵者通过它访问X-windows操作台，它同时需要打开6000端口。
|389|LDAP、ILS| 轻型目录访问协议和NetMeeting Internet Locator Server共用这一端口。
|443|Https|网页浏览端口，能提供加密和通过安全端口传输的另一种HTTP。
|456|[NULL]|木马HACKERS PARADISE开放此端口。
|513|Login,remote login| 是从使用cable modem或DSL登陆到子网中的UNIX计算机发出的广播。这些人为入侵者进入他们的系统提供了信息。
|544|[NULL]| kerberos kshell
|548|Macintosh,File Services(AFP/IP)| Macintosh,文件服务。
|553|CORBA IIOP （UDP）| 使用cable modem、DSL或VLAN将会看到这个端口的广播。CORBA是一种面向对象的RPC系统。入侵者可以利用这些信息进入系统。
|555|DSF| 木马PhAse1.0、Stealth Spy、IniKiller开放此端口。
|568|Membership DPA| 成员资格 DPA。
|569|Membership MSN| 成员资格 MSN。
|635|mountd| Linux的mountd Bug。这是扫描的一个流行BUG。大多数对这个端口的扫描是基于UDP的，但是基于TCP的mountd有所增加（mountd同时运行于两个端口）。记住mountd可运行于任何端口（到底是哪个端口，需要在端口111做portmap查询），只是Linux默认端口是635，就像NFS通常运行于2049端口。
|636|LDAP| SSL（Secure Sockets layer）
|666|Doom Id Software| 木马Attack FTP、Satanz Backdoor开放此端口
|993|IMAP| SSL（Secure Sockets layer）
|1001、1011|[NULL]| 木马Silencer、WebEx开放1001端口。木马Doly Trojan开放1011端口。
|1024|Reserved| 它是动态端口的开始，许多程序并不在乎用哪个端口连接网络，它们请求系统为它们分配下一个闲置端口。基于这一点分配从端口1024开始。这就是说第一个向系统发出请求的会分配到1024端口。你可以重启机器，打开Telnet，再打开一个窗口运行natstat -a 将会看到Telnet被分配1024端口。还有SQL session也用此端口和5000端口。
|1025、1033|1025：network blackjack 1033：[NULL]| 木马netspy开放这2个端口。
|1080|SOCKS| 这一协议以通道方式穿过_blank">防火墙，允许_blank">防火墙后面的人通过一个IP地址访问INTERNET。理论上它应该只允许内部的通信向外到达INTERNET。但是由于错误的配置，它会允许位于_blank">防火墙外部的攻击穿过_blank">防火墙。WinGate常会发生这种错误，在加入IRC聊天室时常会看到这种情况。
|1170|[NULL]| 木马Streaming Audio Trojan、Psyber Stream Server、Voice开放此端口。
|1234、1243、6711、6776|[NULL]| 木马SubSeven2.0、Ultors Trojan开放1234、6776端口。木马SubSeven1.0/1.9开放1243、6711、6776端口。
|1245|[NULL]| 木马Vodoo开放此端口。
|1433|SQL| Microsoft的SQL服务开放的端口。
|1492|stone-design-1| 木马FTP99CMP开放此端口。
|1500|RPC client fixed port session queries| RPC客户固定端口会话查询
|1503|NetMeeting T.120| NetMeeting T.120
|1524|ingress| 许多攻击脚本将安装一个后门SHELL于这个端口，尤其是针对SUN系统中Sendmail和RPC服务漏洞的脚本。如果刚安装了_blank">防火墙就看到在这个端口上的连接企图，很可能是上述原因。可以试试Telnet到用户的计算机上的这个端口，看看它是否会给你一个SHELL。连接到600/pcserver也存在这个问题。
|1600|issd| 木马Shivka-Burka开放此端口。
|1720|NetMeeting| NetMeeting H.233 call Setup。
|1731|NetMeeting Audio Call Control| NetMeeting音频调用控制。
|1807|[NULL]| 木马SpySender开放此端口。
|1981|[NULL]| 木马ShockRave开放此端口。
|1999|cisco identification port| 木马BackDoor开放此端口。
|2000|[NULL]| 木马GirlFriend 1.3、Millenium 1.0开放此端口。
|2001|[NULL]| 木马Millenium 1.0、Trojan Cow开放此端口。
|2023|xinuexpansion 4| 木马Pass Ripper开放此端口。
|2049|NFS| NFS程序常运行于这个端口。通常需要访问Portmapper查询这个服务运行于哪个端口。
|2115|[NULL]| 木马Bugs开放此端口。
|2140、3150|[NULL]| 木马Deep Throat 1.0/3.0开放此端口。
|2500|RPC client using a fixed port session replication| 应用固定端口会话复制的RPC客户|

### 常用软件端口

|端口|服务|说明|
|:-:|:-:|:-:|
|3306|mysql|mysq数据库|
|27017|mongodb|mongodb数据库|
|9200|elaticsearch||
|6379|redis||

### 常见软件包格式

#### 一、deb包

1. 如果是ubuntu系统双击软件包，按照引导即可
2. 也可以用命令：sudo dpkg -i 包名.deb
3. 卸载命令：sudo apt-get remove 包名

#### 二、rpm包

1. 如果是在图形界面，双击即可
2. 也可以使用命令：rpm -i 包名.rpm
3. 卸载命令：rpm -e 完整软件名（如：firefox -1.0.1-1.3.2）

ps:如果不知道完整名称使用命令：rpm -qa 部分包名*　进行模糊查询

#### 三、bin包

1. 打开终端，进入包所在的目录，先给包加上可执行的权限：chmod +x 包名.bin。再执行：./包名.bin。
2. 卸载：把安装时的安装目录删除即可

#### 四、run包

1. 同bin包，先加上可执行权限：chmod +x 包名.run。再执行：./包名.run。
2. 卸载：到安装目录下，有uninstall文件，执行这个文件即可： ./uninstall。

#### 五、tar.gz(bz或bz2等)包

１，打开终端，进入源代码压缩包所在目录
２，根据类型解压文件：tar -zxvf 包名.tar.gz
３，执行解压缩命令后，通常在解压缩后产生的文件中，有“Install”的文件。该文件为纯文本文件，详细讲述了该软件包的安装方法。
４，执行解压缩后产生的一个名为configure的可执行脚本程序。它是用于检查系统是否有编译时所需的库，以及库的版本是否满足编译的需要等安装所需要的系统信息。为随后的编译工作做准备。命令为：#./configure。
５，检查通过后，将生成用于编译的Makefile文件。此时，可以开始进行编译了。编译的过程视软件的规模和计算机性能的不同，所耗费的时间也不同。命令为：#make。
６，成功编译后，键入如下的命令开始安装：#make install

        安装完毕，应清除编译过程中产生的临时文件和配置过程中产生的文件。键入如下命令：

        #make clean
        #make distclean

ｐｓ：如果你的包是二进制包，解压后可以直接使用，３、４、５、６步可以省略。
