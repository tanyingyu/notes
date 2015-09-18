# Git简介
Git是一种版本控制系统。
Git是免费开源软件。

# Git作者设置
>git config --global user.name "谭映宇"
>git config --global user.email "tanyingyu@163.com"

# 必须学会的命令
随时掌握工作区的状态。
>git status
查看commit的日志。
>git log
查看所有操作的日志，包含reset和commit操作。
>git reflog

# 基本用法
>git add ［files］
>git commit -m '备注信息'
将版本库最新版本往前推一个版本。相当于最近一次没有提交。工作区没有修改。
>git reset HEAD^
相当于git reset --mix HEAD^

将版本库，缓冲区，工作区一起会退到commit_id时。
>git reset --hard commit_id 

将版本库中最新版的文件checkout到工作区
>git checkout -- [files]

# Github
## 注册github账号

## 创建SSH Key
[github文档](https://help.github.com/articles/generating-ssh-keys/）
>ssh-keygen -t rsa -C "tanyingyu@163"
在用户主目录~/.ssh目录中有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥。公钥需要上传到github服务器。

## 上传SSH public Key
登陆GitHub，打开“Account settings”，“SSH Keys”页面。然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。
>cat ~/.ssh/id_rsa.pub|pbcopy

## 创建远程库
在github上建名为notes的库。notes这个名字你可以自己定。

## 关联本地库与github远程库
### 关联
>git remote add ghhttps https://github.com/tanyingyu/notes.git
或
>git remote add ghssh git@github.com:tanyingyu/notes.git
#### 查看remote库
>git remote －v
#### 删除remote库
>git remote remove ghhttps
### 第一次推送
>git push -u ghssh master
### 日常推送
>git push ghssh master

