[TOC]

# 1、安装

- 查看是否已经安装

~~~bash
$git
~~~

- 查看操作系统类型

~~~bash
cat /etc/issue
~~~

- Debian或Ubuntu Linux版本（执行如下命令即可安装）

~~~bash
sudo apt-get install git;//12.04之后新版本
sudo apt-get install git-core;//12.04之前老版本
~~~

- 其他linux版本（源码安装）

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入以下命令即可：

~~~bash
$./config
$make
$sudo make install
~~~

- 配置

~~~bash
$ git config --global user.name "manan0611"

$ git config --global user.email "18713508805@163.com"
~~~

# 2、版本库管理

- 把这个目录变成Git可以管理的仓库

~~~bash
$git init
~~~

- 创建版本库副本

~~~bash
$git clone learngit learngit_bak
~~~

# 3、版本管理

- 把文件添加到Git仓库

~~~bash
$git add filename
~~~

- 将当前目录种的文件都添加到版本库

~~~bash
$ git commit -m "SOME COMMENTS"
//等价命令如下：
$git commit  --message=“SOME COMMENTS”
~~~

- 提交到暂存区并提交【<font color='red'>**不建议使用**</font>】

~~~bash
$git commit -a -m "SOME COMMENTS"
~~~

- 追加提交（不增加新的commit_id的情况下将新代码追加到前一次的commit_id中）【<font color='red'>**待深入学习**</font>】

~~~bash
$git commit --amend 
~~~

- 查看文件修改的状态

~~~bash
$git status
~~~

- 查看具体修改了什么内容

~~~bash
$git diff //查看尚未暂存的文件更新了哪些部分
$git diff filename //查看尚未暂存的某个文件更新了哪些
$git diff --cached //查看已经暂存起来的文件和上次提交的版本之间的差异
$git diff --cached filename //查看已经暂存起来的某个文件和上次提交的版本之间的差异
$git diff head //git diff和git diff --cached的合并
$git diff ffd98b291e0caa6c33575c1ef465eae661ce40c9 b8e7b00c02b95b320f14b625663fdecf2d63e74c //查看某两个版本之间的差异
$git diff ffd98b291e0caa6c33575c1ef465eae661ce40c9:filename b8e7b00c02b95b320f14b625663fdecf2d63e74c:filename //查看某两个版本的某个文件之间的差异
~~~

- 查看日志

~~~bash
$ git log
$ git log -- filename //查看某个文件的日志
$ git log --pretty=oneline  //只查看commit_id和comment列
$ git show //查看最近一次提交的详细信息
$ git show-branch --more=10 //额外展示10个版本的comment信息
~~~

- 版本回退

~~~bash
$ git reset
$ git reset --hard HEAD^ //回到上一个版本（慎用！！）
$ git reset --hard a766f4a //回到任意一个版本。a766f4a为commit_id的前几位（慎用！！）
$ git reflog //记录你每一次执行的命令.回退错了可以恢复回去。
~~~

<font color=red>**git reset用法区别**</font>

**git reset --soft commit_id**  //只是将commit的部分回退到commit_id对应版本；<font color='blue'>不动暂存区和工作区</font>。回退后的版本和回退前版本的差异是放在暂存区的。

**git reset （--mixed）commit_id** //将commit的部分回退到commit_id对应版本；<font color='blue'>覆盖暂存区，不覆盖工作区</font>。回退后和回退前版本的差异是放在工作区的。

//mixed可选，不写也是一样的

**git reset --hard commit_id**  //恢复至commit_id版本的同时，<font color='blue'>覆盖暂存区和工作区</font>。【**--hard一定要慎用！！！**】

- 撤销修改

git add 的时候，撤销修改：

~~~bash
$ git restore gitversion.txt //撤销的是工作区的部分
~~~

已经git add了，撤销修改：

~~~bash
$ git restore --staged gitversion.txt
$ git restore gitversion.txt
//先把add的退回到未add的状态，然后再撤销就可以了。
~~~

- 删除文件

~~~bash
$ rm filename
//删错了，恢复回来
$ git restore git_test.txt
//确实要删
$ git rm git_test.txt
$ git commit -m "delete"
~~~

- 重命名文件

~~~bash
$ git mv //直接commit即可
$ mv //需要add，然后再commit
~~~

# 4、远程版本库