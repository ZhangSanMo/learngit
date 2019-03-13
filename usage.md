# 初始化
首先你需要一个空文件夹，~~如果不怕麻烦的话，现有文件夹也是可以的~~，OK，现在我们拥有一个名为**learngit**的文件夹了。

执行命令`git init`

bang！ 现在我们拥有一个名为**learngit**的repository了。git会在该目录下创建.git文件用于保存git的一些操作信息，**勿删！**

# 创建文件
我们可以以任意手段创建一个文件readme.txt，需要注意的是，建议使用utf-8编码格式化的文件，否则的话，git可能将文本文件视为二进制文件，那样git的很多功能都无法体现出来了。

# 提交到stage
我们在本地使用notepad++,vim或者visual studio code等文本编辑器**对于文件做出的更改内容被git视为work内容，这些操作不会被git记录。**

为了将这些信息被git记录上，我们需要两个操作
1. 将修改的文件放入stage，这里我们执行`git add readme.txt`，当然可以一次提交多个文件。
2. 让git把更改信息记录下来，需要我们执行`git commit -m "这里是commit备注"`

如果想要提交所有的更改，直接执行`git commit -a`

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
