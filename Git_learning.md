# Git Learing

## Git教程[->](https://www.liaoxuefeng.com/wiki/896043488029600)

### Git简介

Git是目前世界上最先进的分布式版本控制系统。[Git官网下载](https://git-scm.com/downloads)

### 创建版本库

首先，选择一个合适的地方，创建一个空目录：

```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

第二步，通过`git init`命令把这个目录变成Git可以管理的仓库

```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

> `git` 查找功能；
>
> `git add`把工作区文件添加到缓存区；
>
> `git commit -m "XXX"`缓存区提交到仓库；
>
> `git status`显示仓库当前状态



---

### 时光机穿梭

如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别

- 版本回退

  > - `git log`命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数。
  >
  > - 你看到的一大串类似`1094adb...`的是`commit id`（版本号）
  > - 在Git中，用`HEAD`表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。
  > -    `git reset --hard HEAD^ `回退到上一个版本。还用`git log`再看看现在版本库的状态：
  > -   只要命令行窗口还没有被关掉，找到那个`某次日志`的`commit id`就可以指定回到未来的某个版本：`git reset --hard commit_id`.版本号没必要写全，前几位就可以了.
  > -   如果令行窗口被关掉，可以用命令`git reflog`用来记录你的每一次命令。

---
- 撤销修改

  > 1. **工作区修改**：命令**`git checkout -- readme.txt`**意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：
  > - 一种是`readme.txt`自修改后**还没有被放到暂存区**，现在，撤销修改就回到和版本库（仓库git）一模一样的状态；
  >
  > - 一种是`readme.txt`**已经添加到暂存区**后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
  >
  > ​        总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。
  >
  > 2. **工作区修改后`git add`到暂存区，没有`git commit`**：`git status`后提示我们，用命令**`git reset HEAD <file>`**可以把暂存区的修改撤销掉（unstage）,即`git reset HEAD readme.txt`
  >
  >    > 1. `git reset`命令既可以回退版本，也 可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。
  >    > 2. 再用`git status`查看一下，现在暂存区是干净的，工作区有修改，同上可用**`git checkout -- readme.txt`**丢弃工作区的修改.
  > 3. 工作区修改后`git add`到暂存区，并且`git commit`到版本库，可以用上节的版本回退，回退到上一个版本。不过前提是没有推送到远程库。

---

- 删除文件

  add并且commit到版本库

  >1. 命令**`git rm`**用于删除一个文件。
  >
  >   - 一种是确实要**从版本库中删除该文件**，那就用命令`git rm`删掉，并且`git commit`。
  >   - 另一种情况是**删错了**，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：`git checkout -- test.txt`
  >
  >2. `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
  >
  >   如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

---



### 远程仓库

- 添加远程库

  把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

  > 1. GitHub上创建空的同名仓库，如learngit。
  >
  >    先关联一个远程库，并指定名字（通常为origin）。在本地的`learngit`仓库下运行命令**使用命令`git remote add origin `**
  >
  >    ```
  >    $ git remote add origin git@github.com:michaelliao/learngit.git
  >    ```
  >       请千万注意，把上面的`michaelliao`替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。
  >
  >    **添加后，远程库的名字就是`origin`，这是Git默认的叫法**，也可以改成别的，但是`origin`这个名字一看就知道是远程库。
  >
  > 2. 下一步把本地库的所有内容推送到远程库上。
  >
  >    ```
  >    git push -u origin master
  >    ```
  >    用`git push`命令，实际上是把当前分支`master`推送到远程。
  >
  >    由于远程库是空的，我们第一次推送`master`分支时，**加上了`-u`参数**，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，**还会把本地的`master`分支和远程的`master`分支关联起来**，在以后的推送或者拉取时就可以简化命令。
  >
  >    ---
  >
  >    从现在起，只要本地作了提交，就可以通过命令：
  >
  >    ```
  >    $ git push origin master
  >    ```
  >
  >    把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！
  >
  >    ---
  >
  > 3. 删除远程库（绑定关系）
  >
  >    如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息，然后，根据名字删除，比如删除`origin`：
  >
  >    ```
  >    $ git remote rm origin
  >    ```
  >    此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

- 从远程库克隆

  现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

  > 1. 登陆GitHub，创建一个新的仓库。
  >
  > 2. 下一步是用命令`git clone`克隆一个本地库。
  >
  >    ```
  >    $ git clone git@github.com:michaelliao/gitskills.git
  >    ```
  >
  >    如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。
  >
  >    Git支持多种协议，包括`https`，但`ssh`协议速度最快。

---

### 分支管理[->](https://www.liaoxuefeng.com/wiki/896043488029600/896954848507552)

- 创建与合并分支

  > 查看分支：`git branch`
  >
  > 创建分支：`git branch <name>`
  >
  > 切换分支：`git checkout <name>`或者`git switch <name>`
  >
  > 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`
  >
  > 合并某分支到当前分支：`git merge <name>`
  >
  > 删除分支：`git branch -d <name>`

