# Git的学习
## 初始化
首先你需要一个空文件夹，~~如果不怕麻烦的话，现有文件夹也是可以的~~，OK，现在我们拥有一个名为**learngit**的文件夹了。

执行命令`git init`

bang！ 现在我们拥有一个名为**learngit**的repository了。git会在该目录下创建.git文件用于保存git的一些操作信息，**勿删！**

## 创建文件
我们可以以任意手段创建一个文件readme.txt，需要注意的是，建议使用utf-8编码格式化的文件，否则的话，git可能将文本文件视为二进制文件，那样git的很多功能都无法体现出来了。

## 提交到stage和master
我们在本地使用notepad++,vim或者visual studio code等文本编辑器**对于文件做出的更改内容被git视为work内容，这些操作不会被git记录。**

为了将这些信息被git记录上，我们需要两个操作：
1. 将修改的文件放入stage，这里我们执行`git add readme.txt`，当然可以一次提交多个文件。
2. 让git把更改信息记录下来，需要我们执行`git commit -m "这里是commit备注"`，这样将stage的更改提交到master (master是真正的版本库，当然你可以改这个默认名字)

如果想要提交所有的更改，直接执行`git commit -a -m "这里是commit备注"`

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

经过这两项操作，我们已经将我们所做的更改让git记录下来了。当然我们可以将其视为一个小的版本。而且每个小版本还有我们的备注。

如果在提交到stage之前，我们想要看一下我们到底做出了哪些更改。我们可以执行`git diff`。

举个栗子：我给readme.txt里面最后一行加了个句号"."，执行`git diff`的结果如下：
```
PS D:\git\learngit> git diff
diff --git a/readme.txt b/readme.txt
index c9bb679..77a0fa4 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
 Git is a distributed  version control system.
-Git is a free software
\ No newline at end of file
+Git is a free software.
\ No newline at end of file
```

尽管我觉得不太需要，但是如果你忘了自己是否更改过什么文件，可以使用`git status`大概看一下自己更改了什么文件。

## 版本回滚
这可能是版本控制系统最大的作用了吧，当然，在git你可以滚来滚去，意思是只要是你**提交过的版本**，你都可以回到那个版本。

举个栗子：之前的版本线是这样的1->2->3->4->5，现在你想回到版本4，这当然可以。但是，你现在基于版本4创建了版本6，现在版本线是这样的1->2->3->4->6，一般来说是不能回到版本5的，因为它明显被版本6覆盖了。但是在git里我们还是可以回到版本5的。git可以让你放心的滚来滚去，这一切的前提在于commit。

具体怎么操作呢？有两种方法：

1.  git reset --hard HEAD^


    HEAD表示当前版本，HEAD^表示上一个版本，HEAD^^表示上上个版本，HEAD\~100表示前100个版本，当然我觉得正常人不会这么用HEAD\~100

2. git reset --hard "version_hash"

    version_hash 表示每次commit后git反馈的版本的hash，不要真的写"version_hash"，举个栗子：`git reset --hard 4b8091be3b9c`，这里的hash不用写全，写一部分让git认出来就行，比如也可以这么写`git reset --hard 4b80`，这个命令同上面一个命令达到一样的效果。

    那么如何获得hash呢？可以执行`git log`，这个是看当前版本线的，如果想要的版本不在当前版本线的话，执行`git relog`以查看所有的版本线。
    
## stage和work的回滚
**这部分暂时用不太上，仅供记录**

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。

## 远程仓库
目前为止，git的操作都是在本地进行的，但是为了协同工作或者展示，需要将仓库上传到服务器，[github](https://github.com)给我们提供了一个服务器，自己个人的一些项目就可以放到github上。

那么如何将自己的本地仓库推送到github呢？

1. 首先和github确认彼此的身份，类似登陆服务器。

    这里登陆使用的是rsa密钥的形式，先生成公钥和私钥：
    
    `ssh-keygen -t rsa -C youremail@example.com`
    
    生成的公钥和私钥**必须放到用户目录下的.ssh文件夹**，我的电脑上是C:\Users\用户名\\.ssh\。会生成两个文件id_rsa.pub是公钥，id_rsa是密钥。github需要你的id_rsa.pub里面的文件内容。

    进入github-Settings-SSH keys-New SSH key将id_rsa.pub里面的内容复制进去。现在github拥有公钥，自己拥有私钥，这样我们就可以匹配登陆了。

2. 在github上建立repository

    本地仓库名和远程的仓库名可能不一样，这里我们建立一个learngit。

3. 推送本地仓库到github的仓库

    -  执行`git remote add origin git@github.com:michaelliao/learngit.git`
    
        这里解释一下这个命令，`git remote`表示要对远程服务器进行操作，`add origin git@github.com:michaelliao/learngit.git` 表示将给定地址的repository给个小标签origin，之后origin就表示这个repository的地址了。

    - 执行`git push origin master`，意思是将本地的master branch推送到origin的master branch。详细内容可看：[git push详细用法](https://www.cnblogs.com/qianqiannian/p/6008140.html)