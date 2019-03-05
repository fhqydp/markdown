#  git 培训  

一. 安装及基本配置
-
	# 服务端 创建远程仓库
    # 1. 安装并创建git用户
    [root@c000 ~]# yum install -y git1
    [root@c000 ~]# git --version
    git version 1.8.3.1
    2服务器端创建 git 用户，用来管理 Git 服务，并为 git 用户设置密码
    [root@c000 ~]# id git1
    id: git: no such user
    [root@c000 ~]# useradd git1
    [root@c000 ~]# passwd git1
    更改用户 git 的密码
    新的 密码：
    无效的密码： 密码少于 8 个字符
    重新输入新的 密码：
    passwd：所有的身份验证令牌已经成功更新。
	
	# 2. 服务器端创建 Git 仓库
	登录git1用户
	[root@c000 ~]#su - git1
    设置 /home/git1/repository/project.git为 Git 仓库
	[git1@c000 ~/repository]$mkdir -p /home/git1/repository/project.git
	[git1@c000 ~/repository]$ll
    总用量 0
    drwxrwxr-x. 2 git1 git1 6 3月   5 09:46 project.git

	# 3.初始化空的 Git 版本库
    [git1@c000 ~/repository]$git init --bare /home/git1/repository/project.git/   
	[git1@c000 ~/repository/project.git]$ll
    总用量 12
    drwxrwxr-x. 2 git1 git1   6 3月   5 09:54 branches
    -rw-rw-r--. 1 git1 git1  66 3月   5 09:54 config
    -rw-rw-r--. 1 git1 git1  73 3月   5 09:54 description
    -rw-rw-r--. 1 git1 git1  23 3月   5 09:54 HEAD
    drwxrwxr-x. 2 git1 git1 242 3月   5 09:54 hooks
    drwxrwxr-x. 2 git1 git1  21 3月   5 09:54 info
    drwxrwxr-x. 4 git1 git1  30 3月   5 09:54 objects
    drwxrwxr-x. 4 git1 git1  31 3月   5 09:54 refs
    
> 1.git init 创建本地仓库(在工程目录下创建) </br>
2.git init --bare 创建远端仓库（在服务器或者工程目录以外路径都可以创建的备份仓库）
工程commit到1中，push到2中；

	# 3. 客户端clone
    安装
	验证
	鼠标右击如果看到有两个git单词则安装成功	
	Git GUI Here
	Git Bash Here

    # 4、Git初始化
    
    1、Git安装之后需要进行一些基本信息设置
      　a、设置用户名：   git config -- global  user.name  '你再github上注册的用户名';
    　　b、设置用户邮箱： git config -- global  user.email  '注册时候的邮箱';   
    注意：该配置会在github主页上显示谁提交了该文件
    　　c、配置ok之后，我们用如下命令来看看是否配置成功
     　　git config --list
    注意：git  config --global 参数，有了这个参数表示你这台机器上所有的git仓库都会使用这个配置，当然你也可以对某个仓库指定不同的用户名和邮箱
	
    zhaoqf@zhaoqf-HP MINGW64 /d/git/repository  
    $ git config --list  
    core.symlinks=false  
    core.autocrlf=true  
    color.diff=auto  
    color.status=auto  
    color.branch=auto  
    color.interactive=true  
    pack.packsizelimit=2g  
    help.format=html  
    http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt  
    diff.astextplain.textconv=astextplain  
    rebase.autosquash=true  
    user.name=zhaoqingfu  
    user.email=fhqydp@163.com  
	
	全局配置文件
	c:\Users\zhaoqf\.gitconfig
	[user]
	name = zhaoqingfu
	email = fhqydp@163.com
	
	本地目录配置
	~/.git/config

	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project/.git (GIT_DIR!)
	$ cat config

	[core]
	        repositoryformatversion = 0
	        filemode = false
	        bare = false
	        logallrefupdates = true
	        symlinks = false
	        ignorecase = true
	        hideDotFiles = dotGitOnly
	[remote "origin"]
	        url = git1@192.168.130.200:/home/git1/repository/project.git
	        fetch = +refs/heads/*:refs/remotes/origin/*
	[branch "master"]
	        remote = origin
	        merge = refs/heads/master

	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project/.git (GIT_DIR!)
	$ ll
	total 7
	-rw-r--r-- 1 zhaoqf None 344 三月  5 03:07 config
	-rw-r--r-- 1 zhaoqf None  73 三月  5 03:06 description
	-rw-r--r-- 1 zhaoqf None  23 三月  5 03:06 HEAD
	drwxr-xr-x 1 zhaoqf None   0 三月  5 03:06 hooks/
	drwxr-xr-x 1 zhaoqf None   0 三月  5 03:06 info/
	drwxr-xr-x 1 zhaoqf None   0 三月  5 03:06 objects/
	drwxr-xr-x 1 zhaoqf None   0 三月  5 03:06 refs/


	# 5. clone
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ git clone git1@192.168.130.200:/home/git1/repository/project.git
	Cloning into 'project'...
	warning: You appear to have cloned an empty repository.
	Checking connectivity... done.
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ ll
	total 0
	drwxr-xr-x 1 zhaoqf None 0 三月  5 04:40 project/

	$ cat config
	[core]
	        repositoryformatversion = 0
	        filemode = false
	        bare = false
	        logallrefupdates = true
	        symlinks = false
	        ignorecase = true
	        hideDotFiles = dotGitOnly
	[remote "origin"]
	        url = git1@192.168.130.200:/home/git1/repository/project.git
	        fetch = +refs/heads/*:refs/remotes/origin/*
	[branch "master"]
	        remote = origin
	        merge = refs/heads/master

	# 6. 免密
	客户端创建 SSH 公钥和私钥
	C:\Users\zhaoqf\.ssh
	zhaoqf@zhaoqf-HP MINGW64 /d/git/www/gittest_gitbash
	Git Bash端
	$ ssh-keygen -t rsa -C "fhqydp@163.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/c/Users/zhaoqf/.ssh/id_rsa):
	/c/Users/zhaoqf/.ssh/id_rsa already exists.
	Overwrite (y/n)?

	# 服务器
	[git1@c000 ~]$mkdir -p /home/git1/.ssh
	# 客户端
	GIT bash端上传
	zhaoqf@zhaoqf-HP MINGW64 ~
	$ cd
	
	zhaoqf@zhaoqf-HP MINGW64 ~
	$ pwd
	/c/Users/zhaoqf
	
	zhaoqf@zhaoqf-HP MINGW64 ~
	$ ssh git1@192.168.130.200 'cat >> .ssh/authorized_keys' <~/.ssh/id_rsa.pub
	git1@192.168.130.200's password:

	zhaoqf@zhaoqf-HP MINGW64 ~
	$
	 
	# 服务器
	
	[git1@c000 ~]$pwd
	/home/git1
	[git1@c000 ~]$chmod 700 .ssh/

	[git1@c000 ~]$cd .ssh/
	[git1@c000 ~/.ssh]$chmod 600 authorized_keys 

> 重要：
> 	修改 .ssh 目录的权限为 700  
> 	修改 .ssh/authorized_keys 文件的权限为 600  
	
	# 测试免密clone
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ git clone git@192.168.130.200:/home/git1/repository/project.git
	Cloning into 'project'...
	fatal: '/home/git1/repository/project.git' does not appear to be a git repository
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights
	and the repository exists.

	禁止 git 用户 ssh 登录服务器
	$ /etc/passwd
	找到：
	zhaoqf:x:1000:1000:zhaoqf:/home/zhaoqf:/bin/bash
	git:x:1001:1001::/home/git:/bin/bash
	git1:x:1002:1002::/home/git1:/bin/bash

	修改为
	zhaoqf:x:1000:1000:zhaoqf:/home/zhaoqf:/bin/bash
	git:x:1001:1001::/home/git:/bin/git-shell
	git1:x:1002:1002::/home/git1:/bin/git-shell
二. 基本操作
-
	增加
	$ git clone git1@192.168.130.200:/home/git1/repository/project.git
	$ touch work
	$ git status
	$ git add work
	$ git reset HEAD work
	$ git commit -m "work" work
	$ git push origin master

	撤消
	工作区:git checkout -- work
	暂存区:git reset work
	仓库区:git reset -- hard head^
	
	1版本回退
	查看历史版本
	$ git log
	$ git log --pretty=oneline
	
	上一版本 （Head是当前版本）
	$ git reset --hard head^
	$ git reset --hard head^^
	$ git reset --hard head~100
	指定版本：
	查看以前的操作版本
	$ git reflog
	$ git reset --hard 2c9d



二. 远程仓库
-
	# 1. clone
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ git clone git1@192.168.130.200:/home/git1/repository/project.git
	Cloning into 'project'...
	warning: You appear to have cloned an empty repository.
	Checking connectivity... done.
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ ll
	total 0
	drwxr-xr-x 1 zhaoqf None 0 三月  5 04:40 project/
	本地配置文件
	cat /d/git/repository/project/.git/config
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project/.git (GIT_DIR!)
	$ cat config
	[core]
	        repositoryformatversion = 0
	        filemode = false
	        bare = false
	        logallrefupdates = true
	        symlinks = false
	        ignorecase = true
	        hideDotFiles = dotGitOnly
	[remote "origin"]
	        url = git1@192.168.130.200:/home/git1/repository/project.git
	        fetch = +refs/heads/*:refs/remotes/origin/*
	[branch "master"]
	        remote = origin
	        merge = refs/heads/master
	# 查看远程仓库
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project (master)
	$ git remote -v
	origin  git1@192.168.130.200:/home/git1/repository/project.git (fetch)
	origin  git1@192.168.130.200:/home/git1/repository/project.git (push)
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project (master)
	$ git remote show origin
	* remote origin
	  Fetch URL: git1@192.168.130.200:/home/git1/repository/project.git
	  Push  URL: git1@192.168.130.200:/home/git1/repository/project.git
	  HEAD branch: (unknown)
	  Local branch configured for 'git pull':
	    master merges with remote master

	基本操作:
	D:\git\repository\project\model\work.txt

	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project (master)
	$ git status
	On branch master
	
	Initial commit
	
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	
	        model/
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project (master)
	$ git commit -m "work.txt"
	[master (root-commit) d62170c] work.txt
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 model/work.txt
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project (master)
	$ git push origin master
	Counting objects: 4, done.
	Writing objects: 100% (4/4), 248 bytes | 0 bytes/s, done.
	Total 4 (delta 0), reused 0 (delta 0)
	To git1@192.168.130.200:/home/git1/repository/project.git
	 * [new branch]      master -> master

	
	# 2. 自建
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ mkdir project1
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository
	$ cd project1

	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1
	$ git init
	Initialized empty Git repository in D:/git/repository/project1/.git/

	
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

        model/

	nothing added to commit but untracked files present (use "git add" to track)
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1 (master)
	$ git add .
	warning: LF will be replaced by CRLF in model/work.txt.
	The file will have its original line endings in your working directory.
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1 (master)
	$ git commit -m "project1"
	[master (root-commit) 46b8c7b] project1
	warning: LF will be replaced by CRLF in model/work.txt.
	The file will have its original line endings in your working directory.
	 1 file changed, 1 insertion(+)
	 create mode 100644 model/work.txt

	创建远程仓库并与之关联
	[git1@c000 ~/repository]$git init --bare project1.git
	初始化空的 Git 版本库于 /home/git1/repository/project1.git/

	关联
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1 (master)
	$ git remote
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1 (master)
	$ git remote add origin 192.168.130.200:/root/home/git1/repository/projetc1.git
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1 (master)
	$ git remote -v
	origin  192.168.130.200:/root/home/git1/repository/projetc1.git (fetch)
	origin  192.168.130.200:/root/home/git1/repository/projetc1.git (push)

	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1/.git (GIT_DIR!)
	$ git remote rm origin

	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1/model (master)
	$ git remote add origin git1@192.168.130.200:/root/home/git1/repository/project1.git
	
	zhaoqf@zhaoqf-HP MINGW64 /d/git/repository/project1/model (master)
	$ git remote -v
	origin  git1@192.168.130.200:/home/git1/repository/project1.git (fetch)
	origin  git1@192.168.130.200:/home/git1/repository/project1.git (push)

	# 3. github
	$ git remote add origin https://github.com/fhqydp/markdown.git
	$ git push -u origin master
	https://github.com/fhqydp/markdown/blob/master/gitPx.MD

四. 冲突处理
-
上传测试 2

五. 分支管理
-


    