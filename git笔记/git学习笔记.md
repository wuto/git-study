#git学习笔记

##相关链接:

###1.git速成

http://stormzhang.com/github/2016/05/30/learn-github-fromzero3/

###2.解决身份问题不能提交的:

http://www.mamicode.com/info-detail-595153.html

###3.廖雪峰Git教程

http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000


==================================

##一 搜索并下载git

https://git-for-windows.github.io/ 或百度
国内镜像:http://pan.baidu.com/s/1skFLrMt#path=%252Fpub%252Fgit

##二 设置git


###1. 将git,??????/git/bin/路径加入系统环境变量

###2. 设置用户名和邮箱,

	git config user.email "这个是邮箱"
	
	git config user.name "你的名字"
	
	$ git config --global user.name "Your Name"
	
	$ git config --global user.email "email@example.com"
	
	//--global 用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

###3. 创建仓库目录,并进入 cd


###4. 初始化git,查看文件夹状态

	git init
	git status

###5. 添加,删除,提交文件	

	git add a.txt 				//将文件加入待提交缓存
	git rm a.txt 				//删除文件
	git commit -m '这是提交文件的注释'      //提交文件

###6. 撤销修改（删除）

	git checkout -- 文件名称		//丢弃工作区的修改内容,让这个文件回到最近一次git commit或git add时的状态
    //git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
	git reset HEAD 文件名称			//把暂存区的修改撤销掉（unstage），重新放回工作区,让这个文件回到最近一次git commit

###7. 查看文件修改内容,提交信息,工作区和版本库区别

	git diff				        	//查看被修改文件的内容
    git diff 文件名                     //查看文件与版本库的区别
	git diff HEAD -- 文件名 			  //查看工作区和版本库里面最新版本的区别
	git log					        	//查看提交信息
	git log --pretty=oneline			//查看提交信息,简化版
	git log --pretty=oneline --abbrev-commit  	//查看提交信息,超简化版

###8. 版本回退

	git reset --hard HEAD^ 				//返回上个版本
	git reset --hard HEAD^^ 			//返回上上个版本
	git reset --hard HEAD~100 			//返回前100个版本
	git reset --hard commit_id			//返回commit_id版本,commit_id为commit的版本号,版本号可通过 git log 或 						//git reflog 查看
	git reflog					//查看命令历史,可以找到各版本的版本号commit_id

###9. 查看分支,添加分支,删除分支,合并分支,切换分支


	git checkout -b a 				//创建并切换到分支a
	相当于以下两条命令：
	git branch a 					//创建分支a
    git checkout a 					//切换分支到a
    
	git branch					    //查看所有分支
	git branch -d a					//删除分支a,未合并时不会被删除
	git branch -D a 				//删除分支a,强制删除，删除没有被合并的分支时使用
	
	git merge a 					//合并指定分支到当前分支，必须先切换到主分支,合并a分支到当前分支
	git log --graph					//查看分支合并图
	git log --graph --pretty=oneline    //查看分支合并图（简化版）
	git log --graph --pretty=oneline --abbrev-commit //查看分支合并图（超简化版）
	
	
	git merge --no-ff -m "这里是注释" a     //禁用Fast forward的分支合并，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息
	
	
	合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
	
	

###10. 创建,切换标签

	git tag						//查看已创建的标签
	git tag v1.0 					//创建标签v1.0
	git tag v0.9 6224937				//创建版本id为,6224937,的版本标签为,v0.9
	git tag -a v0.1 -m "说明文字" 3628164		//用-a指定标签名，-m指定说明文字
	git tag -s v0.2 -m "说明文字" fec145a		//通过-s用私钥签名一个标签,签名采用PGP签名,必须首先安装gpg(GnuPG)
	git tag -d v0.1 				//删除一个本地标签
	    
	git push 库名 <标签名> 				//推送一个本地标签
	git push 库名 --tags 				//推送全部未推送过的本地标签
	git push 库名 :refs/tags/<标签名>		//删除一个远程标签
	git checkout v1.0 						//切换到标签v1.0
	git show 标签名称						//查看标签详情

###11. 远程仓库
	
####A. 本地创建SSH Key:id_rsa是私钥,id_rsa.pub公钥
	
	$ ssh-keygen -t rsa -C "youremail@example.com"	//在用户主目录里创建.ssh目录，里面有 id_rsa 和 id_rsa.pub 两个文件

####B. GitHub添加ssh key
	
	打开“Account settings”，“SSH Keys”页面;然后点“Add SSH Key”，填上任意Title，在Key文本框里粘贴 id_rsa.pub 文件的内容：

####C. GitHub创建一个新仓库
	
	[new repository]->[Repository name]->[Description]->[cteate respository]

####D. 把本地仓库的内容推送到GitHub仓库,与远程仓库建立关联,HTTPS/SSH为GitHub的远程仓库地址
	
	git remote add 远程仓库名称 HTTPS/SSH
	//Example		
	//git remote add tips git@github.com:zhangfor14/tips.git 		//SSH:git@github.com:zhangfor14/tips.git
	//git remote add helper https://github.com/zhangfor14/tips.git 	//HTTPS:https://github.com/zhangfor14/tips.git

####E. 把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
	
	git push 仓库名 master
	git push -u 仓库名 master
	//由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

####F. 从远程库克隆
	
	$ git clone git@github.com:zhangfor14/helper.git
	
####其它
    
    git remote              //查看远程库信息
    git remote -v           //显示更详细的信息
    
    
    $ git checkout -b dev origin/dev        //创建远程origin的dev分支到本地
    
    
    git branch --set-upstream dev origin/dev
    //设置dev和远程origin/dev分支的链接
    
#####多人协作

因此，多人协作的工作模式通常是这样：

    首先，可以试图用git push origin branch-name推送自己的修改；

    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

    如果合并有冲突，则解决冲突，并在本地提交；

    没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。


	
## 三 其它

### 1. 工作未完成，需要进行其他工作时
    $ git status        //保存工作区
    git stash list      //查看 stash 保存的内容
    恢复stash有两种方法：
    1.  git stash apply     //恢复stash
        git stash drop      //删除stash
    2.  git stash pop       //恢复并删除stash
    
    
    你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：
    $ git stash apply stash@{0}
    
### 2. 自定义Git

让Git显示颜色，会让命令输出看起来更醒目：
   
    $ git config --global color.ui true
    
#### 忽略特殊文件    

	在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore

最后一步就是把.gitignore也提交到Git，就完成了！当然检验.gitignore的标准是git status命令是不是说working directory clean。


如果你确实想添加该文件，可以用-f强制添加到Git：

    $ git add -f App.class

或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：

    $ git check-ignore -v App.class
    .gitignore:3:*.class    App.class

### 3. 配置别名


#### 基本配置
以后st就表示status
   
    $ git config --global alias.st status
    
很多人都用co表示checkout，ci表示commit，br表示branch：

    $ git config --global alias.co checkout
    $ git config --global alias.ci commit
    $ git config --global alias.br branch
    
    
命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名：

    $ git config --global alias.unstage 'reset HEAD'
    
配置一个git last，让其显示最后一次提交信息：

    $ git config --global alias.last 'log -1'
    
甚至还有人丧心病狂地把lg配置成了：

    git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
    
    
    
    
#### 配置文件

配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：

别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：




## 四 搭建Git服务器

在远程仓库一节中，我们讲了远程仓库实际上和本地仓库没啥不同，纯粹为了7x24小时开机并交换大家的修改。

GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。

搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的apt命令就可以完成安装。

假设你已经有sudo权限的用户账号，下面，正式开始安装。

### 1. 安装git：

    $ sudo apt-get install git

### 2. 创建一个git用户，用来运行git服务：

    $ sudo adduser git

### 3. 创建证书登录：

收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

### 4. 初始化Git仓库：

先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：

    $ sudo git init --bare sample.git

Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：

    $ sudo chown -R git:git sample.git

### 5. 禁用shell登录：

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：

    git:x:1001:1001:,,,:/home/git:/bin/bash

改为：

    git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell

这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

### 6. 克隆远程仓库：

现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

    $ git clone git@server:/srv/sample.git
    Cloning into 'sample'...
    warning: You appear to have cloned an empty repository.

剩下的推送就简单了。
管理公钥

如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。

这里我们不介绍怎么玩Gitosis了，几百号人的团队基本都在500强了，相信找个高水平的Linux管理员问题不大。
管理权限

有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。Gitolite就是这个工具。

这里我们也不介绍Gitolite了，不要把有限的生命浪费到权限斗争中。
小结

* 搭建Git服务器非常简单，通常10分钟即可完成；

* 要方便管理公钥，用Gitosis；

* 要像SVN那样变态地控制权限，用Gitolite。


