# Linux-Docker Examples
### 2019.11.16 - 1.Virtual Machine
下载最新版VirtualBox
创建一个1GB内存+动态15GB磁盘，名为CentOS的虚拟机。注意，放在合适的位置
https://opsx.alibaba.com/mirror
下载CentOS7.7.1908，DVD iso版，4.66GB(4.34GB)
在虚拟机的光驱，引入下载的CentOS镜像
鉴于需登录的校园网络特点，网络模式使用默认的NAT模式
桥接，默认的网络地址转换(NAT)的区别？
从虚拟机切出鼠标/键盘的控制的快捷键？

### 2019.11.16 - 2.CentOS
运行虚拟机，进入centos安装模式
打开网络功能，默认的自动分配IP
安装位置，无需分区
安装minimal版，后续软件包可以再添加
安装过程中，设置root账号密码，创建一个普通操作权限的用户/密码
安装时，查找资料了解root/普通用户，Linux系统操作权限管理
安装完毕，光驱卸载iso，重启

初学者可以直接以root账号登录
查看网络是否正常，ping通百度
停止操作快捷键？自动补全快捷键？

### 2019.11.16 - 3.SSH
win10可安装win10自带的OpenSSH客户端。什么是SSH？
Win7安装Bitvise SSH Client或其他SSH客户端
在VB网络设置中，创建一个宿主机到虚拟机的ssh端口映射
通过控制台，以root登入虚拟机，注意需显式声明端口参数
为什么通过ssh连接服务器，而不直接在虚拟机中操作？

如果能够正确进入服务器，则可以在VB中为虚拟机创建一个系统快照作为基础镜像，
后续操作出问题，可以回滚到当前版本。当然，直接删了虚拟机重来也很方便

### 2019.11.16 - 4.Don’t Be Scared of the Terminal
基本命令
清屏，快速删除命令，列出，进入/退出目录，根目录，home目录，
创建/删除/重命名目录，查看系统版本，系统内核，cpu/内存占用，磁盘占用。要使用自动补全
在/home/用户下，练习创建/删除/重命名目录

### 2019.11.23 - 5.vi
vi，Linux经典编辑器
在/home/用户下，基于vi创建文件test，编写C语言主函数打印输出hello world
```
$ vi test

#include <stdio.h>
#include <stdlib.h>

int main()
{
    printf("Hello world of docker!\n");
    return 0;
}

`esc` + `:w` +`:q`

```
`ctrl+z+z` 不保存退出
`shift+z+z` 保存退出
掌握最基本的操作指令，编辑模式/删除整行/保存退出/不保存退出
```
先按Esc键,再按以下
:wq或:x                      保存并退出(会保存修改的文件内容)
:q                           退出，适用于未修改的文件
:q!                          强制退出，适用于修改文件后不保存退出(加感叹号表示强制,不会保存修改的文件内容)
```
在/home/用户下，创建名为code的目录，将文件重命名为hello.c；移动到code目录。即，学习掌握基本的重命名/移动命令
```
$ mkdir code //创建名为code目录
$ cd .. //退回home目录
$ mv test hello.c //将文件重命名为hello.c

```
Linux mv 命令用来为文件或目录改名、或将文件或目录移入其它位置。
```
mv [options] source dest
mv [options] source... directory
```

|命令格式|运行结果|
|--|--|
|mv 文件名 文件名|将源文件名改为目标文件名|
|mv 文件名 目录名|将文件移动到目标目录|
|mv 目录名 目录名|目标目录已存在，将源目录移动到目标目录；目标目录不存在则改名|
|mv 目录名 文件名|	出错|
### 2019.11.23 - 6.yum
 了解linux的软件管理方式
 yum？repo？rpm？为什么使用yum？基于yum下载的是程序源码还是编译完的二进制文件？
>0. Yum(全称为 Yellow dogUpdater, Modified)是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。
>1. RPM 全称为：Red-Hat Package Manager，即红帽 Linux 发行版的软件包管理器。
>2. linux下，repo文件都是存放在/etc/yum.repos.d文件夹之中的。repo文件即是我们常说的源文件(repositry匹配文件)，在使用yum命令的时候系统会自动读取repo文件，然后去repositry获取软件。
>3. 比起使用rpm命令安装软件，yum方式安装会自动下载依赖文件，更加的方便
>4. 基于yum下载的是编译完的二进制文件

为什么有时需要下载源码在本地编译，而不是直接下载编译好的二进制文件？
>从源代码制作软件的过程，称之为是软件编译。从源代码构建成软件的编译有两种方式：
>- 本机编译 （Natively Compiled），对应编译型语言。(C 语言是本机编译)
>- 解释编译（Interpreted Compiled），对应解释性语言。(如 Python，就需要一个编译步骤，把源代码构建成 Python 的语言解释器（称为 CPython）的可以执行文件)
>实际上，我们在构建二进制 RPM 包时，有两种构建方法：
> - 从源码构建 SRPM，然后再构建二进制 RPM
> - 直接从源码构建二进制 RPM。
>然而，在软件开发中，我们通常会采用第一种方法，因为它有**以下优势**：
>1. 便于保留的 RPM 版本的确切来源（以 Name-Version-Release 格式标注）。这对于 debug 非常有用。
>2. 需要在不同的处理器硬件平台上使用 SRPM 构建二进制 RPM。

学习yum基本命令：列出所有已安装，基于通配符查询已安装，所有可更新，更新全部可更新，基于通配符列出远程仓库匹配的软件包，安装所需软件包
无需添加国内仓库镜像网址，centos自动在延迟最小的仓库下载(我这是上海交大/163镜像)。还是要理解yum repo

- 列出所有已安装的软件包 ：`yum list installed`
- 基于通配符查询已安装`yum list installed ^bash     #这个根据自己会的正则表达式进行筛选`
`yum list|grep gcc`
```
“| ”管道符用法

上一条命令的输出，作为下一条命令参数

方式：command1 | command2
```
- 列出资源库中与正则表达式匹配的所有可以更新的rpm包`yum list updates #正则表达式匹配`
- 查看信息`yum info installed gcc`

```
1 安装
yum install 全部安装
yum install package1 安装指定的安装包package1
yum groupinsall group1 安装程序组group1
```
```
2 更新和升级
yum update 全部更新
yum update package1 更新指定程序包package1
yum check-update 检查可更新的程序
yum upgrade package1 升级指定程序包package1
yum groupupdate group1 升级程序组group1
```
```
3 查找和显示
yum info package1 显示安装包信息package1
yum list 显示所有已经安装和可以安装的程序包
yum list package1 显示指定程序包安装情况package1
yum groupinfo group1 显示程序组group1信息yum search string 根据关键字string查找安装包
```
```
4 删除程序
yum remove &#124; erase package1 删除程序包package1
yum groupremove group1 删除程序组group1
yum deplist package1 查看程序package1依赖情况
```
```
5 清除缓存
yum clean packages 清除缓存目录下的软件包
yum clean headers 清除缓存目录下的 headers
yum clean oldheaders 清除缓存目录下旧的 headers
yum clean, yum clean all (= yum clean packages; yum clean oldheaders) 清除缓存目录下的软件包及旧的header
```
基于yum安装gcc，查看是否已安装
`yum install gcc`
`yum info installed gcc`

基于gcc将code目录下的hello.c，编译生成可运行的名为hello的文件，运行查看输出结果
```
$ gcc -o hello hello.c
$ ./hello
```
也可安装openjdk11，编写Java版hello world。java11起可直接通过java命令运行，自动先编译
gcc安装到哪了？列出安装gcc的位置，各位置的作用，为什么可以在任意位置直接运行gcc命令？
`# rpm -ql gcc`
`whereis gcc`
`-query 中的 -l  list all license files`
>简单说PATH就是一组路径的字符串变量，当你输入的命令不带任何路径时，LINUX会在PATH记录的路径中查找该命令。有的话则执行，不存在则提示命令找不到，也就是我们经常看到的-bash:` * * * : command not found`。比如在根目录/下可以输入命令`ls`,在/usr目录下也可以输入`ls`,但其实`ls`命令根本不在这个两个目录下，当你输入ls命令时LINUX会去/bin,/usr/bin,/sbin等目录寻找该命令。而PATH就是定义/bin:/sbin:/usr/bin等这些路劲的变量，其中冒号为目录间的分割符。使用export $PATH命令可以查看环境变量的内容。

基于yum history卸载(回滚)gcc及全部依赖
yum remove卸载时却只卸载这个文件包本身,如果需要删除安装时附加的依赖包可以使用yum history的相关操作实现回滚
```
[root@localhost bin]# yum history list gcc
已加载插件：fastestmirror
ID     | 命令行                   | 日期和时间       | 操作           | 变更数
-------------------------------------------------------------------------------
     2 | install gcc              | 2019-11-24 14:20 | I, U           |   11 EE
[root@localhost bin]# yum histroy undo 2
```
直接删除非空的test目录。命令参数？
`rm -rf code/`


### 2019.11.23 - 7.Directory Structure
了解根目录下的，主要目录的功能
bin/; dev/; mnt/; etc/; opt/; usr/; lib/; home/; /usr/bin/; /usr/lib/; /usr/libexec/;
![linux目录结构](https://www.runoob.com/wp-content/uploads/2014/06/003vPl7Rty6E8kZRlAEdc690.jpg)
`bin/`:bin是Binary的缩写, 这个目录存放着最经常使用的命令.
`dev/`:dev是Device(设备)的缩写, 该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。
`mnt/`:系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。
`etc/`:这个目录用来存放所有的系统管理所需要的配置文件和子目录。
`opt/`: 这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。
`usr/`: 这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。
`lib/`:这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。
`/usr/bin`：系统用户使用的应用程序。
`/usr/lib`:存放一些函数库、执行文件及连接文件，特别的是，存放在这里面的文件都是不希望直接被用户或shell脚本所使用的文件，在/usr/lib中有非常多的子目录，每一个软件都有其各自所需的函数库；
`/usr/libexec`: 目录下存放一些函数库、执行文件及连接文件
>在 Linux 系统中，有几个目录是比较重要的，平时需要注意不要误删除或者随意更改内部文件。
>/etc： 上边也提到了，这个是系统中的配置文件，如果你更改了该目录下的某个文件可能会导致系统不能启动。
>/bin, /sbin, /usr/bin, /usr/sbin: 这是系统预设的执行文件的放置目录，比如 ls 就是在/bin/ls 目录下的。
>值得提出的是，/bin, /usr/bin 是给系统用户使用的指令（除root外的通用户），而/sbin, /usr/sbin 则是给root使用的指令。
>/var： 这是一个非常重要的目录，系统上跑了很多程序，那么每个程序都会有相应的日志产生，而这些日志就被记录到这个目录下，具体在/var/log 目录下，另外mail的预设放置也是在这里。

### 2019.11.30 - 8.Mount
**插入一个fat32/ntfs格式U盘，exfat默认不支持
设置虚拟机识别读取。基本命令：列出所有指定格式磁盘；挂载设备，浏览设备内文件；取消挂载**
>CentOS默认源里没有NTFS-3G，想要添加ntfs支持，无非是自己下载编译安装或者加源yum安装。重新安装了一个CentOS7，用的是添加aliyun的epel源来yum安装的方式，简单易行。
```
1、加源
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
2、安装
# yum update;yum install ntfs-3g
如果系统提示：没有可用软件包，可以输入
# yum install ntfs*
```
`fdisk -l`

`mount.ntfs-3g  /dev/sdb4 /mnt/ `

```
# umount -v /dev/sda1          通过设备名卸载  
/dev/sda1 umounted  
# umount -v /mnt/mymount/      通过挂载点卸载  
/tmp/diskboot.img umounted
```

### 2019.11.26 - 9.bash & chmod
**Shell？bash？cat？了解脚本的：基本结构，支持的语句，执行linux命令，运行即可**
####1.What is shell？
>Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。
>Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。
>>bash是Unix shell的一种，Bash是许多Linux发行版的默认Shell
>>cat 命令用于连接文件并打印到标准输出设备上。（cat是使用方法不仅局限于查看内容，他也可以做到修改内容但是个人平常并不推荐这么用

####2.基本结构
```
#!/bin/bash
echo "Hello World !"
```
<kbd>\#!</kbd> 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。
echo 命令用于向窗口输出文本。
####3.支持语句
<kbd>echo</kbd>
<kbd>printf</kbd>
<kbd>test</kbd>
<kbd>for循环语句<kbd>：
```
for 变量名 in 列表;do
               循环体
       done
```
**shell参数传递：**
<kbd>\$#</kbd> :传递到脚本的参数个数
<kbd>\$\*</kbd> :以一个单字符串显示所有向脚本传递的参数。如<kbd>"\$\*"</kbd>用\「\"\」括起来的情况、以"\$1 \$2 … \$n"的形式输出所有参数。  
<kbd>\$\$</kbd>	:脚本运行的当前进程ID号
<kbd>\$\!</kbd>	:后台运行的最后一个进程的ID号
<kbd>\$\@</kbd>	:与<kbd>\$\*</kbd>相同，但是使用时加引号，并在引号中返回每个参数。如<kbd>\"\$\@\"</kbd>用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。
<kbd>\$\-</kbd>	:显示Shell使用的当前选项，与set命令功能相同。
<kbd>\$\?</kbd>	:显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。

**在/home/用户名/test下，基于vi编写一个由bash执行的，打印出/home/用户名/test/下所有文件的脚本
需要添加脚本文件的执行权限，运行
基于cat读取显式脚本代码**
```
#!/bin/bash
for file in `ls`;do
        echo $file
done
```
使用 <kbd>Ctrl</kbd>+<kbd>Z</kbd>+<kbd>Z</kbd>可以直接保存退出


**带权限的列出文件**
`ls -al ` ` ls -l`
**chmod命令，r/w/x？3组权限？u/g/o？增加/修改/删除指定角色的指定权限。使用语义参数比数字好记
为以上脚本文件，添加创建者具有读写执行权限命令？取消其他用户的读权限？
权限角色，u，所有者；g，组；o，其他人**

### 2019.11.26 - 10.Docker
可以把安装的gcc/openjdk等等都卸载了
https://docs.docker.com/engine/docker-overview/
https://geekflare.com/docker-vs-virtual-machine/
https://yeasy.gitbooks.io/docker_practice/
#### 1.虚拟化技术&docker虚拟化优势
**了解早先服务器基于虚拟化技术的部署，为什么使用虚拟化技术？当前Docker的虚拟化与之前的区别？优点？了解docker images docker containers？**
Docker engine提供了启动Images和containers核心的技术的支持。当你运行docker run hello-world 命令时，实际上可分为三个部分：
![运行docker run hello-world的时间过程](https://images2015.cnblogs.com/blog/918915/201701/918915-20170126134304191-517283657.png)

1. 告诉你操作系统你正在使用的docker程序
2. 一个子命令创建并且运行docker容器
3. 告诉docker将载入到容器中的Image映像  

一个映像是一个文件系统，是在运行时使用的参数，它没有状态和不会改变。容器用来运行映像的实例。当你运行下面命令的时候将会发生下面这些情况：

1. 检查你是否有hello-world软件映像
2. 从Docker Hub中下载映像
3. 将映像载入容器中并运行它。

依赖于这个映像如何创建，一个映像可能运行一个简单、单一的命令然后退出，hello-world映像就是这样的，不过docker还能启动向数据库那样的软件。Docker引擎能够是人们或者公司创建和分享自己的Docker 映像。使用Docker引擎，你不需要担心你的计算机能否运行Docker映像中的软件，Docker容器总是可以运行它。
#### 2.What is vps and Cloud Servers?
**Servers？VPS？Cloud Servers？为什么VPS创建了就开始计时付费？而云可以按流量/CPU内存等的实际使用量弹性付费？**
- vps： 是采用操作系统虚拟化技术，将一台服务器分割为多个虚拟专享服务器
   用户和服务器存在一种绑定的关系
- 云服务器：在服务器集群中采用硬件虚拟化技术。
   随时虚拟化的过程

|Virtual Machine|Docker Container|
|--|--|
|Hardware-level process isolation|OS level process isolation|
|Each VM has a separate OS|Each container can share OS|
|Boots in minutes|Boots in seconds|
|VMs are of few GBs|Containers are lightweight (KBs/MBs)|
|Ready-made VMs are difficult to find|Pre-built docker containers are easily available|
|VMs can move to new host easily|Containers are destroyed and re-created rather than moving|
|Creating VM takes a relatively longer time|Containers can be created in seconds|
|More resource usage|Less resource usage|


https://docs.docker.com/
官网查找适合centos系统的docker-ce社区稳定版的安装方法。Community版？
安装基本工具；添加docker官方仓库，下载docker-ce本身的仓库使用官方地址即可，速度很快。无需指定版本，安装最新版docker-ce
启动docker。开机自动启动docker服务
```
[root@localhost home]# systemctl start docker
[root@localhost home]# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:4df8ca8a7e309c256d60d7971ea14c27672fc0d10c5f303856d7bc48f8cc17ff
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

[root@localhost home]#

```
### 2019.11.26 - 11.Docker Images
- **docker官方镜像仓库国内速度慢，基于vi修改配置文件，**  

`[root@localhost docker]# vi  /etc/docker/daemon.json`
```
{
 "registry-mirrors": ["https://dockerhub.azk8s.cn"]
}
```
使用微软Azure仓库https://dockerhub.azk8s.cn，我这拉取500MB镜像1分钟。基本满速。服务器在国外的不要配。其他仓库要么需要密钥，要么已作废

- **重新加载配置，重启docker**
`# systemctl status docker.restart`
<br>
- **Docker基本命令：拉取镜像；列出本地镜像；删除镜像；**
不建议在本地查询，去官方网站查询更方便
`# docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]` 拉取镜像
`# docker image ls`:列出本地镜像
`# docker image rm [选项] <镜像1> [<镜像2> ...]`:删除本地镜像╰(\*°▽°\*)╯
`#docker ps -a`:查看所有容器记录（包括未运行的容器）
<br>
- **不用拉取hello-world测试，直接拉取最新的openjdk**
如果出现Error response from daemon，说明centos DNS域名解析错误，修改系统DNS解析地址为Google的域名服务器
`# docker pull openjdk`

- **Docker仓库？docker镜像仓库？**
仓库（Repository）是集中存放镜像的地方，分为公共仓库和私有仓库。


### 2019.11.26 - 12.Docker Container
#### Docker run
Docker命令：基于指定镜像创建容器；列出全部已创建的容器；停止运行容器；删除容器。容器ID使用hash值的前2位即可
run基本参数：-p；-v；-d；-i；-t；--rm
<kbd>-p</KBD>：指定要映射的IP和端口，但是在一个指定端口上只可以绑定一个容器
>支持的格式有 `hostPort:containerPort`、`ip:hostPort:containerPort`、 `ip::containerPort`。
>>- **hostPort:containerPort（映射所有接口地址）**
将本地的 5000 端口映射到容器的 5000 端口，可以执行如下命令：
`$ sudo docker run -d -p 5000:5000 training/webapp python app.py`
此时默认会绑定本地所有接口上的所有地址。
>>- **ip:hostPort:containerPort （映射指定地址的指定端口）**
指定映射使用一个特定地址，比如 localhost 地址 127.0.0.1
`$ sudo docker run -d -p 127.0.0.1:5000:5000 training/webapp python app.py`
>>- **ip::containerPort （映射指定地址的任意端口）**
绑定 localhost 的任意端口到容器的 5000 端口，本地主机会自动分配一个端口。
`sudo docker run -d -p 127.0.0.1::5000 training/webapp python app.py`
还可以使用 udp 标记来指定 udp 端口
`$ sudo docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py`

<kbd>-P</KBD>：Docker 会随机映射一个 49000~49900 的端口到内部容器开放的网络端口
<kbd>-v</KBD>：挂载宿主机的一个目录
<kbd>-d</KBD>：让 Docker 在后台运行而不是直接把执行命令的结果输出在当前宿主机下
>使用 -d 参数启动后会返回一个唯一的 id，也可以通过 `docker container ls` 命令来查看容器信息。
>要获取容器的输出信息，可以通过`docker container logs ` 命令

<kbd>-i</kbd>:交互式操作，让容器的标准输入保持打开
<kbd>-t</KBD>：让Docker分配一个伪终端并绑定到容器的标准输入上
<kbd>--rm</KBD>：	退出时自动删除容器

创建容器时，追加在容器启动后，容器内执行操作指令
在/home/用户名/test下，创建HelloWorld.java
`# vi HelloWorld.java`

基于openjdk创建一个容器：挂载home/用户名/test/目录到容器内的/home/code/目录，
即可以在容器中访问挂载目录中的文件；测试用，创建运行完就删除容器；
在前台运行，即显示容器中的输出，后台运行看不到输出；添加容器内java直接运行挂载目录下的HelloWorld的命令

`# docker run -it -v /home/Rice/test:/home/code --rm openjdk  sh -c "cd /home/code &&java HelloWorld.java"`
当容器中没有运行的进程时，容器将关闭。tomcat/MySQL/Nginx等带服务进程的容器会一直运行，
而普通openjdk的容器运行即关闭，除非运行像带web容器的springboot
如何创建一个不关闭的openjdk容器？
创建一个openjdk容器：依然挂载以上目录；启动标准输入，
启动终端控制台；在后台运行；在容器内运行/bin/bash。即，创建一个一直运行的进程，使容器不会关闭；
`# docker run -it -v /home/Rice/test:/home/code --rm openjdk /bin/bash`
查看容器是否为运行状态
`#docker ps -a`
#### Docker exec
exec基本参数：-i；-t。结合/bin/bash使用
以可互交的带终端的模式，进入之上创建的后台运行的，未停止的openjdk容器
在容器内进入挂载目录，运行HelloWorld，查看输出
查看容器内系统版本？查看镜像/容器信息？查看镜像/容器占用？
`cat /etc/issue`
`docker inspect  [id/name] ` 容器id/镜像id查看容器镜像的详细信息。
`docker images [id/name]`：查看镜像信息
`ps -ef | grep 8dac6ac683f5`:查看镜像/容器占用  

### 2019.11.26 - 13.FirewallD & Services
CentOS集成的firewall工具。ports？firewall zone？使用默认的zone-public无需声明
列出firewall所有打开服务与端口等信息，这一个命令就够所有查询了
防火墙重载；永久开启http服务；永久打开80端口；永久关闭服务；永久关闭端口
firewall规则为动态添加，改变规则后需重载，无需重启

查看一个服务的状态。一个服务的启动/停止/启动/禁用。基于firewalld操作

### 2019.11.26 - 14.Docker Web Container
在宿主机，通过scp命令将本地文件上传到服务器。注意，虚拟机网络为NAT模式，需显式声明ssh映射的端口，但参数与ssh命令不同
创建目录，/home/用户名/services/。services下按应用创建目录
将/github/resources/docker-examples.war文件下载到本地，再上传到/home/用户名/services/docker-tomcat/。目录需先创建

拉取最新tomcat镜像。默认暴露的端口？部署路径？集成的openjdk版本？查看镜像信息？
基于命令行创建一个容器：映射服务器80端口到容器的8080端口；挂载docker-examples.war所在目录到容器中的部署目录；后台运行
查看容器是否创建/启动成功。容器中的tomcat自动在挂载目录解压war包部署
在虚拟机添加端口，例如8888，映射虚拟机的80端口
在宿主浏览器，本地+端口+部署在tomcat应用的名称，访问应用

https://github.com/firewalld/firewalld/issues/461
创建容器时在服务器映射的端口，即使服务器firewall没有开启服务或端口，外部依然可以直接访问？
停止，并删除此容器。命令写在一行执行
注意，服务器的一个端口只能被一个应用/容器监听，反复创建容器会端口冲突

### 2019.11.26 - 15.Dockerfile
Orchestration System？为什么需要Docker Compose？优点？k8s(Kubernetes)？k8s与官方docker compose的适用场景？编写docker-compose文件的最大最大特点？
https://docs.docker.com/compose/
按官网教程安装最新版，添加执行权限
基于vi在/home/用户名/services/docker-tomcat/下，编写一个docker-compose文件，基于第3版，服务名称自定义。
将14Docker Web Container，基于命令行创建容器的命令，转为在文件中描述，包括tomcat基础镜像，挂载目录，映射端口
基于文件创建在后台运行的容器；停止/停止删除基于文件创建的容器
查看容器日志，错误时可查看
注意，严格的缩进与空格
