[TOC]

# 1、安装

- **查看是否已经安装**

~~~bash
$git
~~~

- **查看操作系统类型**

~~~bash
cat /etc/issue
~~~

- **Debian或Ubuntu Linux版本（执行如下命令即可安装）**

~~~bash
sudo apt-get install git;//12.04之后新版本
sudo apt-get install git-core;//12.04之前老版本
~~~

- **其他linux版本（源码安装）**

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入以下命令即可：

~~~bash
$./config
$make
$sudo make install
~~~

- **配置**

~~~bash
$ git config --global user.name "manan0611"

$ git config --global user.email "18713508805@163.com"
~~~

# 2、版本库管理

- **把这个目录变成Git可以管理的仓库**

~~~bash
$git init
~~~

- **创建版本库副本（本地到本地）**

~~~bash
$git clone learngit learngit_bak
~~~

# 3、版本管理

- **把文件添加到Git仓库**

~~~bash
$git add filename
~~~

- **将当前目录种的文件都添加到版本库**

~~~bash
$ git commit -m "SOME COMMENTS"
//等价命令如下：
$git commit  --message=“SOME COMMENTS”
~~~

- **提交到暂存区并提交**【<font color='red'>**不建议使用**</font>】

~~~bash
$git commit -a -m "SOME COMMENTS"
~~~

- **追加提交**（不增加新的commit_id的情况下将新代码追加到前一次的commit_id中）【<font color='red'>**待深入学习**</font>】

~~~bash
$git commit --amend 
~~~

- **查看文件修改的状态**

~~~bash
$git status
~~~

- **查看具体修改了什么内容**

~~~bash
$git diff //查看尚未暂存的文件更新了哪些部分
$git diff filename //查看尚未暂存的某个文件更新了哪些
$git diff --cached //查看已经暂存起来的文件和上次提交的版本之间的差异
$git diff --cached filename //查看已经暂存起来的某个文件和上次提交的版本之间的差异
$git diff head //git diff和git diff --cached的合并
$git diff ffd98b291e0caa6c33575c1ef465eae661ce40c9 b8e7b00c02b95b320f14b625663fdecf2d63e74c //查看某两个版本之间的差异
$git diff ffd98b291e0caa6c33575c1ef465eae661ce40c9:filename b8e7b00c02b95b320f14b625663fdecf2d63e74c:filename //查看某两个版本的某个文件之间的差异
~~~

- **查看日志**

~~~bash
$ git log
$ git log -- filename //查看某个文件的日志
$ git log --pretty=oneline  //只查看commit_id和comment列
$ git show //查看最近一次提交的详细信息
$ git show-branch --more=10 //额外展示10个版本的comment信息
$ git log --graph --pretty=oneline --abbrev-commit //查看日志对于分支合并的记录情况
//--abbrev-commit表示只显示commit_id的前几个字符,而非所有的 40 个字符
~~~

- **版本回退**

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

- **撤销修改**

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

- **删除文件**

~~~bash
$ rm filename
//删错了，恢复回来
$ git restore git_test.txt
//确实要删
$ git rm git_test.txt
$ git commit -m "delete"
~~~

- **重命名文件**

~~~bash
$ git mv //直接commit即可
$ mv //需要add，然后再commit
~~~

# 4、远程版本库

- **推送到远程库**

~~~bash
$ git remote add origin https://github.com/manan0611/learngit.git
~~~

说明：git默认的远程库名是origin

-----------

<font color='red'>如果url地址写错了怎么办</font>

可以通过如下命令取消

~~~bash
$ git remote rm origin
~~~

通过如下命令可以查看远程库的地址（删除后可以执行这个查看一下，结果为空就是对的）

~~~bash
$ git remote -v
~~~

-----------------------------

接下来，把本地库的所有内容推送到远程库上

~~~bash
$ git push -u origin master
~~~

说明：第一次用-u，不仅推送master分支，且建立本地和远程的关联

后续可以简化命令为`git push origin master`，提交后可以直接用此命令push

- **从远程库上克隆 git clone**

克隆之前，需要先生成SHH KEY。步骤如下：

~~~bash
//查看一下是否生成了id_rsa文件，如果没有说明没有生成ssh key
$ cd ~/.ssh
//如果没有生成ssh key，需要执行如下命令生成ssh key
$ ssh-keygen -t rsa -C "manan0611"
~~~

打开/c/Users/Lenovo/.ssh这个路径下的id_rsa.pub文件，复制其中的ssh key

打开github，个人>>settings>>SSH and GPG keys 点击 New SSH key ，起个名，把复制的ssh key命令粘上去

执行克隆命令：

~~~bash
$ git clone git@github.com:manan0611/futures.git
~~~

# 5、分支管理

- **创建和切换分支 git branch & git checkout&git switch**

```bash
$ git checkout -b brfutures  //创建并切换到新的分支brfutures上

//说明：上面的checkout -b 相当于下面两个语句
$ git branch brfutures  // 创建分支brfutures
$ git checkout brfutures //切换到brfutures分支下面

//说明：上面的git checkout -b brfutures等同于如下语句
$ git switch -c brfutures

//说明：上面的git checkout brfutures等同于如下语句
$ git switch master

$ git branch //查看分支（当前分支前用*标记）
* brfutures
  main
```

在 brfutures分支上了，我们在"README.md"里增加一行"add by brfutures"。然后提交， brfutures 分支中的README.md包含新增项，main分支不包含新增项。

- **合并 git merge**

  把brfutures分支合并回 *master* 

  ```bash
  $ git branch //查看当前分支，如果不是master需要checkout切换
    brlearn
  * master
  
  $ git merge brfutures  //合并brfutures分支到当前分支
  ```

  合并完成后，就可以删除 brfutures分支了，删除后，查看 *`branch`*，就只剩下 *`master`* 分支了。如下：

  ```bash
  $ git branch -d brfutures  //删除brfutures分支
  //如果分支没有被合并，在执行上述删除语句会提示，想要强制删除，可以将-d改成-D即可强制删除
  $ git branch
  * master
  ```

使用`git merge brfutures`默认是使用fast-forward模式，这种模式下，删除分支后，会丢掉分支信息。建议使用如下命令：

~~~bash
git merge --no-ff -m "some comments" brnoff
~~~

<font color='red'>**对比ff模式和no-ff模式区别**</font>

创建分支fftest使用fast-forward  f1.txt

git switch -c fftest
~~~bash
*673fd59 (HEAD -> fftest, main) Merge branch 'brff'
...
~~~

echo 'add by fftest ***'>f1.txt
git add f1.txt
git commit -m "commit f1.txt by fftest"

~~~bash
*   ee685ed (HEAD -> fftest) commit f1.txt by fftest
*   673fd59 (main) Merge branch 'brff'
    ...
~~~

git switch main

~~~bash
*   673fd59 (HEAD -> main) Merge branch 'brff'
...
~~~

git merge fftest

~~~bash
* ee685ed (HEAD -> main, fftest) commit f1.txt by fftest
*   673fd59 Merge branch 'brff'
...
~~~

创建分支nofftest使用禁用fast-forward  f2.txt

git switch -c nofftest

~~~bash
* ee685ed (HEAD -> nofftest, main, fftest) commit f1.txt by fftest
*   673fd59 Merge branch 'brff'
...
~~~

echo 'add by nofftest ***'>f2.txt
git add f2.txt
git commit -m "commit f2.txt by nofftest"

~~~
* dd2c509 (HEAD -> nofftest) commit f2.txt by nofftest
* ee685ed (main, fftest) commit f1.txt by fftest
*   673fd59 Merge branch 'brff'
...
~~~

git switch main

~~~bash
* ee685ed (HEAD -> main, fftest) commit f1.txt by fftest
...
~~~

git merge --no-ff -m "merge nofftest to main" nofftest

~~~bash
*   81420e1 (HEAD -> main) merge nofftest to main
|\
| * dd2c509 (nofftest) commit f2.txt by nofftest
|/
* ee685ed (fftest) commit f1.txt by fftest
*   673fd59 Merge branch 'brff'
...
~~~

总结：可以看出，使用默认的ff方式，体现不出分支merge记录，而使用no-ff时，因为会创建一个新的commit，可以将分支的提交comment和合并的comment都展示出来。恢复的时候有用处：

对于ff方式来说，恢复至ee685ed，只能恢复成合并以后的状态；

对于noff方式来说，恢复至dd2c509表示此时分支没有合并；恢复至81420e1表示此时分支合并了。

![image-20210520150909558](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210520150909558.png)

<font color='red'>**如果删除了分支后发现删错了想恢复怎么办？**</font>

用reflog命令，查看想恢复分支的commit_id，然后执行如下语句，可以恢复至目标节点：

~~~bash
$ git branch brfuture commit_id
~~~

需要注意的是，此时只是恢复了分支brfuture到目标节点，对于其他分支，没有发生任何改变。

<font color='red'>**合并分支之前想要知道两个分支的差别怎么做？**</font>

假设我们有两个分支，dev和master（以下比较均仅针对提交内容）

查看dev有，而master中没有的

~~~bash
$ git log dev ^master
//或者用如下命令，表示dev比master多提交的内容（与上面结果一样）
$ git log master..dev
~~~

查看master中有，而dev中没有的内容：

~~~bash
$ git log master ^dev
//或者用如下命令，表示master比dev多提交的内容（与上面结果一样）
$ git log dev..master
~~~

如果不知道谁提交的多，谁提交的少，可以用如下命令查看各自的提交：

~~~bash
$ git log --left-right dev...master
~~~

“>”表示是master提交的，“<”表示是dev提交的。

- **解决冲突（人工合并）**

如果发生冲突，在merge的时候会提示：Automatic merge failed; fix conflicts and then commit the result.类似的信息

此时 git status会提示我们哪个文件发生了冲突。

通过cat filename（查看冲突文件的内容），里面有提示哪里有差别

通过vi filename 手工修改解决冲突，然后add，commit即可。

- **通过bug分支修复缺陷 git stash**

切换分支时，如果当前分支有没做完的内容，可以用如下命令进行暂存：

~~~bash
$ git stash //会生成id用于区分
$ git stash save "commet" //可以自己加描述
~~~

查看暂存清单：

~~~bash
$ git stash list
~~~

恢复的时候，暂存清单由上到下依次恢复，例如：

~~~bash
$ git stash list
stash@{0}: On test1: test-2
stash@{1}: On test1: test-1
stash@{2}: On main: m
~~~

如果默认恢复，需要先在test1分支上恢复stash@{0}

~~~bash
$ git stash pop //恢复暂存内容并且删除stash list
//等同于如下两条命令：
$ git stash apply //恢复暂存内容
$ git stash drop //删除stash list内容
~~~

如果想要恢复某一个暂存节点，需要执行id，例如：

~~~bash
$ git stash list
stash@{0}: On test1: test-2
stash@{1}: On test1: test-1
stash@{2}: On main: m
$ git stash pop stash@{1}
//或者
$ git stash apply stash@{1}
$ git stash drop stash@{1}
~~~

注意：

git stash不针对特定的分支，切换分支后，stash内容不变，所以弹出时要小心；

git stash pop或者drop后，stash的序号会自动改变，连续弹出时要注意。

- 将master分支的修复，merge到其他dev分支 git cherry-pick

`git cherry-pick` 复制一个特定的提交到当前分支

执行此命令的前提是当前分支的工作已完成且全部提交。

bug在其他分支修改时，会有一个commit_id，例如：

~~~bash
$ git commit -m "Git learn: fix issue-001"
[brissue-001 10baade] Git learn: fix issue-001
~~~

找到它，并且执行：

~~~bash
$ git cherry-pick 10baade
~~~

如果合并发生冲突，手工解决就可以了。