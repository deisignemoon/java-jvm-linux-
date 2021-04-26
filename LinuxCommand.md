### Linux常用指令
1. 一般指令
 - cd <文件地址> 切换目录
 - cd ..:返回上一级目录
 - cd ~：返回家目录
 - pwd：当前目录绝对路径
 - mkdir：创建目录，-p多级创建，-m <三个数字>加上权限
 - rmdir：删除空目录，-r删除目录下所有内容，-p连同上层空目录一起删除
 - ls：查看当前目录，-a显示所有档案，包含隐藏的，-l显示长信息，--full-time显示完整的时间，--color=alway显示颜色，-连同子目录内容一起显示，相当于显示目录下所有内容，-t按时间排列显示，-S按档案容量大小显示
 - rm：删除文件 -f 无视确定消息强制删除 -r 多级删除，-i 表示互动模式，删除之前会询问是否动作
 - touch：修改档案时间或建制新档。-a仅修订档案内容读取时间，-c仅修改档案的时间，若档案不存在不建立新档，-d后面可以接欲修订的日期，也可使用--date=a"日期或时间"，-m仅修改档案内容改变时的时间，-t后面可以接欲修订的日期，格式为[YYMMDDhhmm]
 -  mv <原文件> <新文件>：移动文件并重命名，-f如果目标档案已存在，不询问，强制覆盖，-i如果目标档案已存在，就会询问是否覆盖，-u如果目标档案已存在且source比较新才会更新
 -  cp <原文件> <新文件>：复制文件并重命名，-r递归复制，-p连同档案的属性一起复制，-i表示若目标文件存在时，在覆盖时会先询问动作的进行
 -  echo：输出语句
 -  tail：输出文件最末尾10行信息，-f持续监控是否有新信息写入末尾，-n看末尾几行
 -  head：查看文件头部10行信息，-n设置信息行数
 -  cat：只读查看文件信息。-n显示行号
 -  more：全屏方式分页显示文件信息，一次全部加载
 -  less：同上，但根据显示加载内容
 -  grep <字段>：分析一段讯息，若存在则撷取，-c查询到的次数，-i忽略大小写，-n输行号，-v反向选择
 -  \>:输出到文件，并覆盖原内容
 -  \>\>:输出到文件，追加到尾部  
 -  od：以二进制的方式读取文件内容，-t  【type】输出类型type可为a(默认)、c(ACSll码)、d(十进制)、f(浮点)、o(八进制)、x(十六进制)
 -  xxd:二进制查看文件（可以看到原文件内容）
 - ps -ef | grep <进程名>：查看服务进程
 - date：显示当前时间
 - cal <月> <年>：显示当前日历
2. vim 文件操作
 - ESC：使用一般模式
 - i或者a：进入编辑模式
 - ：或者/：进入命令模式
 - yy或5yy：拷贝当前行或起始当前行的向下5行，用p粘贴
 - dd或5dd：删除当前行或起始当前行的向下5行
 - ：set nu或：set nonu：显示文件行号或取消显示
 - G：到达文件最末行（一般模式下）
 - gg：到达文件首行（一般模式下）
 - 撤销操作：切换到一般模式下 u
 - 移动到某行：shift+g（命令模式下）
 - 移动到行头或行尾，使用键盘的HOME或END，或者在命令模式下^或$
 - 清空文件内容：将空数据覆盖到文件，如: >  xxx.txt或echo "" >xxx.txt 或 : > xxx.txt 或 cat /dev/null > xxx.txt 
3. 开关机操作
 - shoutdown -h now:立即关机
 - shutdown -h 1：一分钟后关机
 - shutdown -r now：立即重启
 - init <0-6>：根据启动级别不同，进入不同模式，关机或重启
 - halt:立即关机
 - poweroff：立即关机
 - reboot：立即重启
 - sync：将内存同步到磁盘，关机或重启前都应该同步一下，防止数据丢失
4. 用户登录和注销
 - 尽量不要以root登陆，可以以一般用户登录，在su - <用户名>切换用户身份
 - logout：注销用户
5. 用户操作
 - useradd <选项> <用户名>：创建用户后会自动创建对应用户名的家目录
 - useradd -d <用户名>：指定家目录
 - passwd <用户名>：修改或设置该用户密码
 - userdel <-r> <用户名>：删除该用户，使用-r会将对应家目录也删除，不建议这么做
 - id <用户名>：查询用户信息
 - groupadd <用户组名>：添加一个用户组
 - groupdel <用户组名>：删除一个用户组
 - useradd -g <用户组> <用户名>：添加一个用户，并制定其用户组
 - usermod -g <用户组> <用户名>：修改用户的用户组
 - usermod -d <目录名> <用户名>：修改用户登录初始目录
 - /etc/passwd：用户配置信息
 - /etc/shadow：用户密码配置信息
 - /etc/group：用户组配置信息
6. 运行级别
 - 0:关机
 - 1:单用户模式（可以用于找回密码）
 - 2: 多用户模式（无网络）
 - 3:多用户模式（一般远程操作模式）
 - 4: 未使用保留
 - 5:图形界面
 - 6:重启
 - systemctl get-default：获取当前的运行级别；
 - systemctl set-default multi-user.target：将默认运行级别设置为mulit-user；
 - systemctl isolate multi-user.target：不重启系统的情况下，将运行级别切换至mulit-user；
 - systemctl isolate graphical.target：不重启系统的情况下，将运行级别切换至图形模式。
 - runlevel：返回结果中，第一个数为之前运行级别，后一个数为当前运行级别；
 - init <0-6>：根据启动级别不同，进入不同模式
7. 帮助
 - man <指令>
 - help <指令>
8. 搜索查找
 - find <范围> <选项>：指定目录下查找文件或目录。-name按文件名查找，-user按用户查找，-size按文件大小查找，支持模糊查找
 - local：定位文件路径 local <文件名>，第一次运行前使用updatedb创建local数据库，默认一天更新一次，需要手动更新数据库
 - whereis：whereis  [-bmsu]  档案或目录名
9. 压缩命令
 - tar：-zxvf <压缩包> <解压目录> 解压，-zcvf <压缩包名> <要压缩的文件(们)> 压缩文件
 - zip/unzip：-r递归 ，-d解压缩后存放目录
10. 文件管理
 - 查看文件所有者：ls -ahl
 - chown <用户名> <文件名>：修改文件所有者，或chown <用户名>:<用户组> <文件名>
 - chgrp <用户组> <文件名>：修改文件所在组，-R该目录下文件都修改
 - chmod <操作> <文件名>：修改文件权限，以+/-/=，为u/g/o/a变更r/w/x权限，或以4/2/1(读/写/运行)修改，如：chmod 751 <文件或目录>
 - lsattr：显示档案隐藏属性。 -a将隐藏文件的属性也秀出来，-d如果连接的是目录，仅显示目录本身的属性，而非目录内的文件名， -R连同子目录的数据也一并列出来
11. 任务调度
 - crontab：-e编辑任务，-l查询任务，-r删除该用户的所有任务
 - 任务设置：* * * * *，分别为分，时，日，月，星期，以确实数字那些时间，/n每隔一段时间，0-5某段时间
 - 任务可以是shell指令，以.sh文件执行，记得加上可执行权限
 - at：延时命令。at <时间> ，写入命令后ctrl+d，设置命令。-l查看所有命令
 - jobs： 查看当前会话后台的任务。 -l 同时显示任务的线程id，类似于ps
 - kill %n：n代表jobs查出的任务id号
 - &： 放在命令后，使该指令在后台执行，断开会话任务结束
 - ctrl+z：暂停当前任务
 - fg %n：将后台任务放到前台执行
 - bg %n：将暂停的任务放到后台运行
 - nohup：写在指令最前，忽略所有挂断（SIGHUP）信号，即断开会话不结束任务，默认输出写到nohup.out
12. 进程管理
 - ps：ps -aux 当前用户所有进程信息参数
 - ps -ef：显示全格式所有进程及其父进程
 - kill <进程id>：杀死进程，-9强制杀死
 - killall <进程名>：杀死所有该名的进程，支持通配符
 - pstree：以树的方式查看进程，-p显示进程id，-u显示进程所属用户
13. 服务管理
 - [service和systemctl](https://www.cnblogs.com/shijingjing07/p/9301590.html)
 - [systemctl](https://blog.csdn.net/liuchonghua/article/details/81743606)
14. 网络管理
 - ifconfig或ip:网络配置与状态，ifconfig 属于 net-tools 软件包，ip 属于 iproute2 软件包
 - 虽然这两个命令输出的格式不尽相同，但是输出的内容基本相同，比如都包含了 IP 地址、子网掩码、MAC 地址、网关地址、MTU 大小、网口的状态以及网路包收发的统计信息，下面就来说说这些信息，它们都与网络性能有一定的关系。

 - 第一，网口的连接状态标志。其实也就是表示对应的网口是否连接到交换机或路由器等设备，如果 ifconfig 输出中看到有 RUNNING，或者 ip 输出中有 LOWER_UP，则说明物理网路是连通的，如果看不到，则表示网口没有接网线。

 - 第二，MTU 大小。默认值是 1500 字节，其作用主要是限制网络包的大小，如果 IP 层有一个数据报要传，而且数据帧的长度比链路层的 MTU 还大，那么 IP 层就需要进行分片，即把数据报分成干片，这样每一片就都小于 MTU。事实上，每个网络的链路层 MTU 可能会不一样，所以你可能需要调大或者调小 MTU 的数值。

 - 第三，网口的 IP 地址、子网掩码、MAC 地址、网关地址。这些信息必须要配置正确，网络功能才能正常工作。

 - 第四，网路包收发的统计信息。通常有网络收发的字节数、包数、错误数以及丢包情况的信息，如果 TX（发送） 和 RX（接收） 部分中 errors、dropped、overruns、carrier 以及 collisions 等指标不为 0 时，则说明网络发送或者接收出问题了，这些出错统计信息的指标意义如下：

 - errors 表示发生错误的数据包数，比如校验错误、帧同步错误等；
 - dropped 表示丢弃的数据包数，即数据包已经收到了 Ring Buffer（这个缓冲区是在内核内存中，更具体一点是在网卡驱动程序里），但因为系统内存不足等原因而发生的丢包；
 - overruns 表示超限数据包数，即网络接收/发送速度过快，导致 Ring Buffer 中的数据包来不及处理，而导致的丢包，因为过多的数据包挤压在 Ring Buffer，这样 Ring Buffer 很容易就溢出了；
 - carrier 表示发生 carrirer 错误的数据包数，比如双工模式不匹配、物理电缆出现问题等；
 - collisions 表示冲突、碰撞数据包数；
 - ifconfig 和 ip 命令只显示的是网口的配置以及收发数据包的统计信息，而看不到协议栈里的信息，那接下来就来看看如何查看协议栈里的信息。
15. rpm与yum
 - rpm：rpm安装操作
 - rpm -q <应用>：查看某应用是否安装
 - rpm -qi <软件包名>：查看软件包信息
 - rpm -ql <软件包名>：查看软件包中文件
 - rpm -qf <文件全路径>：查看文件所属软件包
 - rpm -e <软件名>：卸载软件，--nodeps强制卸载，不推荐
 - rpm -ivh <rpm包全路径>：安装rpm包
 - yum：shell前端软件包管理器，可以自动处理依赖
 - yum list|grep <软件名>：查询yum服务器是否有该软件
 - yum install <软件名>：下载安装
16. 网络命令
 - curl：访问指令。
 - curl -O <url>：下载该文件
 - curl -T <文件路径> -u <用户名>:<密码> ftp://<FTP地址>/<ftp路径>/ 上传文件
 - curl <url>：访问该地址，获得html
 - curl -o <文件名> <url> ：将html保存
 - nc：nc -zvw3 ip port 查看tcp端口是否开启。 nc -l port ,监听某端口。 nc ip port 连接某ip的端口
 - netstat -anpl|grep port 查看端口占用
 - telnet
17. linux状态查询
 - top：整机进程信息
 - netstat:套接字连接情况 -a 列出所有，-t TCP的连接，-u UDP的链接，-n 禁用域名解析，加快查询，-l，正在监听的套接字, -s 协议栈统计信息 。一般使用 netstat -lantp|grep 端口号，查询对应端口号的套接字
 - ss: netstat的性能不太好，可以使用ss，获得简略信息
 - vmstat：查看CPU(包含不限于)。vmstat -n 2 3 每2秒一次，一共3次 
 - mpstat -P ALL 2：查看所有CPU核信息
 - pidstat -u 1 -p 进程编号：每个进程使用cpu的用量分解信息
 - free：应用程序可用内存数 -m使用mb计数
 - pidstat -p 进程号 -r 采样间隔秒数：查看额外
 - df -h：查看磁盘剩余空闲数
 - du -ash <目录> :查看目标目录下文件大小
 - iostat -xdk 2 3：磁盘IO性能评估，每2秒一次，一共3次，可以下载iotop
 - pidstat -d 采样间隔秒数 -p 进程号：查看额外
 - ifstat 1：查看网络IO，1秒一次，可以下载iftop
 - sar: -h 帮助；-d 磁盘；-b io;-r 内存；-u CPU；-n DEV 网卡（rxpck/s 和 txpck/s 分别是接收和发送的 PPS，单位为包 / 秒。rxkB/s 和 txkB/s 分别是接收和发送的吞吐率，单位是 KB/ 秒。rxcmp/s 和 txcmp/s 分别是接收和发送的压缩数据包数，单位是包 / 秒。）；查看机器状态
 - ethtool：ethtool eth0 | grep Speed 不过注意这里小写字母 b ，表示比特而不是字节。我们通常提到的千兆网卡、万兆网卡等，单位也都是比特（bit）
 - ping ：它是基于 ICMP 协议的，工作在网络层。 icmp_seq（ICMP 序列号）、TTL（生存时间，或者跳数）以及 time （往返延时），而且最后会汇总本次测试的情况，如果网络没有丢包，packet loss 的百分比就是 0。ping 不通服务器并不代表 HTTP 请求也不通，因为有的服务器的防火墙是会禁用 ICMP 协议的。
18. 服务操作指令
 - service <服务名> <操作>：操作系统服务，在centos6以下可用，如：service iptables status 查看防火墙状态
 - systemctl <操作> <服务名>:操作系统服务，在centos7及以上可用，如：systemctl status firewalld.service
 - 操作：status(服务状态)、start(启动服务)、stop(停止服务)、restart(重启服务)、enable(设置开机启动，centos7)、disable(设置开机禁用,centos7)、reload(重新加载更新状态)
 - chkconfig iptables off:设置防火墙开机禁用，centos6
19. 虚拟机创建
 - Xshell链接其它主机上的虚拟机，可以在虚拟机上配置主机与虚拟机的端口映射，并打开主机对应端口。Xshell则连接主机上的对应端口，即可连接到对应虚拟机。
 - 虚拟机配置网络，需要修改 /etc/sysconfig/network-stripts/ifcfg-nes233
 - BOOTPROTO="static",ONBOOT="yes",IPADDR=192.168.x.x,GATEWAY=192.168.x.x,NETMASK=255.255.255.0,DNS=192.168.x.x
 - 对应的GATEWAY在虚拟机NAT配置中存在，DNS由局域网对应网关，IPADDR则是在GATEWAY同一网段下
20. JDK的安装
 - 首先删除默认的openJDK
 - 其次下载对应JDK安装包
 - 然后解压到/usr/local/lib对应文件夹下 
 - 最后修改/etc/profile文件，配置PATH，保存后source /etc/profile
 - 使用java -version检查是否安装完成
21. 调试工具
 - strace:跟踪一个命令的系统调用。strace -ff -o xxx.out <对应指令>，还可以-t输出对应时间戳。
 - tcpdump:一个命令行下的抓包工具。-i 抓哪个网卡，-c 抓几个包，-X 将包中内容与协议头原原本本地显示 ，-nn 将域名显示为ip和端口号 ，-e 打印链路层的头信息，源mac与目的mac，-v或-vv输出更详尽的报文信息。 sudo tcpdump -i eth0 -e -nn -X -c 2 port 1111
22. 使用tmux
 - tmux有会话（Session）、窗口（Window）、窗格（Pane）
 - tmux ls：查看当前存在的会话
 - 组合键 Ctrl-b (Tmux 快捷键前缀)
 - 启动：tmux
 - 创建一个新会话：tmux new -s <name-of-my-session>
 - 进入一个存在的会话：tmux attach -t n
 - 查看所有会话：快捷键+s
 - 查看当前会话的所有窗口：快捷键+w
 - 创建一个新窗口：快捷键+c
 - 创建一个新窗格：快捷键+%
 - 窗格间移动：快捷键+方向键
 - exit：离开当前窗格，窗口，会话
23. 端口配置
 - /etc/sysconfig/iptables 编辑文件
 - 重启服务：/etc/init.d/iptables restart
 - 查看端口是否开放：/sbin/iptables -L -n
