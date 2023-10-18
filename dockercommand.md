#### Docker常用操作
1. 安装
 - yun -y install gcc
 - yum -y install gcc-c++
 - yum install -y yum-utils device-mapper-persistent-data lvm2
 - yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
 - yum clean all
 - yum makecache fast
 - yum -y install docker-ce
 - systemctl start docker
 - docker version
 - docker run hello-world
2. 帮助命令
 - docker version
 - docker info
 - docker --help
3. 镜像命令
 - docker images:查看所有本地镜像。-a显示所有本地镜像，-q只显示镜像id，--digests显示镜像缩略信息，--no-trunc 显示镜像完整信息
 - docker search <镜像名>：去镜像源搜索镜像 --no-trunc:完整镜像描述，-s收藏数不小于某值的镜像
 - docker pull <镜像名>:<版本>：拉取某镜像，不指定版本号则为latest
 - docker rmi <镜像名或id>:<版本>：删除镜像。可以多个删除，或docker rmi $(docker images -qa) 删除所有镜像
4. 容器命令
 - docker run <参数> <镜像名> <指令> <指令参数>：运行某镜像，生成容器。参数：--name 为容器取一个名字，-d 后台运行容器(容器后台运行容器内必须有一个前台进程)， -it 交互式容器，并生成一个伪交互终端。 -p 指定内外端口映射
 - 一般：docker run -it 镜像名 /bin/bash:产生一个交互容器
 - docker ps <参数>：查看容器。-a查看所有容器，-q只输出容器id，-l显示最近创建的一个容器，-n显示最近创建的n个容器
 - 退出容器：exit，退出并关闭容器。ctrl+p+q,容器不停止退出
 - docker start <容器名或id>：启动容器
 - docker restart <容器名或id> :重启容器
 - docker stop <容器名或id> :停止容器
 - docker kill <容器名或id> :强制停止容器
 - docker rm <容器名或id>:删除容器，docker rm $(docker ps -q -a),docker ps -q -a|xargs docker rm,删除所有容器
 - docker logs -ft --tail <信息条数> <容器名或id>：查看容器日志
 - docker top <容器id>:查看容器内进程
 - docker inspect <容器id>：查看容器内部详细信息
 - docker stat --no-stream <容器id>：查看容器的cpu、men、io信息。free -h 本质上是读取 /proc/meminfo 文件内容。stat读取的是容器内/sys/fs/cgroup/memory.stat
 - docker exec -it <容器id> /bin/bash:进入正在运行的容器，打开新的终端
 - docker attach <容器id>：进入正在运行的容器，不会打开新的终端
 - docker cp <容器id>:<容器内路径> <宿主机路径>:拷贝容器内文件到宿主机
 - ![](download.png)
6. docker镜像
 - docker镜像都是只读的，启动后会生成可写的容器层，之下都是只读的镜像层
 - docker commit -m="镜像描述" -a="作者" <容器id> <要生成的镜像名>:<版本>：将一个容器打包为一个镜像
7. 容器的数据卷
 - 一种持久化策略，也可以使容器间共享数据
 - docker run -v <宿主机绝对路径>:<容器内路径> <镜像名>：容器运行时挂载数据卷，没有路径会自动生成
 - 可以使用docker inspect <容器id> 查看是否挂载成功
 - 可以进行宿主与容器的数据共享。且容器停止后宿主修改挂载目录数据，容器启动后会自动同步
 - docker run -v <宿主机绝对路径>:<容器内路径>：ro <镜像名>:带权限，容器目录只能读，不可写
 - 也可使用dockerfile的VOLUME指令添加数据卷，不过挂载宿主机的目录需要查询inspect
 - 容器间共享数据：docker run -volumes-from <存在数据卷的父容器> <镜像名>
 - 容器间数据卷会相互继承，只要有一个容器的活动，数据卷内数据就一直同步着，数据卷的生命周期一直持续到没有容器使用它为止
8. Dockerfile
 - Dockerfile是用于构建docker镜像的文件，由命令与参数构成
 - docker build -f <Dockerfile文件位置> -t <生成的镜像名+版本号> . 在Dockerfile文件目录下执行可以没有-f
 - 流程：从基础镜像创建容器，执行Dockerfile中的指令，commit容器生成一个镜像层，重复上一步骤直到指令执行完
 - 主要的命令：
 - FROM 基础镜像
 - MAINTAINER 镜像作者与邮箱
 - RUN 容器构建时运行的命令，主要是shell
 - EXPOSE 容器暴露的端口
 - WORKDIR 容器运行后终端默认登陆的目录 
 - ENV 设置构建镜像过程的环境变量 ENV PATH /my/dest
 - ADD 为容器添加文件，会自动解压缩和解析url
 - COPY 从宿主复制文件到容器，COPY src dest
 - VOLUME 设置数据卷 
 - CMD 容器运行后执行的命令，会被覆盖
 - ENTRYPOINT 容器运行后执行的命令，不会被覆盖
 9. 问题
 - docker 权限问题：sudo chmod a+rw /var/run/docker.sock 运行这条命令就没问题了
