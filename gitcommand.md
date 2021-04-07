#### GIT常用指令
1. 本地仓库初始化：git init 或者 git clone <远程仓库地址>也会初始化本地仓库
2. 设置签名：
 - 项目级别/仓库级别：git config user.name <用户名> | git config user.email <邮箱地址>
 - 系统用户级别：git config --global user.name <用户名> | git config --global user.email <邮箱地址>
 - 优先级：采取就近原则，有项目级使用项目级，没有采用系统级，都没有则不允许
3. 基本操作
 - 状态查看：git status
 - 添加:git add <文件名> ，使用\.表示所有文件
 - 提交：git commit -m "提交信息" -a <文件名>
 - 查看历史记录：git log 。空格向下翻页，b向上翻页，q退出。git reflog
 - 查看提交内容：git show <版本号> 
 - 移动版本号：git reset --hard <版本号> 。git reset --hard HEAD^ 一个^表示向下移动一个版本。git reset --hard HEAD~n 移动n个版本
 - 三个版本移动参数：--soft 只移动本地库的指针。 --mixed 移动本地库指针，并重置暂存区。 --hard 移动本地库指针，并重置暂存区和工作区。
 - 比较文件差异：git diff <文件名> 比较工作区与暂存区的差异。git diff <本地库版本号> <文件名> 比较工作区与本地库文件差异。不加文件名，比较多个文件的差异
 - gitk:打开图形化操作界面，gitk & 可以同时使用控制台和图形化界面
4. 分支管理
 - 创建分支： git branch <分支名>
 - 查看所有分支： git branch -v
 - 切换分支： git checkout <分支名>
 - 合并分支： git checkout <主分支或合并分支> ，git merge <被合并的分支名>
 - 解决冲突： 打开冲突文件，将文件修改到满意，保存文件，git add <文件名>，git commit -m "信息"。记得commit不能加文件名
5. 远程仓库
 - 创建远程仓库地址别名： git remote <别名> <远程仓库地址>
 - 查看所有远程仓库： git remote -v
 - 推送到远程仓库： git push <远程仓库别名> <分支名>
 - 下载远程仓库：git clone <远程仓库地址> 。可以初始化本地库，下载远程仓库文件，创建别名为origin的远程仓库
 - 拉取远程仓库： git pull <远程仓库地址或别名> <远程分支名>。工作中，push前记得先pull，并解决冲突。
6. 团队工作
 - 先fork工作的远程仓库
 - clone到本地
 - 修改后push到自己的远程仓库
 - 对工作的远程仓库发起pull请求
