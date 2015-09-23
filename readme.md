# Git简介
Git是一种版本控制系统。

Git是免费开源软件。

# Git作者设置

    git config --global user.name "谭映宇"
    git config --global user.email "tanyingyu@163.com"

# 必须学会的命令

随时掌握工作区的状态。

    git status

查看commit的日志。
    git log

查看所有操作的日志，包含reset和commit操作。

    git reflog

# 基本用法

将工作区文件添加到stage暂存区。

    git add [files]

提交并写提交备注。

    git commit -m '备注信息'

订正最近一次的提交。

    git commit --amend

比如：

刚才我做了修改，并且提交了。但马上发现提交的数据不全，或其他问题。我们可以马上订正提交。

    git commit -m '提价一次'

发现有问题，即刻订正。如‘提交’错写成了‘提价’。

    git commit --amend -m '提交一次。'

当然，你也可以，add一些文件后，在amend提交。相当于上次忘提交了一些东西。

将版本库最新版本往前推一个版本。HEAD ref往前移动。工作区没有修改。

    git reset HEAD^

相当于

    git reset --mix HEAD^

将版本库，缓冲区，工作区一起会退到commit_id时。

    git reset --hard commit_id 

将版本库中最新版的文件checkout到工作区

    git checkout -- [files]

# Github
## 注册github账号

## 创建SSH Key

[github文档](https://help.github.com/articles/generating-ssh-keys/）

    ssh-keygen -t rsa -C "tanyingyu@163"

在用户主目录~/.ssh目录中有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥。公钥需要上传到github服务器。

## 上传SSH public Key

登陆GitHub，打开“Account settings”，“SSH Keys”页面。然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。

    cat ~/.ssh/id_rsa.pub|pbcopy

## 创建远程库

在github上建名为notes的库。notes这个名字你可以自己定。

## 关联本地库与github远程库
### 使用https关联，无写入权限。（由于https没有写入方式）

    git remote add ghhttps https://github.com/tanyingyu/notes.git

### 使用ssh关联。

    git remote add ghssh git@github.com:tanyingyu/notes.git

#### 查看remote库
    git remote －v

#### 删除remote库
    git remote remove ghhttps

### 第一次推送,推送当前branch到ghssh/master分支。
    git push -u ghssh master

### 日常推送，推送当前branch到ghssh/master分支。
    git push ghssh master

## 克隆远程库

在一个全新的目录中。

    git clone git@github.com:tanyingyu/notes.git

# 分支

## 查看分支

    git branch -a

## 创建分支

    branch <<branch_name></branch_name>

## 创建并切换分支
    checkout -b <<branch_name></branch_name>

## 切换分支
    checkout <<branch_name></branch_name>

## 合并分支
将dev分支合并入当前分支

    merge <<branch_name></branch_name>

## 删除分支

    git branch -d <<branch_></branch_>

## 获取远端分支
获取远端分支到本地当前分支。
    git pull ghssh dev

## 解决冲突


