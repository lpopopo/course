## Git

Git是目前世界上最先进的分布式版本控制系统（没有之一）

下载安装好git 之后 ， 可以通过

$  git  --version            查看自己的git 版本号 ， 来确定自己是否安装成功



git安装成功之后在对git 进行相应的配置

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

创建版本库

```
$ mkdir   文件夹名称
$ cd          文件夹名称

然后在你自己新建的文件夹中进行初始化操作
$ git  init                                            #git init 初始化完成之后，会生成一个隐藏文件，用来追踪管理版本库
```



开始上传文件到相应的仓库

```
$ git add      #用来告诉git ， 讲文件添加进仓库
# git add .              此处的.  代表全选的意思 ， 将文件夹中的所有文件都添加到仓库中 ， 如果你只想将少量的文件添加 ， 也可以使用   git add 后面添加相应的文件名。
但是如果你想在大量文件中只有少量的文件不进行添加和上传 ， 可以在文件夹下添加相应的.gitgore ,在里面加入相应的文件名 ， 即可避免相关文件的上传
```



将文件提交到仓库

```
$ git commit - m    " "     -m 后面""中添加自己对于上传文件的描述 ， 
```

git commit  一个可以提交多个文件 ， 所以你可以在多次git add 后再使用git commit 进行相应的上传



最后就是将本地仓库中的文件推到远程仓库中

方式一 ： 

使用ssh方式 ， git 是支持 ssh验证的 。

首先生成ssh

```
$    ssh-keygen -t rsa -C "youremail@example.com"  
```

进行上面的命令输入后 ， 在windows下实在 user/   里面的一个.ssh文件中  

Linux 中是在 /home/用户名/.ssh/   文件夹里面   

```
ls@ls-X542URR:~$ cd /home/ls/.ssh
ls@ls-X542URR:~/.ssh$ ls
id_rsa  id_rsa.pub  known_hosts
```

其中  id_rsa 是私钥 ， 只有自己才能知道 ， id_rsa.pub 是公钥 ，公共的 。

然后当你申请完自己的ssh后，你需要将自己的公钥添加到自己的githup上 ， 这样才能进行相应的验证。

上传完成之后 ：

```
git remote add origin git@github.com:michaelliao/learngit.git       //冒号后面应该根据自己的情况进行相应的输入
```

添加完成之后，远程仓库的名字就叫origin , git 默认的名字也是 origin

接下来最后一部就是将本地的仓库推到githup上 ， 

```
$ git push -u origin master
```



方式二 ： 

利用用户名和密码进行验证 ：

在你进行 git  push  之后会进行相应的用户名和密码的输入。





## Markdown语法

标题     

#一级标题

##二级标题

加粗

*一个斜体       两个加粗  三个加粗斜体

引入图片



