Actually this post i want to record the git command on linux, and how to use git. many people don't know how to use git when know it fist.

实际上，这篇文章我想记录一下在Linux上使用的git命令，以及如何使用git。
很多人在初次接触git时并不知道如何使用。
当然也不要由于在Linux系统上而下意识的产生畏惧心理，无需如此，其实很简单，而且命令都是相通的。

# what is git - 什么是git

> [!note] what is git
> 
> git is a distribution system to control the code version, and also now can control any file version. so i use it control my knowledge base file on github.



Git 是一个用于控制代码版本的分布式系统，现在也可以控制任何文件的版本。所以我使用它来控制我的知识库文件在 GitHub 上的版本。通俗讲，git是一个可以控制你系统文件版本的一个控制系统，内里集成了很多用于版本控制的功能，可以通过不同的命令进行文件的版本控制，这是一个十分高效的版本控制+记录的系统，可以极大的省去各种繁琐和无效的版本记录时间。

当然也无需紧张，实际上学会git的命令相当简单，如果你看不了官方文档，可以直接看下文的步骤，对于平时使用的需求来说，几乎足够用了。

# how to use - 如何使用

## 下载安装

本篇虽然是讲git在linux上的应用，但是也顺便告诉各位读者windows系统的安装方式，其余命令都基本一样，这样各位读者也可以在Windows系统上学习使用git。

### Windows 系统安装 git

- https://git-scm.com/downloads - 官方下载界面

只需要点击右侧的按钮下载git安装包，按照正常的程序点击安装即可，和其他软件是一样的

![[Pasted image 20250308110704.png]]

![](../images/Pasted%20image%2020250308110704.png)

### Linux安装git

Linux各大发行版基本都有默认安装的git版本，或者软件仓库中有，只需要轻轻敲几个命令即可，按照下图所示，即可安装成功。

> [!note]
> 在安装成功之前，请先确定好本机的Linux发行版版本，再按照对应的命令

- https://git-scm.com/downloads/linux - 下载指南界面

![](../images/Pasted%20image%2020250308110741.png)

## 初始化 - initialization

首先需要选定一个空目录初始化，意思就是告诉git我选了这个目录作为后面操作的文件目录，git就会对这个目录进行一些配置，生成一些对于的文件。

```bash
git init
```

### 本地配置

初始化后，要先对git进行一些对应的配置

### 查看主分支名称

git 初始化后会在本地产生分支，一般分支默认为***master***，但是我建议改为 ***main***，因为后面如果需要和GitHub进行远程连接，需要保持一致，GitHub上默认的repo分支版本是 ***main***

```bash
git branch -m main   # 把分支名称改为 main
```

### 绑定github远程分支

可能到这里有朋友疑惑，为什么要连接GitHub远程分支呢，其实这里就涉及到了一个同步的问题，GitHub可以在云端存储你的文件，使用git与其连接后，你对于多端同步的需求是不是就能满足了呢。

```bash
# 使用git 添加远程分支 需要后续登陆用户名和密码
git remote add origin https://github.com/HachGo/KnowledgeBase.git
# 需要提前配置好本地的远程的GitHub的密钥
git remote add origin git@github.com:HachGo/Linux-Lab.git
```

密钥的配置稍微有些多，也需要单独讲讲，可以查看下面的官方文档，一步步操作

- [github 密钥配置](https://git-scm.com/book/zh/v2/GitHub-%e8%b4%a6%e6%88%b7%e7%9a%84%e5%88%9b%e5%bb%ba%e5%92%8c%e9%85%8d%e7%bd%ae)
  若是命令运行成功后，然后使用下面命令查看
  
  ```bash
  git remote -v  # 查看和GitHub远程分支连接情况
  ```
  
  命令运行示例如下：
  
  ```bash
  eric@MyPc ~/KnowledgeBase (main)> git remote -v
  origin    https://github.com/HachGo/KnowledgeBase.git (fetch)
  origin    https://github.com/HachGo/KnowledgeBase.git (push)
  ```
  
  ### 移除绑定的方法
  
  ```
  git remote remove origin
  ```

## operate git - 操作使用git进行版本控制

操作使用git时，最好按照如下步骤，每次先拉取远程分支，同步最新的状态，然后再对本地操作进行提交，这样会减少报错。

### pull version from the remote - 拉取远程分支

拉取远程仓库进行同步

```bash
git fetch origin     # 命令用于从远程仓库拉取数据到本地，但不会自动合并到当前工作分支
git pull origin main # git fetch后跟git merge的简写，用于从远程仓库拉取数据并合并到当前工作分支
```

### pull the remote version to local

在提交到远程仓库之前，你需要先将本地的更改提交到本地仓库，这样本地仓库就会记录下来

```bash
git add .                                ## 注意有个点，意思是提交当前目录全部文件
git commit -m "Initial commit"           ## 这个操作是将本地更改记录提交到记录库中
```

最后，将本地的提交推送到 GitHub 上的远程仓库：

```
git push -u origin main
```

-u 参数会将 origin master 设置为默认的远程分支，这样以后你只需要运行 git push 就可以推送到这个分支。

> [!note] 初始提交时需要选择如何合并版本的方式
> 
> hint: You have divergent branches and need to specify how to reconcile them.
> hint: You can do so by running one of the following commands sometime before
> hint: your next pull:
> hint: 
> hint:   git config pull.rebase false  # merge (the default strategy)
> hint:   git config pull.rebase true   # rebase
> hint:   git config pull.ff only       # fast-forward only
> hint: 
> hint: You can replace "git config" with "git config --global" to set a default
> hint: preference for all repositories. You can also pass --rebase, --no-rebase,
> hint: or --ff-only on the command line to override the configured default per
> hint: invocation.



- `--rebase`：强制使用变基策略。
  - 本地分支的提交“重新应用”到远程分支的最新提交上，使历史更加线性
- `--no-rebase`：强制使用合并策略。- 推荐
  - 保留两个分支的完整提交历史，可以选择合并策略
- `--ff-only`：仅允许快进。
  - 在远程分支领先于本地分支时进行快进，而不进行合并或变基，可以选择仅快进策略


# gitignore 配置某个文件不参与远程分支同步

The file .gitignore is the file for git system to know which file will not be in the git sync process.
***.gitignore*** 文件是 Git 系统用来识别哪些文件不会被包含在 Git 同步过程中的文件。

## 方法 1：添加到 `.gitignore` - 推荐

1. 打开 `.gitignore` 文件（如果没有，可以创建一个）。

2. 向 .gitignore 文件添加不需要同步的目录或者文件



![](../images/Pasted%20image%2020250308114841.png)

3. 保存文件。

4. 如果该文件已经被 Git 跟踪，需要先从 Git 中移除它：
   
   ```
   git rm --cached .obsidian/workspace.json
   ```

5. 再提交更改：
   
   ```
   git add .gitignore
   git commit -m "Ignore .obsidian/workspace.json"
   ```

## 方法 2：使用 --assume-unchanged

如果不想修改 `.gitignore`，可以直接告诉 Git 忽略该文件的更改：

```bash
git update-index --assume-unchanged .obsidian/workspace.json
```

# reference - 参考网址

- [官方教程 - 中文](https://git-scm.com/book/zh/v2)
- [git 官方教程 - 英语原址](https://git-scm.com/docs)