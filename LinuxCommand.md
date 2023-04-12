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
 - dd:if=文件名：输入文件名，默认为标准输入。即指定源文件。
	of=文件名：输出文件名，默认为标准输出。即指定目的文件。
	ibs=bytes：一次读入bytes个字节，即指定一个块大小为bytes个字节。
	obs=bytes：一次输出bytes个字节，即指定一个块大小为bytes个字节。
	bs=bytes：同时设置读入/输出的块大小为bytes个字节。
	cbs=bytes：一次转换bytes个字节，即指定转换缓冲区大小。
	skip=blocks：从输入文件开头跳过blocks个块后再开始复制。
	seek=blocks：从输出文件开头跳过blocks个块后再开始复制。
	count=blocks：仅拷贝blocks个块，块大小等于ibs指定的字节数。
	conv=<关键字>，关键字可以有以下11种：
		conversion：用指定的参数转换文件。
		ascii：转换ebcdic为ascii
		ebcdic：转换ascii为ebcdic
		ibm：转换ascii为alternate ebcdic
		block：把每一行转换为长度为cbs，不足部分用空格填充
		unblock：使每一行的长度都为cbs，不足部分用空格填充
		lcase：把大写字符转换为小写字符
		ucase：把小写字符转换为大写字符
		swap：交换输入的每对字节
		noerror：出错时不停止
		notrunc：不截短输出文件
		sync：将每个输入块填充到ibs个字节，不足部分用空（NUL）字符补齐。
	--help：显示帮助信息
	--version：显示版本信息
 - ps -ef | grep <进程名>：查看服务进程
 - date：显示当前时间
 - cal <月> <年>：显示当前日历
2. vim 文件操作
 - ESC：使用一般模式， h，j，k，l，上下左右移动
 - 进入编辑模式：i插入当前，a插入下一位，o下方插入新一行，I插入行首，A插入行尾，O上方插入新一行
 - ：或者/：进入命令模式。 
 - yy或与y5y：拷贝当前行或起始当前行的向下5行，用p粘贴
 - dd或d5d：删除当前行或起始当前行的向下5行
 - dw：删除光标后1个单词，dnw，删除n个单词
 - pw：同上粘贴
 - r:替换光标处字符，R：持续替换，直至返回一般模式
 - ：set nu或：set nonu：显示文件行号或取消显示
 - G：到达文件最末行（一般模式下）
 - gg：到达文件首行（一般模式下）
 - 撤销操作：切换到一般模式下 u。ctrl+r,恢复撤销
 - 移动到某行：shift+g（命令模式下）,或者:xxx（移动到xxx行）,xxx向下移动xxx行
 - 移动到行头或行尾，使用键盘的HOME或END，或者在一般模式下^(0)或$
 - 清空文件内容：将空数据覆盖到文件，如: >  xxx.txt或echo "" >xxx.txt 或 : > xxx.txt 或 cat /dev/null > xxx.txt 
 - 批量替换：命令模式下，%s/目标位单词/替换后单词/g,或者%s#目标位单词#替换后单词#g
 - :noh 关闭查找关键词高亮
 - /word：向光标之后寻找第一个值为word的字符串
 - ?word：向光标之前寻找第一个值为word的字符串
 - n：重复上一个查找操作
 - N：反向重复前一个查找操作
 - :n1,n2s/word1/word2/g：n1与n2为数字，在第n1行与n2行之间寻找word1这个字符串，并将该字符串替换为word2
 - :1,$s/word1/word2/g：将全文的word1替换为word2
 - :1,$s/word1/word2/gc：将全文的word1替换为word2，且在替换前要求用户确认。
 - gg=G：将全文代码格式化
 - 可视化模式：v(单行)或者V(多行)或者Ctrl+v(块)。使用上下左右选择。小写指令操作选中字符，大写操作选中字符所在行
 - 多文件操作： :n下一个文件 :N上一个文件 :n fileName操作那个文件 :ls列出所有文件信息 :bn切换到buffer为n的文件 
 - vim -o f1 f2 f3 :水平分隔打开文件 -O垂直分隔 -on 预留窗口分割
 - :e file:打开新文件  ：sp file 水平分割打开新文件 ：vs file 垂直分割打开新文件
 - :shell :打开shell，vim后台运行，exit返回vim
 - :!command :执行command
 - :r !command:执行command，并将结果插入光标下一行
 - :new fileName:横向新建窗格 :vsp fileName 水平新建窗格
 - 关闭文件: 命令模式下 q关闭光标所在文件，only关闭除光标所在文件 qa关闭所有文件
 - 窗口操作：Ctrl+w 进入窗格操作 hjkl(上下左右)，文件窗口中移动 +-<> 当前窗格大小改变一行 =所有窗格等宽高 |当前窗格宽度最大 _当前窗格高度最大
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
 - logout：注销用户，exit
 - systemd-run:在临时 scope 或 service 单元中运行命令, 可以在ssh连接退出后保证对应用户创建的进程不被关闭：systemd-run --scope --user tmux [systemd-run 中文手册](http://www.jinbuguo.com/systemd/systemd-run.html)
 - logind.conf:/etc/systemd/logind.conf 登录管理器 [systemd-logind.service 中文手册](http://www.jinbuguo.com/systemd/systemd-logind.service.html)
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
 - w: 有哪些用户连接服务器
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
 - find <范围> <选项>：指定目录下查找文件或目录。-name按文件名查找，-user按用户查找，-size按文件大小查找，支持模糊查找。find / -xdev -size +100M -exec ls -l {} \;可以查询大于100M的大文件，然后可以从返回值里面找到大文件所在目录
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
 - [systemd](https://wiki.archlinux.org/title/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
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
15. 包管理
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
 - pacman 由于pacman数据库操作异常被锁定：rm -f /var/lib/pacman/db.lck
 - pacman：-Syu=对整个系统进行更新; -S 包名=安装包，多个包以空格分割；-Sy 包名=同步包数据后再安装； -Sv 包名=显示一些信息后安装；-U 本地包名=安装本地包，其扩展名为 pkg.tar.gz；-U url=安装远程包；-R 包名=删除包，但不删除依赖；-Rs 包名=删除包与不被其它包依赖的包；-Rsc 包名=删除包与其所有依赖的包；-Rd 包名=删除包，不检查其依赖； -Ss 关键字=在仓库中搜索含关键字的包；-Qs 关键字=搜索已安装的包；-Qi 包名=查看有关包的详尽信息；-Ql 包名=列出该包的文件；-Sw 包名=只下载包，不安装；-Sc=清理未安装的包文件，包文件位于 /var/cache/pacman/pkg/；-Scc=清理所有的缓存文件。
 - error:GPGME error:No data   -->  sudo rm -R /var/lib/pacman/sync
16. 网络命令
 - curl：<url>：访问该地址，获得html,-O <url>：下载该文件,-o <文件名> <url> ：将html保存,-T <文件路径> -u <用户名>:<密码> ftp://<FTP地址>/<ftp路径>/ 上传文件,-X 指定POST或GET，-b '' 指定请求报文体，-H 指定请求报文header，-v 打印请求和返回的请求
 - nc：nc -zvw3 ip port 查看tcp端口是否开启。 nc -l port ,监听某端口。 nc ip port 连接某ip的端口
 - netstat -anpl|grep port 查看端口占用
 - telnet
 - arp:查看服务器地址解析 -a:查看全部 -d：删除缓存 -s：手动输入一个缓存
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
 - blkid：查看块设备的文件系统类型，LABEL，UUID等信息
 - lspci：列出所以链接PCI接口的外部设备。即显卡、网卡、声卡等等。
 - dmesg：显示内核环形缓冲区（kernel-ring-buffer）里面的内容。在进行系统引导时，内核会将有关硬件以及驱动谢谢写入这个缓冲区。usb，bluetooth等驱动信息，可以使用grep过滤查询
 - 查看CPU个数:cat /proc/cpuinfo | grep “physical id” | uniq | wc -l
 - 查看CPU核数:cat /proc/cpuinfo | grep “cpu cores” | uniq
 - 查看CPU型号:cat /proc/cpuinfo | grep ‘model name’ |uniq
 - /proc:设备信息目录
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
 - 最后修改/etc/profile文件，配置JAVA_HOME、PATH、CLASSPATH，保存后source /etc/profile
 - 使用java -version检查是否安装完成
21. 调试工具
 - strace:跟踪一个命令的系统调用。strace -ff -o xxx.out <对应指令>，还可以-t输出对应时间戳。
 - tcpdump:一个命令行下的抓包工具。-i 抓哪个网卡，-c 抓几个包，-X 将包中内容与协议头原原本本地显示 ，-nn 将域名显示为ip和端口号 ，-e 打印链路层的头信息，源mac与目的mac，-v或-vv输出更详尽的报文信息。 sudo tcpdump -i eth0 -e -nn -X -c 2 port 1111
 - tcpdump -i eth0 dst/src host hostname and/or dst/src port ! portNum 监听eth0的目标/源头为hostname的，且/或端口不为portNum的信息 
 - [tcpdump使用详解](https://www.cnblogs.com/lvdongjie/p/10911564.html)
22. 使用tmux
 - tmux有会话（Session）、窗口（Window）、窗格（Pane）
 - tmux ls：查看当前存在的会话
 - 组合键 Ctrl-b (Tmux 快捷键前缀)
 - 启动：tmux
 - 创建一个新会话：tmux new -s <name-of-my-session>
 - 进入一个存在的会话：tmux attach -t n
 - 查看所有会话：快捷键 s
 - 查看当前会话的所有窗口：快捷键 w
 - 创建一个新窗口：快捷键 c
 - 创建一个新窗格：快捷键 %
 - 关闭一个窗格： 快捷键 x
 - 当前窗格全屏显示，再使用一次会变回原来大小：快捷键 z
 - 按箭头方向调整窗格大小：快捷键 ctrl+方向键
 - 窗格间移动：快捷键 方向键
 - 浮动窗口：tmux popup -w 80% -h 80% 生成一个窗格，ctrl+c关闭
 - exit：离开当前窗格，窗口，会话
23. 端口配置
 - /etc/sysconfig/iptables 编辑文件
 - 重启服务：/etc/init.d/iptables restart
 - 查看端口是否开放：/sbin/iptables -L -n
24. 挂载
 - df：查看已挂载设备信息
 - fdisk:创建和维护分区表的程序。-l=查看所有分区表；fdisk /dev/sdx=操作对应磁盘的分区
 - 挂载信息：mount -l
 - 挂载：mount /dev/sdxY /mnt/xxx
 - 解除挂载：umount /dev/sdxY
 - mount -t ntfs-3g /dev/sdxY 目录 。挂载NTFS分区
 - /etc/fstab :自动挂载配置文件。有如下字段：file system：要挂载的分区或存储设备；dir：挂载位置；type：文件系统类型，ntfs,ext4等；options：挂载时使用的参数，ro/rw/auto/relatime等；dump：何时dump它做备份，0表示忽略，1则进行备份；pass：文件系统的检查顺序，0不检查，1最高优先级如根目录，2其它被检查的设备。
25. 扩大分区容量
 - 1.使用fdisk
 - 2.停下对应分区所有程序。systemctl stop xxx
 - 3.解除对应磁盘挂载。umount -v 设备名/挂载点
 - 4.如果无法解除挂载，关闭该分区的操作程序。fuser -m -v 挂载目录；fuser -m -v -i -k 挂载目录
 - 5.先删除该分区，记下该分区的磁柱号(重要：会使数据发生丢失)。
 - 6.再次创建该分区。（记得对比磁柱start位置需要相同，且end，Blocks大于之前的分区）
 - 7.保存推出fdisk
 - 8.检查分区信息：e2fsck -f /dev/sdxY
 - 9.调整分区大小：resize2fs -p /dev/sdxY
 - 10.重新挂载分区
 - 11.查看分区大小：df -h
26. 查看内核
 - uname -a
 - cat /proc/version
 - dmesg | grep Linux
27. 从U盘安装Linux系统
 - 1.制作安装介质
 - 2.准备安装的磁盘分区
 - 3.设置启动顺序
 - 4.进入U盘下的系统
 - 5.检查引导方式。efi+gpt或bios+mbr
 - 6.联网
 - 7.更新系统时间
 - 8.创建引导分区
 - 9.创建根分区
 - 10.挂载分区
 - 11.安装基本包
 - 12.设置fstab
 - 12.chroot
 - 13.设置时区
 - 14.设置字符集
 - 15.设置主机名
 - 16.设置root密码
 - 17.重启
100. 其它
 - 数据恢复：可以使用testdisk[操作手册](https://www.cgsecurity.org/wiki/Testdisk_%E6%93%8D%E4%BD%9C%E6%8C%87%E5%8D%97)
 - 制作安装介质：使用dd。windows下可以使用usbwriter

