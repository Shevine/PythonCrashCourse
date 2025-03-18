# 附录D Git版本控制学习笔记
## 1  Git概述
版本控制软件能对项目进行快照记录，在项目出现问题时可恢复到之前的可行状态，无论是大型项目还是小型程序都非常实用。Git是当下流行的版本控制软件，它通过跟踪项目中每个文件的修改来实现版本控制，即使是独立开发者也能轻松使用其基本功能。

## 2  安装Git
### 2.1  Linux系统
在Linux系统中，打开终端，执行命令：
```bash
$ sudo apt-get install git
```
安装完成后即可在项目中使用Git。

### 2.2  OS X系统
1. 先在终端尝试执行命令：
```bash
git --version
```
若输出具体版本号，表明系统已安装Git；若提示安装或升级，按照屏幕上的说明操作。
2. 也可以访问[https://git-scm.com/](https://git-scm.com/)，点击“Downloads”，选择适合自己系统的安装程序进行安装。

### 2.3  Windows系统
访问[http://msysgit.github.io/](http://msysgit.github.io/)，点击“Download”下载安装程序并进行安装。

### 2.4  配置Git
Git需要知道你的用户名和电子邮件地址（即使只有自己参与项目开发），在终端执行以下命令进行配置：
```bash
$ git config --global user.name "username"
$ git config --global user.email "username@example.com"
```
若首次提交时未配置，Git会提示你进行设置。

## 3  创建项目
在系统中创建一个名为`git_practice`的文件夹，在该文件夹内创建一个Python程序`hello_world.py`，内容如下：
```python
print("Hello Git world!")
```
这个程序将用于学习Git的基本功能。

## 4  忽略文件
在Python项目中，扩展名为`.pyc`的文件是自动生成的，无需Git跟踪。在Python 3中，这些文件存储在`__pycache__`目录下。为让Git忽略该目录，在`git_practice`文件夹中创建一个名为`.gitignore`的特殊文件（文件名以句点打头且无扩展名），并在其中添加：
```
__pycache__
```
如果使用的是Python 2.7，应将内容改为：
```
*.pyc
```
部分文本编辑器默认忽略名称以句点打头的文件，可能需要修改设置以显示隐藏文件，才能打开`.gitignore`进行编辑。

## 5  初始化仓库
打开终端，切换到`git_practice`文件夹，执行命令：
```bash
git_practice$ git init
Initialized empty Git repository in git_practice/.git/
git_practice$
```
这表明Git在`git_practice`中初始化了一个空仓库。仓库是被Git主动跟踪的一组文件，Git管理仓库的文件都存储在隐藏的`.git/`目录中，不要删除此目录，否则会丢失项目所有历史记录。

## 6  检查状态
执行`git status`命令可查看项目当前状态，例如：
```bash
git_practice$ git status
# On branch master
# Initial commit
# Untracked files: 
#   (use "git add <file>..." to include in what will be committed)
# 	.gitignore
# 	hello_world.py
nothing added to commit but untracked files present (use "git add" to track)
git_practice$
```
从输出可知，当前位于`master`分支，处于初始提交状态，有未跟踪文件，需要使用`git add`命令来跟踪这些文件。

## 7  将文件加入到仓库
使用命令`git add.`将项目中所有未被跟踪的文件加入到仓库（但此时文件只是被Git关注，尚未提交）：
```bash
git_practice$ git add.
git_practice$ git status
# On branch master
# Initial commit
# Changes to be committed: 
#   (use "git rm --cached <file>..." to unstage)
# 	new file: .gitignore
# 	new file:  hello_world.py
git_practice$
```
此时再次查看状态，会发现Git识别出有需要提交的修改，且文件状态为“new file”，表示这些文件是新添加到仓库中的。

## 8  执行提交
执行提交操作，使用命令`git commit -m "message"`，其中`-m`用于记录提交消息：
```bash
git_practice$ git commit -m "Started project."
[master (root-commit) c03d2a3] Started project.
 2 files changed, 1 insertion(+)
 create mode 100644.gitignore
 create mode 100644 hello_world.py
git_practice$ git status
# On branch master
nothing to commit, working directory clean
git_practice$
```
提交后，再次查看项目状态，若显示“nothing to commit, working directory clean”，说明提交成功，工作目录干净。

## 9  查看提交历史
执行`git log`命令可查看详细的提交历史：
```bash
git_practice$ git log
commit a9d74d87f1aa3b8f5b2688cb586eac1a908cfc7f
Author: Eric Matthes <eric@example.com>
Date:   Mon Mar 16 07:23:32 2015 -0800
    Started project.
git_practice$
```
若想查看更简洁的版本，可使用`git log --pretty=oneline`命令：
```bash
git_practice$ git log --pretty=oneline
a9d74d87f1aa3b8f5b2688cb586eac1a908cfc7f Started project.
git_practice$
```
该命令只显示提交的引用ID和提交消息。

## 10  第二次提交
修改`hello_world.py`文件，添加一行代码：
```python
print("Hello Git world!")
print("Hello everyone.")
```
此时查看项目状态：
```bash
git_practice$ git status
# On branch master
# Changes not staged for commit: 
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
# 	modified: hello_world.py
no changes added to commit (use "git add" and/or "git commit -a")
git_practice$
```
可以看到Git检测到`hello_world.py`文件被修改且未提交。执行提交命令`git commit -am "message"`，其中`-a`表示将仓库中所有修改的文件加入到当前提交，`-m`用于记录提交消息：
```bash
git_practice$ git commit -am "Extended greeting."
[master 08d4d5e] Extended greeting.
 1 file changed, 1 insertion(+)
git_practice$ git status
# On branch master
nothing to commit, working directory clean
git_practice$ git log --pretty=oneline
08d4d5e39cb906f6cff197bd48e9ab32203d7ed6 Extended greeting.
be017b7f06d390261dbc64ff593be6803fd2e3a1 Started project.
git_practice$
```
提交后查看状态，确认工作目录干净，查看提交历史，可看到包含两个提交记录。

## 11  撤销修改
在`hello_world.py`中再添加一行代码：
```python
print("Hello Git world!")
print("Hello everyone.")
print("Oh no, I broke the project!")
```
保存后查看状态：
```bash
git_practice$ git status
# On branch master
# Changes not staged for commit: 
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
# 	modified: hello_world.py
# no changes added to commit (use "git add" and/or "git commit -a")
git_practice$
```
若不想提交此次修改，恢复到最后一次提交的状态，在终端执行命令：
```bash
git_practice$ git checkout.
git_practice$ git status
# On branch master
nothing to commit, working directory clean
git_practice$
```
此时`hello_world.py`文件会恢复到上次提交时的内容。对于大型项目，此功能可撤销自最后一次提交后对多个文件的所有修改，无需手动记录和撤销修改，方便快捷。

## 12  检出以前的提交
可以检出提交历史中的任意提交，在`git checkout`命令末尾指定该提交引用ID的前6个字符：
```bash
git_practice$ git log --pretty=oneline
08d4d5e39cb906f6cff197bd48e9ab32203d7ed6 Extended greeting.
be017b7f06d390261dbc64ff593be6803fd2e3a1 Started project.
git_practice$ git checkout be017b
Note: checking out 'be017b'.
You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by performing another checkout.
If you want to create a new branch to retain commits you create, you may do so (now or later) by using -b with the checkout command again. Example:
git checkout -b new_branch_name
HEAD is now at be017b7... Started project.
git_practice$
```
检出以前的提交后，会离开`master`分支，进入“detached HEAD”（分离头指针）状态。若要回到`master`分支，执行命令：
```bash
git_practice$ git checkout master
Previous HEAD position was be017b7... Started project.
Switched to branch'master'
git_practice$
```
若想放弃较近的所有提交，恢复到以前的状态，在`master`分支上执行命令`git reset --hard`，并指定要恢复到的提交引用ID前6个字符：
```bash
git_practice$ git status
# On branch master
nothing to commit, working directory clean
git_practice$ git log --pretty=oneline
08d4d5e39cb906f6cff197bd48e9ab32203d7ed6 Extended greeting.
be017b7f06d390261dbc64ff593be6803fd2e3a1 Started project.
git_practice$ git reset --hard be017b
HEAD is now at be017b7 Started project.
git_practice$ git status
# On branch master
nothing to commit, working directory clean
git_practice$ git log --pretty=oneline
be017b7f06d390261dbc64ff593be6803fd2e3a1 Started project.
git_practice$
```

## 13  删除仓库
当仓库历史记录混乱且无法恢复，若只有自己参与项目开发，可删除`.git`目录来删除仓库历史记录。删除后文件当前状态不受影响，但无法再检出项目的其他状态。
在终端中，先查看状态确认工作目录干净：
```bash
git_practice$ git status
# On branch master
nothing to commit, working directory clean
```
然后执行删除命令（Windows系统使用`rmdir /s.git`，其他系统使用`rm -rf.git`）：
```bash
git_practice$ rm -rf.git
```
删除后查看状态，会提示不是Git仓库：
```bash
git_practice$ git status
fatal: Not a git repository (or any of the parent directories):.git
```
若要重新跟踪修改，需重新创建仓库，执行命令：
```bash
git_practice$ git init
Initialized empty Git repository in git_practice/.git/
```
重新创建仓库后，再次查看状态，会回到初始状态等待第一次提交。接着将所有文件加入仓库并执行第一次提交：
```bash
git_practice$ git status
# On branch master
# Initial commit
# Untracked files: 
#   (use "git add <file>..." to include in what will be committed)
# 	.gitignore
# 	hello_world.py
nothing added to commit but untracked files present (use "git add" to track)
git_practice$ git add.
git_practice$ git commit -m "Starting over."
[master (root-commit) 05f5e01] Starting over.
 2 files changed, 2 insertions(+)
 create mode 100644.gitignore
 create mode 100644 hello_world.py
git_practice$ git status
# On branch master
nothing to commit, working directory clean
git_practice$
```
经过练习熟练掌握版本控制后，它将成为开发过程中不可或缺的工具。 