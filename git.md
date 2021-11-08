# git：分布式版本控制

与svn集中版本控制不同，git是分布式的，由本地的版本库，在本地管理版本。

## 基本操作

创建目录 并初始化：git init，生成.git文件：

![image-20210727124916736](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727124916736.png)

设置签名：

git config user.name Cuizhufan

git config  user.email 1435820234@qq.com



git status 查看状态（工作区，缓存区）

git add [file name]将文件添加至缓存区。修改的未提交至缓冲区的文件，git status显示为红色，git add 后变为绿色。

![image-20210727131107815](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727131107815.png)

git commit 提交至本地库，并输入修改信息。

git commit -m "修改信息" 文件名。//不用打开vim编辑器，填写修改信息

完成后：

![image-20210727131659394](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727131659394.png)

## 版本的前进后退

git log 查看提交的记录：

![image-20210727133146976](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727133146976.png)

git log --pretty=oneline 显示简洁一些

![image-20210727133312426](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727133312426.png)

 git log --oneline 更简洁

![image-20210727133533990](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727133533990.png)

git log reflog 显示当前版本到某一版本需要几步

![image-20210727133815183](C:\Users\agent\AppData\Roaming\Typora\typora-user-images\image-20210727133815183.png)

git reset --hard [索引值]：基于索引值的前进后退

git reset命令的三个参数对比：

--soft参数：

仅仅在本地库移动head指针

--mixed参数：

在本地库移动head指针

并重置缓存区

--hard参数：

在本地库移动head指针

重置缓存区

重置工作区

## 比较文件差异 

git diff [file name] 将工作区的文件与暂存区的对应文件的比较

git diff [本地库中历史版本 ] [file name] 将工作区的文件和本地库历史记录比较 例如和上一个版本比较：

git diff HEAD^ [filename]

不指定文件名的时候会比较工作区下的所有文件

## 分支操作

创建分支：giit branch [分支名]

查看分支：git branch -v

切换分支： git checkout [分支名]

合并分支：

​	第一步：切换到接受修改的分支（被合并，增加新内容）

​	git checkout [分支名]

​	第二步：执行merge命令

​	git merge [分支名]

# git操作指令

新增文件的命令：git add file或者git add .
提交文件的命令：git commit –m或者git commit –a
查看工作区状况：git status –s
拉取合并远程分支的操作：git fetch+git merge或者git pull（更新仓库）
查看提交记录命令：git reflog

# 提交冲突

提交时发生冲突，你能解释冲突是如何产生的吗？你是如何解决的？
	如公共类的公共方法，我和别人同时修改同一个文件，他提交后我再提交就会报冲突的错误。

1、手动修改发生冲突，在IDE里面一般都是对比本地文件和远程分支的文件，然后把远程分支上文件的内容手工修改到本地文件，然后再提交冲突的文件使其保证与远程分支的文件一致，这样才会消除冲突，然后再提交自己修改的部分。特别要注意下，修改本地冲突文件使其与远程仓库的文件保持一致后，需要提交后才能消除冲突，否则无法继续提交。必要时可与同事交流，消除冲突。
2、发生冲突，也可以使用命令。

通过git stash命令，把工作区的修改提交到栈区，目的是保存工作区的修改；
通过git pull命令，拉取远程分支上的代码并合并到本地分支，目的是消除冲突；
通过git stash pop命令，把保存在栈区的修改部分合并到最新的工作空间中；

https://www.cnblogs.com/wangqi2019/p/10645906.html