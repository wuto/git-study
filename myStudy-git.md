##廖雪峰的git教程：

http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

#安装Git
   首先，你可以试着输入git，看看系统有没有安装Git：
   
	$ git
	The program 'git' is currently not installed. You can install it by typing:
	sudo apt-get install git
	
   像上面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。

   如果你碰巧用Debian或Ubuntu Linux，通过一条sudo apt-get install git就可以直接完成Git的安装，非常简单。        
   
   老一点的Debian或Ubuntu Linux，要把命令改为sudo apt-get install git-core，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。

   如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install这几个命令安装就好了。
   
   在Mac OS X上安装Git

   如果你正在使用Mac做开发，有两种安装Git的方法。

   一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/。

   第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。
   ![](http://www.liaoxuefeng.com/files/attachments/001384907061183ba2a452af9de4a8a8640339239bc3e5e000/0)  
