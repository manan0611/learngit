# Git学习

[toc]

## 一、Git简介

### 集中式vs分布式

|模式|代表|特点|
|---|---|---|
|集中式|CVS、SVN|1、必须中央服务器<br>2、必须联网才能使用<br>3、中央服务器挂了，大家都歇了|
|分布式|Git、BitKeeper、Bazaar|1、无中央服务器<br>2、每台电脑都是完整仓库<br>3、互相推送各自改动的内容<br>4、互为备份，避免丢失|

## 二、Git安装

### 2.1 Linux版本安装

- 查看是否已经安装

```shell
$git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```

说明：$git为查询命令；sudo apt-get install git提示安装命令

- 查看操作系统类型

~~~
cat /etc/issue
~~~

- Debian或Ubuntu Linux版本（执行如下命令即可安装）

```shell
sudo apt-get install git;//12.04之后新版本
sudo apt-get install git-core;//12.04之前老版本
```

- 其他linux版本（源码安装）

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入以下命令即可：

```shell
$./config
$make
$sudo make install
```

### 2.2 Windows版本安装（git config）

- 安装

在Windows上使用Git，可以从Git官网直接下载安装程序，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，弹出命令窗口，说明Git安装成功！

- 配置

安装完成后，还需要最后一步设置，在命令行输入以下两行命令：

```bash
$ git config --global user.name "manan0611"

$ git config --global user.email "18713508805@163.com"
```

注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

也可以用GIT_AUTHOR_NAME和GIT_AUTHOR_EMAIL环境变量来配置。

另，以上内容记录在".gitconfig"文件中。

```bash
$ cat /c/Users/lenovo/.gitconfig
[user]
        name = Liujx
        email = liujixia0410@163.com
[gui]
        recentrepo = Z:/Git/learngit
```

## 三、版本库repository管理

### 3.1 创建版本库（git init命令&git clone命令）

可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

- 1、建一个新目录（我起名learngit）

```bash
$cd /z/Git
$mkdir learngit
$cd learngit
$pwd
/z/Git/learngit
```

- 2、通过 ***`git init`*** 命令把这个目录变成Git可以管理的仓库

```bash
$cd /z/Git/learngit
$git init
Initialized empty Git repository in Z:/Git/learngit/.git/
```

Git仓库建好了，而且是一个空的仓库（empty Git repository）.
当前目录（/z/Git/learngit）下多了一个<font color="red">.git</font>的目录（隐藏目录），是Git跟踪管理版本库的，<font color="red">千万不能动</font>。

- 3、创建版本库副本

  ***`git clone learngit learngit_bak `***    //需要在learngit 上层目录执行此命令。

  克隆的learngit_bak和learngit保函相同的对象、文件和目录。一旦复制了一个版本库，就可以修改这个复制版本、做出新的提交、查看它的日志和历史等。这是一个有着完整历史的版本库。

### 3.2 版本管理

#### 3.2.1 git add & git commit

将学习笔记《Git_Learn_Note.md》放到版本控制目录下，即"/z/Git/learngit"下面，子目录也行
<font color="blue">我建了子目录，实际放在"/z/Git/learngit/git_learn_notes"</font>

- ***git add***
第一步，使用 ***`git add`*** 命令，把文件添加到Git仓库
这步执行之后，是没有任何提示的

```bash
$git add Git_Learn_Note.md
```

- ***git commit***
第二步，使用 ***`git commit`*** 命令，把文件提交到Git仓库

```bash
$ git commit -m "First Git Learn, it's my git learning note."
[master (root-commit) d8ca75e] First Git Learn, it's my git learning note.
 1 file changed, 108 insertions(+)
 create mode 100644 git_learn_notes/Git_Learn_Note.md
```

***"git add & git commit"说明：***

- *git add . 表示将当前目录种的文件都添加到版本库*

- *git add 表示一个中间暂存的状态，可以用git status显示中间状态文件*

- *git commit 的"-m"后面，是本次提交的说明，comment*

- *git commit -m “First Git Learn, it's my git learning note.”和git commit  --message=“First Git Learn, it's my git learning note.”是等价的*

- *git commit -a -m “massage”*

  *-a参数可以将所有已跟踪文件中的执行修改或删除操作的文件都提交到本地仓库，即使它们没有经过git add添加到暂存区。建议不使用-a参数，正常的提交还是使用git add先将要改动的文件添加到暂存区，再用git commit 提交到本地版本库。*

- *git commit --amend //也叫追加提交，它可以在不增加一个新的commit-id的情况下将新修改的代码追加到前一次的commit-id中* <font color='red'>待后面学习</font>

- *git commit命令执行成功后会告诉你*
  
  - *1 file changed：1个文件被改动（我们新添加的学习笔记）*
  - *108 insertions：插入了108行内容（该学习笔记当时108行）*
  
- *<font color="green">关于目录，Git是不进行目录管理的，而是只管理仓库内的文件。git add 可以操作目录，git commit 操作目录会提示"nothing to commit"，如下</font>*

```bash
$ git commit -m "First Git Learn, it's learning notes directory."
On branch master

Initial commit

nothing to commit
```

#### 3.2.2 git status & git diff

可以用来查看接受Git管理的文件的修改状态，以及比较修改内容

- ***git status***
用于查看文件修改的状态，当前Git_Learn_Note.md已经被修改过，我们通过 ***`git status`*** 看看会告诉我们什么？

![git_status_01](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_status_01.png)

***`git status`***命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，Git_Learn_Note.md被修改过了(modified:   Git_Learn_Note.md)，但还没有准备提交的修改(no changes added to commit)。

- ***git diff***
查看具体修改了什么内容：

![git_diff_01](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_diff_01.png)

~~~shell
不同的git diff命令：
(1)git diff //查看尚未暂存的文件更新了哪些部分
(2)git diff filename //查看尚未暂存的某个文件更新了哪些
(3)git diff --cached //查看已经暂存起来的文件和上次提交的版本之间的差异
(4)git diff --cached filename //查看已经暂存起来的某个文件和上次提交的版本之间的差异
(5)git diff head //git diff和git diff --cached的合并
(6)git diff ffd98b291e0caa6c33575c1ef465eae661ce40c9 b8e7b00c02b95b320f14b625663fdecf2d63e74c //查看某两个版本之间的差异
(7)git diff ffd98b291e0caa6c33575c1ef465eae661ce40c9:filename b8e7b00c02b95b320f14b625663fdecf2d63e74c:filename //查看某两个版本的某个文件之间的差异
~~~

#### 3.2.3 git log & git reset & git reflog（版本回退）

版本回退需要根据提交本版的日志情况，确定回退到以前的某个版本。

- ***git log***
在实际工作中，我们肯定记不住每次都改了什么内容，所以我们用***`git log`***命令查看：

```bash
$ git log
commit 0471539bc0556b48a3371101fd98c17aabb0480e (HEAD -> master)
Author: Liujx <liujx@dce.com.cn>
Date:   Wed Jan 13 10:36:10 2021 +0800

    Git Learning note: modified Git_learn_note.md

commit 47fb0e319187d32e1b2796080911f44e6d41a91c
Author: Liujx <liujx@dce.com.cn>
Date:   Wed Jan 13 10:35:19 2021 +0800

    Git Learning note: add images & modified Git_learn_note.md

commit bbd52530c96650b49f27a14b6a09457bb8c528e1
Author: Liujx <liujx@dce.com.cn>
Date:   Wed Jan 13 10:11:10 2021 +0800

    My git learning note, git diff

commit 5284557de44e9f0efc6a932a3a1b81de55dd7bd6
Author: Liujx <liujx@dce.com.cn>
Date:   Mon Jan 11 21:36:09 2021 +0800

    Git learn: add commit status diff

commit d8ca75e78a1c7b06fcadd2bcc4fefdd7a9856c03
Author: Liujx <liujx@dce.com.cn>
Date:   Mon Jan 11 20:38:41 2021 +0800

    First Git Learn, it's my git learning note.
```

***`git log`***命令显示从最近到最远的提交日志，我们可以看到5次提交，最近的一次是 ***Git Learning note: modified Git_learn_note.md***，上一次是 ***Git Learning note: add images & modified Git_learn_note.md***，最早的一次是 ***First Git Learn, it's my git learning note.*** 。

如果有多个文件，想要查看其中某个文件的日志，则可使用：***`git log -- filename`***命令

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上 ***`--pretty=oneline`*** 参数：

```bash
$ git log --pretty=oneline
0471539bc0556b48a3371101fd98c17aabb0480e (HEAD -> master) Git Learning note: modified Git_learn_note.md
47fb0e319187d32e1b2796080911f44e6d41a91c Git Learning note: add images & modified Git_learn_note.md
bbd52530c96650b49f27a14b6a09457bb8c528e1 My git learning note, git diff
5284557de44e9f0efc6a932a3a1b81de55dd7bd6 Git learn: add commit status diff
d8ca75e78a1c7b06fcadd2bcc4fefdd7a9856c03 First Git Learn, it's my git learning note.
```

<font color="green">友情提示:
你看到的一大串类似0471539bc...的是commit_id（版本号），和SVN不一样，Git的commit_id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit_id和我的肯定不一样，以你自己的为准。
为什么commit_id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。SHA散列计算的一个重要特性是不管内容在哪里，它对同样的内容始终产生同样的ID，换言之，在不同目录例甚至不同机器中的相同文件内容产生的SHA1哈希ID是完全相同的。因此，文件的SHA1散列ID是一种有效的全局唯一标识符</font>

相似的命令还有**git show**

<img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210518105948739.png" alt="image-20210518105948739" style="zoom:50%;" />

git show 只能展示最近一次提交的详细信息。另外一种查看方式是 git show-branch --more=10

(--more=10表示额外10个版本)，可以查看修改的comment信息

![image-20210518110249622](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210518110249622.png)

- ***git reset***
版本回退时，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新提交的，上一个版本就是<font color="orange">HEAD\^</font>，上上一个版本就是<font color="orange">HEAD\^\^</font>，当然往上100个版本写100个\^是数不过来的，所以写成<font color="orange">HEAD~100</font>。

***回退上一版本***
为了演示更加清晰，新建一个文件gitversion.txt，然后进行两次修改提交，总共三个版本，内容分别如下（参考git log模式，时间从后往前排列）：
版本3：1st version. 2nd version. 3th version.
版本2：1st version. 2nd version.
版本1：1st version.

```bash
$ git log --pretty=oneline
a766f4ae555cd9a4a8b9e141da582f1a27ef9ab7 (HEAD -> master) modify gitversion.txt 3th
92a45b1e176eaf979f95935a8c657215e367a787 modify gitversion.txt 2nd
8b59c8d2deb541ee00baae115c512ac27c44bef7 add gitversion.txt
```

从上述log内容看，新建了一个文件，并且修改了两次，当前最新版本是a766f4a...，我们要回退到上一版本92a45b1...，可以通过如下操作执行：

```bash
$ git reset --hard HEAD^
HEAD is now at 92a45b1 modify gitversion.txt 2nd

$ cat gitversion.txt
1st version. 2nd version.

$ git log --pretty=oneline
92a45b1e176eaf979f95935a8c657215e367a787 (HEAD -> master) modify gitversion.txt 2nd
8b59c8d2deb541ee00baae115c512ac27c44bef7 add gitversion.txt
```

通过上述操作看到，果然回退到上一个版本了，并且通过 ***`git log`*** 看到当前最新版本的commit_id已经是92a45b1...了。

***回退任意版本***

但是，又想回到之前的最后一个版本a766f4a...怎么办？
只要窗口没关掉，或者你能通过任何方法找到版本的commit_id，就可以通过下面的方式，回到某个具体版本。
*<u>版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。</u>*

```bash
$ git reset --hard a766f4a
HEAD is now at a766f4a modify gitversion.txt 3th

$ cat gitversion.txt
1st version. 2nd version. 3th version.

$ git log --pretty=oneline
a766f4ae555cd9a4a8b9e141da582f1a27ef9ab7 (HEAD -> master) modify gitversion.txt 3th
92a45b1e176eaf979f95935a8c657215e367a787 modify gitversion.txt 2nd
8b59c8d2deb541ee00baae115c512ac27c44bef7 add gitversion.txt
```

- ***git reflog***

上述提到的“只要窗口没关掉”，目的是为了找到某个版本的commit_id，只要能找到这个commit_id，窗口关掉几次都没关系，一样可以回退。但是窗口关掉之后，如何找到commit_id呢？

```bash
$ git reflog
a766f4a (HEAD -> master) HEAD@{0}: reset: moving to a766f4a
92a45b1 HEAD@{1}: reset: moving to HEAD^
a766f4a (HEAD -> master) HEAD@{2}: commit: modify gitversion.txt 3th
92a45b1 HEAD@{3}: commit: modify gitversion.txt 2nd
8b59c8d HEAD@{4}: commit: add gitversion.txt
```

Git提供了一个命令 ***`git reflog`*** 用来记录你每一次执行的命令，有了这个，放心回退吧。

- ***git版本回退原理***

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向到某个版本：

┌────┐
│HEAD│
└────┘
   └──> ○ modify gitversion.txt 3th
　　　│
　　　○ modify gitversion.txt 2nd
　　　│
　　　○ add gitversion.txt

改为指向 modify gitversion.txt 2nd：

┌────┐
│HEAD│
└────┘
   │　　○ append GPL
   │　　│
   └──> ○ add distributed
　　　│
　　　○ wrote a readme file

然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

引申：如果文件只是被git add 了，但是没有commit，且执行了git reset --hard，此时git add 的版本将不复存在，想要恢复回来，需要执行如下操作：

~~~bash
git fsck --lost-found
~~~

执行完以后，会在**`.git/lost-found/other`**路径下找到git add，但是被版本回退弄丢的版本。逐个打开可以查看到具体内容。

另外，如果没有git add，就找不回来了。

由此想到，如果某个文件git add了，想要清楚git add的内容，那么可以用**`git reset HEAD`**(回退到当前版本)来取消git add（不用--hard可以起到回退的效果，且不动工作区）

**<font color='red'>git reset --hard一定要慎用！！！</font>**

git reset （--mixed）commit_id //将commit的部分回退到commit_id对应版本；覆盖暂存区，不覆盖工作区。回退后和回退前版本的差异是放在工作区的。

//mixed可选，不写也是一样的

git reset --hard commit_id  //恢复至commit_id版本的同时，覆盖暂存区和工作区。

git reset --soft commit_id  //只是将commit的部分回退到commit_id对应版本；不动暂存区和工作区。回退后的版本和回退前版本的差异是放在暂存区的。

#### 3.2.4 工作区 & 暂存区

- **工作区（Working Directory）**
就是在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：

```bash
$ cd /z/Git/learngit
$ ll
total 0
drwxr-xr-x 1 lenovo 197121 0  1月 13 14:59 git_learn_notes/

$ cd git_learn_notes
$ ll
total 17
-rw-r--r-- 1 lenovo 197121 14170  1月 13 16:18 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121    40  1月 13 14:59 gitversion.txt
drwxr-xr-x 1 lenovo 197121     0  1月 13 10:42 image/
```

- **版本库（Repository）& 暂存区（stage）**

工作区有一个隐藏目录 *.git*，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
（分支和HEAD的概念后面再说）

![git_repository](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_repository.png)

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用 ***`git add`*** 把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用 ***`git commit`*** 提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，***`git commit`*** 就是往master分支上提交更改。
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

我们再练习一遍，先对gitversion.txt做个修改，比如加上一行内容：

```txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
```

然后，在工作区新增一个git_test.txt文本文件（内容随便写）。

先用git status查看一下状态：

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git_test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git非常清楚地告诉我们，gitversion.txt被修改了，而git_test.txt还从来没有被添加过，所以它的状态是Untracked。

现在，使用两次命令 ***`git add`***，把gitversion.txt和git_test.txt都添加后，用git status再查看一下：

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   git_test.txt
        modified:   gitversion.txt
```

现在，暂存区的状态就变成这样了：

![git_stage](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_stage.png)

所以，***`git add`*** 命令实际上就是把要提交的所有修改放到 **暂存区（Stage）**，然后，执行 ***`git commit`*** 就可以一次性把暂存区的所有修改提交到分支。

```bash
$ git commit -m "Git learn: stage"
[master 4af1b44] Git learn: stage
 2 files changed, 1 insertion(+)
 create mode 100644 git_learn_notes/git_test.txt
```

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

现在版本库变成了这样，暂存区就没有任何内容了：

![git_stage_after_commit](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_stage_after_commit.png)

#### 3.2.5 管理修改而非文件

**问：为什么Git比其他版本控制系统设计得优秀？**
**答：因为Git跟踪并管理的是<font color="red">修改</font>，而非文件。任何增删改，都是修改**

我们做一个实验，看看Git是如何管理修改，而不是管理文件的。

第一步，对gitversion.txt添加一行(Git tracks changes.)：

```txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
```

第二步，***`git add`*** 将第一次修改放入暂存区

```bash
$ git add gitversion.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   gitversion.txt
```

第三步，再次修改gitversion.txt，再添加一行(Git tracks changes of files 2nd.)

```txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

第四步，***`git commit`***，然后 ***`git status`*** 再看状态

```bash
$ git commit -m "Git test: git tracks changes"
[master 652163d] Git test: git tracks changes
 1 file changed, 2 insertions(+), 1 deletion(-)

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

至此，你会发现，**第二次修改没有被提交！第二次修改没有被提交！第二次修改没有被提交！**

原因如下：
第一次修改 -> ***`git add`*** -> 第二次修改 -> ***`git commit`***

你看，前面提到了Git管理的是修改，当使用 ***`git add`*** 命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，***`git commit`*** 只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用 ***`git diff`*** 命令可以查看工作区和版本库里面最新版本的区别，可见，第二次修改确实没有被提交。

```bash
$ git diff
diff --git a/git_learn_notes/gitversion.txt b/git_learn_notes/gitversion.txt
index 42b2849..fd43f3f 100644
--- a/git_learn_notes/gitversion.txt
+++ b/git_learn_notes/gitversion.txt
@@ -1,3 +1,4 @@
 1st version. 2nd version. 3th version.
 Git has a mutable index called stage.
-Git tracks changes.
\ No newline at end of file
+Git tracks changes.
+Git tracks changes of files 2nd.
\ No newline at end of file
```

#### 3.2.6 撤销修改 git restore

撤销修改分为两类

1. 撤销 ***`git add`*** 之前的修改内容
2. 撤销 ***`git add`*** 之后，还未 ***`git commit`*** 的修改内容

- **git add 之前 撤销**

先对gitversion.txt进行修改，添加一行"Git undo change before add."。

```bash
$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git undo change before add.
```

通过 ***`git status`*** 查看当前状态

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

我们会发现，Git告诉我们，***`git restore <filename>...`*** 可以丢弃工作区的修改，尝试一下：

```bash
$ git restore gitversion.txt

$ git status
On branch master
nothing to commit, working tree clean

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

命令 ***`git restore gitversion.txt`*** 意思就是，把gitversion.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是gitversion.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是gitversion.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次 ***`git commit`*** 或 ***`git add`*** 时的状态。
从上述输出看，文件内容果然复原了。

- **git add 之后 撤销**

如果修改后执行了 ***`git add`*** 怎么办？我们再来操作一下。
先添加一句话"Git undo change after add."，再执行 ***`git add`***；
执行 ***`git commit`*** 之前，我们发现这句话错了，***`git status`***看一下，发现修改只是添加到暂存区，还未提交。

```bash
$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git undo change after add.

$ git add gitversion.txt

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   gitversion.txt
```

我们发现，Git同样告诉我们，用命令 ***`git restore --staged <file>...`*** 可以把暂存区的修改撤销掉（unstage），重新放回工作区，我们尝试一下：

```bash
$ git restore --staged gitversion.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git undo change after add.
```

我们可以看到，暂存区干净了，工作区还存在文件修改，查看一下文件内容，"Git undo change after add."这句不该存在的内容确实还在。

接下来呢，按照“撤销 ***`git add`*** 之前的修改”在操作一次就行了。

```bash
$ git restore gitversion.txt

$ git status
On branch master
nothing to commit, working tree clean

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

到这里，全干净了，***`git status`***什么也没有了，查看文件内容，"Git undo change after add."这句确实不存在了，一切都回到了原点。

撤销修改，除了使用 ***`git restore`*** 之外，还可以使用 ***`git checkout -- <filename>`*** 命令，该命令此处不做详细介绍。

**<font color='red'>总结：</font>**

~~~
没git add 的时候，撤销修改：git restore gitversion.txt //撤销的是工作区的部分

已经git add了，撤销修改：git restore --staged gitversion.txt、git restore gitversion.txt //先把add的退回到未add的状态，然后再撤销就可以了。
~~~

#### 3.2.7 删除文件 git rm&重命名文件 git mv

Git中，删除也被当做一种修改操作来管理

~~~bash
rm git_test.txt
~~~

此时，Git知道有文件被删除了，工作区和版本库不一致了，***`git status`***命令会告诉哪些文件被删除了。

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    git_test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

此时可以有两个选择

1. 一是删除错了，要从版本库恢复回来，使用命令 ***`git restore git_test.txt`***
通过以下执行，可以看到，"git_test.txt"被恢复回来了，***`git status`*** 也是干净的。

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

2. 二是确实要从版本库中删除该文件，使用命令 ***`git rm git_test.txt `***  删掉，并且 ***`git commit`***
通过以下执行，可以看到，"git_test.txt"已经不存在了，并且 ***`git status`*** 也是干净的。

**引申：文件重命名**

~~~
git mv 和直接mv区别
一、git mv
行为：
　　1.创建一个和之前文件内容一样的文件，文件名为新的文件名
　　2.将原来的文件删除
　　3.将删除的文件添加到暂存区
　　4.将新建的文件添加到暂存区
提交：
　　直接 git commit -m ''
恢复：
　　1. 恢复暂存区（git reset HEAD oldName）
　　2. 将新添加的文件从暂存区移除（git reset HEAD newName）
　　3. 将原来的文件从暂存区恢复到工作区（git checkout -- oldName）
　　4. 从工作区删除新添加的这个文件（rm newName）
二、直接调用系统的mv
行为：
　　只是重命名了一个文件
提交：
　　1.把新文件和旧文件加入暂存区 git add
　　2.提交暂存区的改动　　git commit
恢复：
　　1.将旧文件恢复到工作区，git checkout -- oldName
　　2.将新文件删除， rm newName
~~~

总结：使用系统命令，需要执行git add后再执行git commit；

​            使用git命令进行重命名和删除操作，可以直接git commit

- 将一个文件由已暂存的转化成未暂存的

~~~bash
$ git rm --cached filename
~~~

## 四、远程版本库

GitHub也可以创建Git仓库，并且让GitHub与本地仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作。

### 4.1 添加到远程仓库 git remote & git push

首先，注册并登录GitHub，创建一个仓库。我针对Git学习，创建一个叫做learngit的仓库。创建后，仓库是空的。

GitHub给出了很明确的提示，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

GitHub提示信息如下：

![GitHub_new_repo](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/GitHub_new_repo.png)

现在，根据GitHub的提示，在本地的learngit仓库下运行命令：

```bash
$ git remote add origin http://github.com/liujixia0410/learngit.git
```

上面的liujixia0410需要替换成自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

<font color='red'>如果url地址写错了怎么办</font>

可以通过如下命令取消

~~~bash
$ git remote rm origin
~~~

通过如下命令可以查看远程库的地址（删除后可以执行这个查看一下，结果为空就是对的）

~~~bash
$ git remote -v
~~~

下一步，就可以把本地库的所有内容推送到远程库上：

```bash
$ git push -u origin master
warning: redirecting to https://github.com/liujixia0410/learngit.git/
Enumerating objects: 79, done.
Counting objects: 100% (79/79), done.
Delta compression using up to 8 threads
Compressing objects: 100% (55/55), done.
Writing objects: 100% (79/79), 193.28 KiB | 7.73 MiB/s, done.
Total 79 (delta 16), reused 0 (delta 0)
remote: Resolving deltas: 100% (16/16), done.
To http://github.com/liujixia0410/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

把本地库的内容推送到远程，用 ***`git push`*** 命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后的Git页面，与本地一样了。

```bash
$ ll
total 33
-rw-r--r-- 1 lenovo 197121 26672  1月 22 15:07 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121   132  1月 19 19:32 gitversion.txt
drwxr-xr-x 1 lenovo 197121     0  1月 13 16:50 image/
```

![GitHub_push_01](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/GitHub_push_01.png)

从现在起，只要本地作了提交，就可以通过命令 ***`git push`*** 推送到GitHub上，现在就是真正的分布式版本库了。

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Git_Learn_Note.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git add Git_Learn_Note.md

$ git commit -m "Git learn: git push"
[master 8f497b1] Git learn: git push
 1 file changed, 82 insertions(+)

$ git push origin master
warning: redirecting to https://github.com/liujixia0410/learngit.git/
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 2.30 KiB | 336.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To http://github.com/liujixia0410/learngit.git
   3fb1270..8f497b1  master -> master

$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

### 4.2 从远程仓库克隆 git clone

现在，假设我们先有一个远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库，名字叫gitremotetest，勾选

```
Initialize this repository with a README
```

这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件。

-----------------------

------------



<font color='red'>使用SSH做clone之前需要这样做</font>

克隆之前，需要先生成SHH KEY。步骤如下：

~~~bash
//查看一下是否生成了id_rsa文件，如果没有说明没有生成ssh key
$ cd ~/.ssh
//如果没有生成ssh key，需要执行如下命令生成ssh key
$ ssh-keygen -t rsa -C "manan0611"
~~~

![image-20210519144707947](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210519144707947.png)

可以看到提示路径：/c/Users/Lenovo/.ssh/id_rsa

打开这个路径下的id_rsa.pub文件，复制其中的ssh key

打开github，个人>>settings>>SSH and GPG keys 点击 New SSH key ，起个名，把复制的ssh key命令粘上去就可以了。

----------------------------

----------------



现在，远程库已经准备好了，使用命令 ***`git clone`*** 克隆一个本地库。

```bash
$ ll
total 57
-rwxr-xr-x 1 lenovo 197121  5114 12月 14 19:57 github.sh*
drwxr-xr-x 1 lenovo 197121     0  1月 11 20:32 learngit/

$ git clone git@github.com:liujixia0410/gitremotetest.git
Cloning into 'gitremotetest'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.

//如果路径下有多个分支，可以用如下命令克隆某个分支（如master分支）
$ git clone -b master git@github.com:liujixia0410/gitremotetest.git

$ ll
total 57
-rwxr-xr-x 1 lenovo 197121  5114 12月 14 19:57 github.sh*
drwxr-xr-x 1 lenovo 197121     0  1月 23 22:27 gitremotetest/
drwxr-xr-x 1 lenovo 197121     0  1月 11 20:32 learngit/
```

GitHub给出的地址不止一个，还可以用 https://github.com/liujixia0410/gitremotetest.git 这样的地址。实际上，Git支持多种协议，默认的 git:// 使用ssh，但也可以使用https等其他协议。

使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

说明：克隆下来的库，可以看出它是和远程端建立了链接的，可以通过git push origin main的命令来上传更新

![image-20210519150751193](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210519150751193.png)

### 4.3 从远端拉取 git pull

【git clone 和 git pull 相同点】：都是从远程服务器拉取代码到本地

【git clone 和 git pull 不同点】：

git clone
是在本地没有版本库的时候，从远程服务器克隆整个版本库到本地，是一个本地从无到有的过程。

git pull
在本地有版本库的情况下，从远程库获取最新commit 数据（如果有的话），并merge（合并）到本地。

git pull = git fetch + git merge

举例：

将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。

```bash
git pull origin master:brantest
```

如果远程分支是与当前分支合并，则冒号后面的部分可以省略。

~~~bash
git pull origin master
~~~

【使用场景】
通常情况下，远程操作的第一步，是使用git clone从远程主机克隆一个版本库到本地。

本地修改代码后，每次从本地仓库push到远程仓库之前都要先进行git pull操作，保证push到远程仓库时没有版本冲突。

## 五、分支管理

### 5.1 创建与合并分支

在版本回退里，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。

截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点，比如下图：

![git_branch_init](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_init.png)

每次提交，master分支都会向前移动一步，这样，随着不断提交，master分支的线也越来越长。

当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上。

![git_branch_create](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_create.png)

Git创建一个分支很快的原因就在这，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化。

不过，从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变。

![git_branch_brlearn](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_brlearn.png)

假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并。

![git_branch_merge](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_merge.png)

所以Git合并分支也很快，就改改指针，工作区内容也不变。

合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支。

![git_branch_rm](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_rm.png)

到这，通过分支dev的一系列操作和提交，都全部合并到master了，但是我们都看不出来曾经有过一个dev分支。

下面，具体操作一次。

#### 5.1.1 创建和切换分支 git branch & git checkout

我们先创建并且换到一个新的分支上，分支命名"brlearn"（对应上文描述原理中的dev）。

```bash
$ git checkout -b brlearn //创建并切换至新的分支
Switched to a new branch 'brlearn'

$ git branch  //列出所有分支，当前分支前面标注*号
* brlearn
  master
```

***`git checkout`*** 命令加上 ***`-b`*** 参数表示创建并切换，相当于以下两条命令。

```bash
$ git branch brlearn //创建分支
$ git checkout brlearn //切换到某个分支
Switched to a new branch 'brlearn'

$ git branch  //列出所有分支，当前分支前面标注*号
* brlearn
  master
```

现在已经在 *brlearn* 分支上了，我们在"gitversion.txt"里增加一行"Git branch brlearn add 1st."。然后提交，看看 *brlearn* 分支与 *master* 的区别。

```bash
$ git branch
* brlearn
  master

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git branch brlearn add 1st.

$ git status
On branch brlearn
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add gitversion.txt

$ git commit -m "Git learn: git branch brlearn"
[brlearn cf09a3c] Git learn: git branch brlearn
 1 file changed, 2 insertions(+), 1 deletion(-)

$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

$ git branch
  brlearn
* master

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

切换回 *master* 分支后，发现"gitversion.txt"刚才添加的内容不见了！因为那个提交是在 *brlearn* 分支上，而 *master* 分支此刻的提交点并没有变。

![git_branch_on_master](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_on_master.png)

#### 5.1.2 合并 git merge

现在我们把 *brlearn* 分支合并回 *master* ，使用 ***`git merge`*** 命令。

```bash
$ git branch
  brlearn
* master

$ git merge brlearn
Updating 946c07b..cf09a3c
Fast-forward
 git_learn_notes/gitversion.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git branch brlearn add 1st.
```

***`git merge`*** 命令用于合并指定分支到当前分支。合并后，再查看`gitversion.txt`的内容，就可以看到，和*`brlearn`* 分支是一样的了。

另外，我们注意上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把 *`master`* 指向 *`brlearn`* 的当前提交，所以合并速度非常快。

当然，也不是每次合并都能`Fast-forward`，我们后面会讲其他方式的合并。

合并完成后，就可以放心地删除 *`brlearn`* 分支了，删除后，查看 *`branch`*，就只剩下 *`master`* 分支了。如下：

```bash
$ git branch -d brlearn
Deleted branch brlearn (was cf09a3c).

$ git branch
* master
```

因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在 *`master`* 分支上工作效果是一样的，但过程更安全。

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

说明：

如果dev做了修改提交，master没有做修改提交，那么此时做merge操作将master合并到dev上，不会发生任何变化。也就是说不会覆盖dev的提交。

如果master做了修改，没有add，或者只add但没有commit，则此部分合并时不会合并到其他分支上

如果工作区有修改，或者dev分支的暂存区有修改，将master分支合并到dev分支上，不会对工作区和dev分支的暂存区做任何改动。

总结：

合并的是已提交的内容，合并的根本是移动HEAD指针，所以未修改的分支不会通过合并操作覆盖掉修改的分支。

#### 5.1.3 切换分支 git switch

我们注意到切换分支使用 ***`git checkout <branch>`***，而前面讲过，撤销修改也可以使用 ***`git checkout -- <file>`***，同一个命令，有两种作用，确实很容易搞混。

实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的 ***`git switch`*** 命令来切换分支。（***`git switch`*** 确实比 ***`git checkout`*** 更容易理解）

创建并切换到新的 *`brlearn`* 分支：

```bash
$ git switch -c brlearn
Switched to a new branch 'brlearn'

$ git branch
* brlearn
  master
```

直接切换到已有的`master`分支：

```bash
$ git switch master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

$ git branch
  brlearn
* master
```

### 5.2 解决冲突（人工合并）

分支合并时，如果两个分支修改了同一个文件，可能会存在文件合并冲突，在这种情况下，Git不能使用“快速合并”，会提示需要解决冲突才可以合并。

我们新建一个分支，尝试一下。

首先，新建并切换至新的分支`brconflict`，并在该分支下修改“gitversion.txt”文件的最后一行内容，并提交（最后一行结尾处增加“modify by brconflict”）。

```bash
$ git switch -c brconflict
Switched to a new branch 'brconflict'

$ git branch
* brconflict
  master

$ vi gitversion.txt
Git tracks changes of files 2nd modify by brconflict.

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd modify by brconflict.

$ git add gitversion.txt

$ git commit -m "Git learn: git merge brconflict"
[brconflict 1ba9b5c] Git learn: git merge brconflict
 1 file changed, 1 insertion(+), 1 deletion(-)
```

然后，我们切换回`master`分支，也修改该文件的最后一行，并提交（最后一行结尾处增加“modify by master”）。

```bash
$ git switch master
Switched to branch 'master'

$ git branch
  brconflict
* master

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.

$ vi gitversion.txt
Git tracks changes of files 2nd modify by master.

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd modify by master.

$ git add gitversion.txt

$ git commit -m "Git learn: git merge master"
[master 1f0e9a1] Git learn: git merge master
 1 file changed, 1 insertion(+), 1 deletion(-)
```

现在，`brconflict`分支和`master`分支都有了各自提交的内容，就像下图这样了。

![git_conflict](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_conflict.png)

这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，我们试试看。

```bash
$ git merge brconflict
Auto-merging git_learn_notes/gitversion.txt
CONFLICT (content): Merge conflict in git_learn_notes/gitversion.txt
Automatic merge failed; fix conflicts and then commit the result.
```

果然冲突了`Automatic merge failed; fix conflicts and then commit the result.`！

Git告诉我们，文件存在冲突，必须手动解决冲突后再提交。`git status`也可以告诉我们冲突的文件。

```bash
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

在这种情况下，我们可以直接查看“gitversion.txt”文件，能够看到冲突的具体内容。

```bash
$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
<<<<<<< HEAD
Git tracks changes of files 2nd modify by master.
=======
Git tracks changes of files 2nd modify by brconflict.
>>>>>>> brconflict
```

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们可以直接通过 ***`vi`*** 进行修改，也就是手工解决冲突，修改后就可以正常提交了。

```bash
$ vi gitversion.txt
Git tracks changes of files 2nd modify by master and brconflict.

$ git add gitversion.txt

$ git commit -m "Git learn: fix conflict"
[master 7f87757] Git learn: fix conflict

$ git status
On branch master
nothing to commit, working tree clean
```

至此，`brconflict`分支和`master`分支的冲突已经被我们手工解决掉了，内容也已经提交到`master`分支上，两个分支的关系如下图：

![git_fix_conflict](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_fix_conflict.png)

通过带参数的 ***`git log --graph`*** 可以看到日志对于分支合并的记录情况。之后删除 `brconflict` 分支即可，工作完成。

```bash
$ git log --graph --pretty=oneline --abbrev-commit
*   7f87757 (HEAD -> master) Git learn: fix conflict
|\
| * 1ba9b5c (brconflict) Git learn: git merge brconflict
* | 1f0e9a1 Git learn: git merge master
|/
* a9e4065 Git learn: gitee
* 9054985 Delete git_learn_notes/image directory
......

$ git branch -d brconflict
Deleted branch brconflict (was 1ba9b5c).

$ git branch
* master
```

### 5.3 分支策略 git merge --no-ff

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

我们具体操作一下，禁用 `Fast forward` 模式，是在 ***`git merge`*** 的时候加上参数 ***`--no-ff`*** 。

首先，仍然创建并切换 `brnoff` 分支：

```bash
$ git switch -c brnoff
Switched to a new branch 'brnoff'

$ git branch
* brnoff
  master
```

修改"gitversion.txt"文件（增加一行"Git merge no fast forward."），并提交一个新的commit。

```bash
$ git switch -c brnoff
Switched to a new branch 'brnoff'

$ git branch
* brnoff
  master

$ vi gitversion.txt
Git merge no fast forward.

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd modify by master and brconflict.
Git merge no fast forward.

$ git add gitversion.txt

$ git commit -m "Git learn: add merge no ff"
[brnoff b52772d] Git learn: add merge no ff
 1 file changed, 1 insertion(+)
```

然后，我们切换回 `master` 分支，通过 ***`--no-ff`*** 参数合并 `brnoff` 分支。

因为本次合并要创建一个新的commit，所以加上 ***`-m`*** 参数，把commit描述写进去。

```
$ git switch master
Switched to branch 'master'

$ git branch
  brnoff
* master

$ git merge --no-ff -m "Git learn: merge with --no-ff parameter" brnoff
Merge made by the 'recursive' strategy.
 git_learn_notes/gitversion.txt | 1 +
 1 file changed, 1 insertion(+)
```

合并后，我们用 ***`git log --graph`*** 看看分支历史，不使用`Fast forward`模式，merge后就像这样。

```
$ git log --graph --pretty=oneline --abbrev-commit
*   6944519 (HEAD -> master) Git learn: merge with --no-ff parameter
|\
| * b52772d (brnoff) Git learn: add merge no ff
|/
*   7f87757 Git learn: fix conflict
|\
| * 1ba9b5c Git learn: git merge brconflict
* | 1f0e9a1 Git learn: git merge master
|/
* a9e4065 Git learn: gitee
* 9054985 Delete git_learn_notes/image directory
* cdd0ce7 Upload by PicGo
......
```

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

- <font color="red">**分支策略说明**</font>

<font color="red">在实际开发中，我们应该按照几个基本原则进行分支管理：</font>

<font color="red">1、`master` 分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；</font>

<font color="red">2、干活都在 `dev` 分支上，也就是说 `dev` 分支是不稳定的，在版本发布时，再把 `dev` 分支合并到 `master` 上，在 `master` 分支发布1.0版本；</font>

<font color="red">3、团队每个人都在 `dev` 分支上干活，每个人都应该有一个自己的分支，比如 `devfrank`、`devtony` 等，时不时地往 `dev` 分支上合并就可以了。</font>

<font color="red">所以，团队合作的分支看起来就像这样：</font>

![git_branch_strategy](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/git_branch_strategy.png)

### 5.4 bug分支管理

#### 5.4.1 通过bug分支修复缺陷 git stash

软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，分支的强大管理应用，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

比如，现在有一个新的bug需要修复，bug代号001。我们创建一个分支 `issue-101` 来修复它，但是，等等，当前正在 `brdev` 上进行的工作还没有提交。

首先，master内容如下：

```bash
$ cat gitversion.txt
This is a gitversion.txt for learngit.
```

`brdev` 分支上已进行的、还未提交的工作内容，如下（通过 ***`git status`*** 也可以看到这两个未提交的文件状态）：

```bash
$ cat gittest.txt
This is a new file.

$ cat gitversion.txt
This is a gitversion.txt for learngit.
Branch brdev's modify.......

$ git status
On branch brdev
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   gittest.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt
```

根据以上对比，可以看到，`brdev` 分支比 `master` 分支多了一个"gittest.txt"文件，以及"gitversion.txt"比 `master` 分支多了一行"Branch brdev's modify....."，很明显，`brdev` 分支还没完成工作，暂时还不能提交。

但是 `master` 分支的缺陷修改不能等，必须马上修改，怎么办？

Git的强大也再次体现，Git提供了一个 ***`git stash`*** 功能，可以把当前工作现场<font color='red'>**保存**</font>起来，等以后恢复现场后继续工作。

并且用 ***`git status`*** 查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。如下：

```bash
$ git stash
Saved working directory and index state WIP on brdev: 4615a5f Git learn: rewirte gitversion.txt

$ git branch
* brdev
  master

$ git status
On branch brdev
nothing to commit, working tree clean
```

现在我们开始修改 `master` 分支上的bug。

首先，创建bug修复的分支，要修复哪个分支的bug，就在哪个分支上创建新的bug修复分支。这里我们通过 `master` 分支创建一个 `brissue-001` 的分支。

```bash
$ git switch master
Switched to branch 'master'

$ git switch -c brissue-001
Switched to a new branch 'brissue-001'

$ git branch
  brdev
* brissue-001
  master
```

现在我们已经创建了 `brissue-001` 分支，并且切换到该分支，开始修复bug，把"This is a gitversion.txt for learngit."改为"This is a gitversion.txt."，并完成提交。

```bash
$ cat gitversion.txt
This is a gitversion.txt for learngit.

$ vi gitversion.txt
This is a gitversion.txt.

$ git status
On branch brissue-001
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add gitversion.txt

$ git commit -m "Git learn: fix issue-001"
[brissue-001 10baade] Git learn: fix issue-001
 1 file changed, 1 insertion(+), 1 deletion(-)
```

修复完成后，切换到 `master` 分支，完成合并，删除 `brissue-001` 分支。如下：

```bash
$ git switch master
Switched to branch 'master'

$ git branch
  brdev
  brissue-001
* master

$ git merge --no-ff -m "Git learn: merged fix issue-001" brissue-001
Merge made by the 'recursive' strategy.
 git_learn_notes/gitversion.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

$ git branch -d brissue-001
Deleted branch brissue-001 (was 10baade).

$ git branch
  brdev
* master

$ git status
On branch master
nothing to commit, working tree clean
```

至此，bug修复工作完成了。

但是，回看工作区，***`git status`*** 好干净啊，啥也没有了。我们之前提到的<font color='red'>**保存工作现场**</font>哪儿去了呢？通过 ***`git stash list`*** 看一下：

```bash
$ git stash list
stash@{0}: WIP on brdev: 4615a5f Git learn: rewirte gitversion.txt
```

我们看到，工作现场确实被保存了起来，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

1、用 ***`git stash apply`*** 恢复，但是恢复后，stash内容并不删除，你需要用 ***`git stash drop`*** 来删除；

2、用 ***`git stash pop`***，恢复的同时把stash内容也删了。

无论用哪种方法，stash内容被删除后，***`git stash list`*** 就干净了，什么都没了。

```bash
$ git stash pop
On branch brdev
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   gittest.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

Dropped refs/stash@{0} (4615a5fa69b189adfbe8e71d9ddb5604838d1c96)

$ git stash list

```

特别说明：

git stash不针对特定的分支，切换分支后，stash内容不变，所以弹出时要小心；

git stash pop或者drop后，stash的序号会自动改变，连续弹出时要注意。

#### 5.4.2 将master分支的修复，merge到其他dev分支 git cherry-pick

通过以上操作，在 `master` 分支上修复了bug。但是，`brdev` 分支是早期从 `master` 分支分出来的，所以，这个bug其实在当前 `brdev` 分支上也存在。

那怎么在 `brdev` 分支上修复同样的bug？重复操作一次，提交？肯定没问题。但是，可不可以不重复操作？可以。

同样的bug，要在 `brdev` 上修复，我们只需要把 `10baade Git learn: fix issue-001` 这个提交所做的修改“复制”到 `brdev` 分支。注意：我们只想复制 `10baade Git learn: fix issue-001` 这个提交所做的修改，并不是把整个master分支merge过来。

因此，Git专门提供了一个 ***`git cherry-pick`*** 命令，让我们能复制一个特定的提交到当前分支。

```bash
$ git cherry-pick 10baade
error: your local changes would be overwritten by cherry-pick.
hint: commit your changes or stash them to proceed.
fatal: cherry-pick failed
```

我们发现，***`git cherry-pick`*** 命令执行报错了。根据提示"hint"可以看到，Git虽然可以将某个提交所做的修改合并进来，但是需要本地先把未commit的内容全部commit之后才可以。

我们把 `brdev` 分支的内容编写完成之后，先提交，再把 `10baade Git learn: fix issue-001` 这个提交合并进来，我们试一下。

```bash
$ git cherry-pick 10baade
Auto-merging git_learn_notes/gitversion.txt
CONFLICT (content): Merge conflict in git_learn_notes/gitversion.txt
error: could not apply 10baade... Git learn: fix issue-001
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <paths>' or 'git rm <paths>'
hint: and commit the result with 'git commit'

$ vi gitversion.txt

$ git add gitversion.txt

$ git commit -m "Git learn: cherry-pick"
[brdev d893b6d] Git learn: cherry-pick
 Date: Fri Feb 5 14:12:08 2021 +0800
 1 file changed, 1 insertion(+), 1 deletion(-)
```

***`git cherry-pick`*** 命令给出了一个提示，需要解决冲突，我们按照之前章节提到的方式，***`vi`*** 人工解决冲突，然后提交，合并完成。

说明：***`git cherry-pick`*** 为什么没能直接自动合并成功，目前未找到原因，以后学习过程中再逐渐明确。

### 5.5 feature分支管理

软件开发过程中，经常会有需求变更，经常会随时加入新功能，而且有些功能是具有实验性质的（比如DCE清算7.0一阶段中，把数字类型从BigDecimal改为double，未来是否一定要应用，不确定）。

这类实验性质的功能，任何开发团队都不愿意让其影响主分支。

所以，对于新功能开发，最好新建feature分支，在这上面开发，合并，然后删除分支。

这里，不再做什么操作试验了，没有什么新的命令可学，整个过程就是熟练使用之前章节学到的内容，比如建立和切换分支 ***`git switch -c <branchname>`***、合并分支 ***`git merge --no-ff`***、删除分支 ***`git branch -d <branchname>`*** 等操作。

只是在删除分支过程中，可能会出现一种情况，就是某个实验性功能最终决定不要了，白干了，这时候该分支没有经过merge，Git为防止误删除，会给出一个非常明确的提示：分支没有合并，删除失败。并且很明确的告诉我们，如果确定要删除，参数改为 ***`-D`*** 可以强行删除。

```bash
$ git branch -d feature-double
error: The branch 'feature-double' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-double'.
```



## 六、Gitee学习

如果国内访问GitHub比较慢，可以改用Gitee作为远程仓库。

首先我们可以在Gitee上建立一个仓库，可以与本地仓库同名，以便把本地仓库与远程仓库关联起来。

### 6.1 Gitee仓库建立与SSH公钥

#### 6.1.1 Gitee添加SSH公钥

注册并登录Gitee，与GitHub一样，先上传自己的SSH公钥。Gitee SSH公钥添加页面截图如下：

![Gitee_SSHKey](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/Gitee_SSHKey.jpg)

本地Git获取SSH公钥，如下：

Gitee 提供了基于SSH协议的Git服务，在使用SSH协议访问仓库仓库之前，需要先配置好账户/仓库的SSH公钥。

你可以按如下命令来生成 sshkey:

```bash
$ ssh-keygen -t rsa -C "xxxx@xxxx.com"  
# Generating public/private rsa key pair...
```

> 注意：这里的 `xxxxx@xxxxx.com` 只是生成的 sshkey 的名称，并不约束或要求具体命名为某个邮箱。
> 很多教程均讲解的使用邮箱生成，其一开始的初衷仅仅是为了便于辨识所以使用了邮箱。

按照提示完成三次回车，即可生成 ssh key。通过查看 `~/.ssh/id_rsa.pub` 文件内容，获取到自己的 public key。

```
$ cat /c/Users/lenovo/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxThU= liujixia0410@163.com
```

> 以上public key是我个人的，在本文中使用`xxxxxxxxxxxxxxxxx`隐藏了。

复制生成后的 ssh key，添加到上面截图显示的公钥文本框内即可。

#### 6.1.2 Gitee仓库建立并与本地关联

![Gitee_create_repo](https://gitee.com/liujixia0410/picbed/raw/master/gitlearn/Gitee_create_repo.png)

然后，我们在本地库使用命令 ***`git remote add`*** 把本地库与Gitee远程库关联起来。

git remote add lemontree git@gitee.com:manan0611/learnnote.git

```bash
$ git remote add origin git@gitee.com:liujixia0410/learngit.git
fatal: remote origin already exists.
```

我们发现，执行错误，原因是之前我们本地的git仓库已经与GitHub建立了远程关联，名字也叫origin。我们通过 ***`git remote -v`*** 查看一下，然后可以删除这个远程库，再重新关联。

```
$ git remote -v
origin  git@github.com:liujixia0410/learngit.git (fetch)
origin  git@github.com:liujixia0410/learngit.git (push)

$ git remote rm origin

$ git remote add origin git@gitee.com:liujixia0410/learngit.git
```

此时，我们本地库与Gitee远程库已经建立了关联，可以继续使用 ***`git push`*** 进行上传推送了。

## 附录

### Q&A

- ***不在Git仓库管理目录内执行***
  - Q：输入**git add Git_Learn_Note.md**，得到错误：fatal: not a git repository (or any of the parent directories)。
  - A：Git命令必须在Git仓库目录内执行（**git init**除外），在仓库目录外执行是没有意义的。
- ***文件不存在***
  - Q：输入**git add Git_Learn_Note.md**，得到错误fatal: pathspec 'Git_Learn_Note.md' did not match any files。
  - A：添加某个文件时，该文件必须在当前目录下存在。
- ***git push 报错 Logon failed***
  - Q：在推送至GitHub时，报错信息"Logon failed, use ctrl+c to cancel basic credential prompt."
  - A：连续输入两次账户密码，第一次HTTP协议仍然会报错，第二次会变成OpenSSH协议，就成功了。原因暂未了解。但是如果在GitHub上先建立repo，然后 ***git clone*** 到本地，之后本地修改后再 ***git push*** 就不会出现这个现象了。
- ***git cherry-pick*** 提示需要手动merge
  - Q：在合并某个特定提交至当前分支时，***`git cherry-pick`*** 没有自动完成合并，而是提示conflict，需要手工解决冲突。
  - A：暂未研究明白如何能自动合并成功，未来学习过程中再研究。
- d

### Git命令列表

|Commond|说明|
|---|---|
|git add [file_name]|添加一个文件到Git，无论是新文件还是修改文件，都需要通过add之后，才能commit|
|git commit|将git add之后的文件，全部提交，并产生新的commit_id<br>-m "[comment]"：提交时，添加日志<br>-a [file_name]：讲一个没有add的文件，同时执行add和commit|
|git status|查看Git所管理的文件状态，包括哪些没有add，哪些add没有提交，哪些是新建文件，哪些是修改文件等|
|git diff|查看当前修改与Git当前版本之间的差异|
|git log|查看Git管理下的所有日志<br>--pretty=oneline：该参数简化log显示为同一行，方便查看<br>--graph：查看分支合并日志图<br>***`git log --graph --pretty=oneline --abbrev-commit`***|
|git reset [commit_id]|版本回退|
|git reflog|查看Git管理下所有被记录的操作|
|git restore|撤销修改，分为以下两种情况<br>git restore \<filename\>：git add之前，撤销工作区的修改<br>git restore --stage \<filename\>：git add之后，撤销暂存区的修改|
|git rm|删除文件|
|git remove|git remote add：将本地版本库关联远程版本库<br>git remote -v：查看本地库关联的远程库<br>git remote rm：删除本地库与远程库的关联|
|git push|将本地版本库已经提交的内容推送到远程版本库<br>首次推送增加-u参数|
|git branch|git branch：查看分支，当前分支前面是*<br>git branch \<branchname\>： 创建分支<br>git branch -d \<branchname\>：删除分支（未合并分支Git会提示不让删除，改为`-D`，强行删除）|
|git checkout|git checkout -- \<filename\>：老版本Git，撤销修改<br>git checkout \<branchname\>：切换分支<br>git checkout -b \<branchname\>：创建并切换分支|
|git switch|git switch \<branchname\>：切换分支<br>git switch -c <branchname\>：创建并切换分支|
|git merge|git merge \<branchname\>：合并指定分支到当前分支<br>--no-ff：合并分支时不允许 `fast forward` 模式，强行手动合并，并且体现commit日志<br>***`git merge --no-ff -m "commit日志内容" <branchname>`***|
|git stash|git stash：保存工作现场，便于bug修复分支之后恢复dev分支内容<br>git stash list：查看已经保存的工作现场列表<br>git stash pop：恢复被stash的工作现场，并删除stash内容<br>git stash apply \<stashid\>：恢复被stash的工作现场，但不删除stash内容<br>git stash drop \<stashid\>：删除stash内容|
|git cherry-pick|git cherry-pick \<logid>：复制某个特定提交到当前分支|
|||
|||