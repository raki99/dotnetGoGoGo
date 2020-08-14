## Git

### Centos安装Git

```C#
// git yum安装,自动添加依赖,但不一定是最新版本
$ sudo yum install -y git
// git 源码安装
  // 安装依赖
$ sudo yum install -y wget
$ sudo yum install -y gcc-c++
$ sudo yum install -y zlib-devel perl-ExtUtils-MakeMaker
  // 官网下载最新版本的git源码包
$ wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz
$ tar -zxvf git-2.9.5.tar.gz
$ cd git-2.9.5
$ ./configure --prefix=/usr/local
$ make
$ sudo make install
// 查看git版本
$ git --version
// git使用  
  // 进入某一目录，Linux直接用命令行，Windows右键使用“Git Bash Here”
  // 配置一个用于提交代码的用户，配置一个用户的邮箱, 生成公钥和私钥（用于github）
  // tips：秘钥存储于C:\Users\27634.ssh文件夹中
$ git config --global user.name "raki99"
$ git config --global user.email "email@example.com"
$ ssh-keygen -t rsa -C "youremail@example.com"
  // 进入想要把其变成Git可以管理的仓库的目录，初始化仓库
$ git init
  // 和github通信，将步骤3中生成的公钥(id_rsa.pub文件中的内容)拷贝到github SSH and GPG keys
// 拷贝远端代码到本地
$ git clone git@server-name:path/repo-name.git
// 推送代码到远端
$ git remote add origin git@server-name:path/repo-name.git
$ git add 文件名
$ git commit -m "说明"
$ git push -u origin master
  
  
//安装git后常用命令
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

$ ssh-keygen -t rsa -C "youremail@example.com" 创建ssh key，用于和github通信
(秘钥存储于C:\Users\27634\.ssh，把公钥id_rsa.pub存储于github)

创建版本库
$ pwd 命令用于显示当前目录(没啥用)
$ git init 把这个目录变成Git可以管理的仓库(后续新建提交和ssh克隆需要)	

操作版本库
$ git add 文件名 添加文件(新增或者更改都需要先add)
$ git commit -m "说明" 提交到本地版本库

$ git status 查看仓库状态
$ git diff 文件名 查看修改的地方

版本回退(从一个commit恢复)
$ git log 查看版本历史
$ git reset --hard HEAD^ 回退到上个版本
$ git reset --hard 1094a 回退到特定版本号(commit以后回退)
$ git reflog 记录每一次命令

$ git checkout -- file 直接丢弃工作区的修改(add以前回退)
$ git reset HEAD <file> 添加到了暂存区时，想丢弃修改(add以后回退)

删除文件
$ git rm file(已经add/commit,在目录中删除)

$ git checkout -- file 删错了回退

远程仓库
$ git remote add origin git@server-name:path/repo-name.git 关联远程库
$ git push -u origin master 第一次的push
$ git push origin master 常用的push，本地分支会在服务器上新建分支
$ git pull 需要有关联的分支，第一次下拉最好新建一个空文件夹
$ git branch --set-upstream-to=origin/远程分支 本地分支 关联分支

$ git clone git@server-name:path/repo-name.git 克隆(不需要另建文件夹)

分支
$ git branch -a 查看所有分支
$ git branch -vv 查看分支关联
$ git branch dev 创建分支
$ git checkout dev 切换分支
$ git merge dev 合并某分支到当前分支
$ git merge --no-ff -m "msg" dev 普通模式合并，合并后的历史有分支
$ git branch -d dev 删除分支
$ git checkout -b dev 创建并切换分支


合并分支,无法merge
$ git stash save 名字 暂存工作状态
$ git pull origin dev 拉下来 
$ git stash list 查看已经暂存的状态
$ git stash pop stash@{0} 将暂存状态merge到当前分支
还有冲突时,手动修改文件,然后add/commit
$ git log --graph 分支合并图

bug分支issue
$ git stash 暂存工作状态
$ git stash list 查看暂存工作状态
$ git stash pop 恢复暂存状态并删除状态

开发分支feature
$ git branch -D <name> 强制删除未合并的分支

rebase
$ git rebase 本地未push的分叉提交历史整理成直线

标签
$ git tag 标签名 打在最新提交的commit上
$ git tag 查询所有标签
$ git tag 标签名 f52c633 给特定的commit打标签
$ git tag -a 标签名 -m "msg" commit的id 给标签设置说明
$ git show 标签名 查询标签内容
$ git tag -d 标签名 删除标签
$ git push origin 标签名 推送某个标签到远程
$ git push origin --tags 推送所有标签
$ git push origin :refs/tags/<tagname> 可以删除一个远程标签。
```