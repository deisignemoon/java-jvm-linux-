# 常用操作
---
### java常用操作
1. java -version: 获得java版本号等信息
2. java 缩略设置
 -  -Xms512m： 等价于-XX：InitalHeapSize=512m,设置JVM初始堆内存为512m，初始大小内存，默认为物理内存1/64。
 -  -Xmx2048m:等价于-XX：MaxHeapsSize=2018m，设置JVM最大堆内存为2048m，建议二者设为相同大小。
 -  -Xss：设置单个线程的堆栈大小，一般默认为512K~1024K，等价于-XX:ThreadStackSize
 -  -Xmn：设置年轻代大小
3. java -XX:SurvivoRatio=8 设置新生代中eden区与from、to区的比例，默认为8：1：1，设置为4改为4：1：1
4. java -XX：+PrintFlagsFina -version 打印当前jvm的设置，-XX:+PrintFlagsInitial 打印初始设置
5. java -XX：+PrintGCDetails 程序运行后打印GC日志，默认为-XX：-PrintGCDetails，即不打印
6. java -XX:MetaspaceSize=128m 设置元数据区大小为128m，元数据区在堆外内存中
7. java -XX:MaxTenuringThreshold=15 设置进入老年代最多在from、to区交换15次，可设置最大值也为15
8. java -XX:+PrintCommandLineFlags -version 打印当前设置简略信息
9. java -XX：+PrintFlagsFina [java运行类名]，一边运行java类，并打印信息
10. java -XX:NewRatio=2，设置堆中老年代的占比，默认2：1
11. 设置G1垃圾回收器
 - -XX:+UseG1GC
 - -XX:G1HeapRegionSize=n : 设置G1区域的大小。值是2的幂，范围是1M到32M。目标是根据最小的Java堆大小划分出约2048个区域
 - -XX:MaxGCPauseMillis=n : 最大停顿时间，这是个软目标，JVM将尽可能（但不保证）停顿时间小于这个时间
 - -XX:InitiatingHeapOccupancyPercent=n  堆占用了多少的时候就触发GC，默认是45
 - -XX:ConcGCThreads=n  并发GC使用的线程数
 - -XX:G1ReservePercent=n 设置作为空闲空间的预留内存百分比，以降低目标空间溢出的风险，默认值是10%
12. javap <编译的class文件> 获得字节码指令文件 [javap](https://blog.csdn.net/qq_32447301/article/details/79779894?ops_request_misc=%7B%22request%5Fid%22%3A%22158320967919724847061727%22%2C%22scm%22%3A%2220140713.130056874..%22%7D&request_id=158320967919724847061727&biz_id=0&utm_source=distribute.pc_search_result.none-task)
### jvm调优与故障检查操作
1. jps 查看运行的java进程名和进程id
 - -l 查看完整进程名
2. jinfo java进程配置信息查看工具
 - jinfo -flags <进程id> 该进程配置信息
 - jinfo -flag <jvm参数名> <进程id> 查看该进程是否设置该参数，且参数值为
 - jinfo -flag [+|-]<jvm参数名> <进程id> 开启或关闭该参数
 - jinfo -flag <jvm参数名>=<value> <进程id> 设置该进程参数值
3. jstack jdk自带的线程堆栈分析工具，使用该命令可以查看或导出 java 应用程序中线程堆栈信息。
 - jstack <进程id> 查看当前时间点，指定进程的dump堆栈信息。
 - jstack -F <进程id> 当进程挂起了，可使用此参数来强制打印堆栈信息
 - jstack -m <进程id> 打印java和native c/c++框架的所有栈信息。可以打印JVM的堆栈，以及Native的栈帧 
 - jstack -l <进程id> 长列表. 打印关于锁的附加信息,会使得JVM停顿得长久得多,不建议使用
4. jmap
 - jmap -dump：format=b,file=location <进程id>，生成的文件可以使用jvisualvm工具查看分析。也可以加live参数只打印或者的对象：jmap -dump:live,format=b,file=gc.dhump <进程id>
 - jmap -heap <进程id>：打印堆使用的概况；
 - jmap -clstats <进程id>：打印出类加载器使用情况，主要用来看加载的类的数量，jdk8及以后才可使用。之前版本的jdk使用jmp -perstats pid命令；
 - jmap -histo[:live] <进程id>：打印heap中各类的实例数目，倒序排。加上live参数只打印活着的对象；
 - jmap -finalizerinfo <进程id>：F队列中等待执行finalize方法的对象的数目；
5. jstat 虚拟机运行时的状态信息,显示本地或者远程虚拟机进程中的类加载、内存、垃圾收集、JIT编译等信息。格式：jstat 选项 进程id 间隔时间 采集次数
 - jstat -class <进程id>：加载统计，Loaded:加载class的数量，Bytes：所占用空间大小，Unloaded：卸载的class数量，Bytes:卸载释放的空间，Time：加载和卸载耗费的时间
 - jstat -compiler <进程id>：JIT编译统计，Compiled：编译数量。Failed：失败数量，Invalid：不可用数量，Time：时间，FailedType：失败类型，FailedMethod：失败的方法
 - jstat -gc <进程id>：堆信息统计。S0C：第一个幸存区的大小，S1C：第二个幸存区的大小，S0U：第一个幸存区的使用大小，S1U：第二个幸存区的使用大小，EC：伊甸园区的大小，EU：伊甸园区的使用大小，OC：老年代大小，OU：老年代使用大小，MC：方法区大小，
MU：方法区使用大小
，CCSC:压缩类空间大小
，CCSU:压缩类空间使用大小
，YGC：年轻代垃圾回收次数
，YGCT：年轻代垃圾回收消耗时间
，FGC：老年代垃圾回收次数
，FGCT：老年代垃圾回收消耗时间
，GCT：垃圾回收消耗总时间 
 - jstat -gccapacity <进程id>：与-gc基本相同，主要关注堆各个区域使用到的最大最小空间。
NGCMN：新生代最小容量
，NGCMX：新生代最大容量
，NGC：当前新生代容量
，S0C：第一个幸存区大小
，S1C：第二个幸存区的大小
，EC：伊甸园区的大小
，OGCMN：老年代最小容量
，OGCMX：老年代最大容量
，OGC：当前老年代大小
，OC:当前老年代大小
，MCMN:最小元数据容量
，MCMX：最大元数据容量
，MC：当前元数据空间大小
，CCSMN：最小压缩类空间大小
，CCSMX：最大压缩类空间大小
，CCSC：当前压缩类空间大小
，YGC：年轻代gc次数
，FGC：老年代GC次数
 - 。。。 查看 [其他jstat用法](https://blog.csdn.net/An1090239782/article/details/102532370?ops_request_misc=%7B%22request%5Fid%22%3A%22158323246119724848311858%22%2C%22scm%22%3A%2220140713.130056874..%22%7D&request_id=158323246119724848311858&biz_id=0&utm_source=distribute.pc_search_result.none-task)
6. jhat 命令解析Java堆转储文件并启动WebServer。[参数解释](https://blog.csdn.net/top_explore/article/details/95166138?ops_request_misc=%7B%22request%5Fid%22%3A%22158321406319724811829286%22%2C%22scm%22%3A%2220140713.130056874..%22%7D&request_id=158321406319724811829286&biz_id=0&utm_source=distribute.pc_search_result.none-task)
 - jhat <-port 访问端口> <dump文件地址> 指令使用后可以在该端口访问获得堆信息
 - jhat -J-Xmx512m <heap dump file> dump出来的堆很大，在启动时会报堆空间不足的错误，可以使用
### 一般发生高cpu占用率排查
 - 第一步：使用top指令，定位CPU占用较高的进程。
 - 第二步：使用top -H -p ${进程id}指令，查看指定进程下各个线程的cpu使用情况。或使用：ps -mp <进程id> -o THREAD,tid,time
 - 第三步：使用printf "%x" <线程10进制id> 指令，将线程id转换为16进制。
 - 第四步：使用jstack pid指令，查看当前的堆栈信息；并根据上一步得到的16进制的线程id，找到肇事线程。若信息较多，可以使用：jstack <进程id> | grep -10 <线程16进制id>，-10为该行上下各10行信息，-A10为该行及之后10行信息，-B10为该行及之前10行信息
 - 第五步：分析肇事线程堆栈信息。![信息](https://img-blog.csdnimg.cn/2019052217072340.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2p1c3RyeV9kZW5n,size_16,color_FFFFFF,t_70)
①线程名。②线程优先级。③一个地址(该地址是什么地址，存疑)。④线程十六进制id。⑤线程状态。⑥线程当前所处方法。⑦该箭头表示线程的执行历程。
 - 此时，我们已经定位到了问题代码的位置⑥，接下来查看程序相应位置的代码，解决问题即可。
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
 - runlvel：返回结果中，第一个数为之前运行级别，后一个数为当前运行级别；
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
 - corntab：-e编辑任务，-l查询任务，-r删除该用户的所有任务
 - 任务设置：* * * * *，分别为秒，时，日，月，星期，以确实数字那些时间，/n每隔一段时间，0-5某段时间
 - 任务可以是shell指令，以.sh文件执行，记得加上可执行权限
 - at：延时命令。at <时间> ，写入命令后ctrl+d，设置命令。-l查看所有命令
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
 - netstat -anp:查看所有网络服务
 - ifstat
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
 - nc
 - telnet
17. linux状态查询
 - top：整机进程信息
 - vmstat：查看CPU(包含不限于)。vmstat -n 2 3 每2秒一次，一共3次
 - mpstat -P ALL 2：查看所有CPU核信息
 - pidstat -u 1 -p 进程编号：每个进程使用cpu的用量分解信息
 - free：应用程序可用内存数 -m使用mb计数
 - pidstat -p 进程号 -r 采样间隔秒数：查看额外
 - df -h：查看磁盘剩余空闲数
 - iostat -xdk 2 3：磁盘IO性能评估，每2秒一次，一共3次，可以下载iotop
 - pidstat -d 采样间隔秒数 -p 进程号：查看额外
 - ifstat 1：查看网络IO，1秒一次，可以下载iftop