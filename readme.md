# 命令速查
>工作区（即项目目录中的文件）
>>-->暂存区（及.git/index）
>>>-->本地版本库(.git/*)
>>>>-->远端版本库

* [工作区到暂存区](#工作区到暂存区)
* [暂存区到本地版本库](#暂存区到本地版本库)

# Git简介
Git是一种版本控制系统。Git是免费开源软件。

推荐网站：
* [官网](http://git-scm.com)

推荐书籍：
* [pro git](http://git-scm.com/book/zh/v2)

# 全局环境设定
## 作者设置
```Bash
git config --global user.name "谭映宇"
git config --global user.email "tanyingyu@163.com"
```
## 界面设置
设置git终端界面为彩色显示。
```Bash
git config --global color.ui true
```
# 必须学会的命令
## 状态类命令
随时掌握工作区的状态。
```Bash
git status
```
查看commit的日志。
```Bash
git log
```
查看所有操作的日志，包含reset和commit操作。
```Bash
git reflog
```

## 基本用法
### 初始化新版本库
在HOME\project1目录下新建一个项目，生成一个`.git`的文件夹。
```Bash
cd ~
mkdir project1 && cd project1
git init
```
### 设置忽略的文件
在项目更目录下新建`.gitignore`文件，填写忽略文件列表。然后提交到版本库即可。
>配置语法：  
git 对于`.gitignore`配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；
* 以斜杠“/”开头表示目录；
* 以星号“*”通配多个字符；
* 以问号“?”通配单个字符
* 以方括号“[]”包含单个字符的匹配列表；
* 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；

## 工作区到暂存区
### 跟踪新文件
将工作区文件添加到stage暂存区。
```Bash
＃添加单个文件
git add readme.md
#添加所有后缀为.c的文件
git add *.c
#添加目录下（含子目录下的文件）所有文件，但不含空目录。
git add .
```

### 移除文件
将文件从版本库中清除，同时从stage暂存区移去。
``同时可以清除工作区文件``，无清除工作区使用``--cached``。如果提交的时候，该文件想试使用版本管理了。如果删除之前修改过并且已经放到暂存区域的话，
则必须要用强制删除选项-f。
```Bash
＃移去单个文件
git rm readme.md

＃移去文件，但不清除工作区文件。
git rm --cached readme.md

＃强行移去文件，但不清除工作区文件。
git rm -f --cached readme.md

#移去log目录下（含自文件夹）所有后缀为.log的文件。
#［注意‘\’，相当于git收到的字符串是　log/*.log］。
git rm log/\*.log

#移去log目录下（不含子文件夹）所有后缀为.log的文件。
#［无‘\’，相当于git收到的是shell解析出来的一个文件列表］。
git rm log/*.log

#添加目录下（含子目录下的文件）所有文件，但不含空目录。
git add .
```

## 暂存区到本地版本库
### 提交
提交并写提交备注。
```Bash
git commit -m '备注信息'
```

增补提交，订正最近一次的提交。__只能针对最后一个提交__。
```Bash
git commit --amend -m '备注信息'
```
比如：

刚才我做了修改，并且提交了。但马上发现提交的数据不全，或其他问题。我们可以马上订正提交。
```Bash
git commit -m '提价一次'
```

发现有问题，即刻订正。如‘提交’错写成了‘提价’。
```Bash
git commit --amend -m '提交一次。'
```
当然，你也可以，add一些文件后，在amend提交。相当于上次忘提交了一些东西。

### 反转提交

### 复位操作
reset是Git最常用命令之一，同时也最危险最容易误用的命令。所以要好好理解其工作机理。错误使用的最大问题：暂时丢失**工作区**的修改数据，为什么是暂时了？理解机理后，我相信你即使用错，也可以修复。呵呵！

复位操作命令格式：
```Bash
#用法一：
git reset [-q] [<commit>] [--] <paths>...
#用法二：
git reset [--soft --mixed | --hard | --merge | --keep] [-q] [<commit>]
```

* 第一种用法（`包含了路径<paths>的用法`）不会重置引用，更不会改变工作区，而是用指定提交状态(<commit>)下的文件(<paths>)替换掉暂存区中的文件。  
`一般用途`：git reset HEAD <paths>取消之前执行的git add <paths>命令。
> 注意：  
> 在命令中包含路径<paths>。为了避免无法分辨是路径与引用（或者提交ID）时，需要在<paths>
> 前用两个连续的短线（减号）作为做标记。如：<commit>和<paths>同名时，就需要用'--'标记<paths>。

* 第二种用法（`不使用路径<paths>的用法`）则会重置引用。根据不同的选项，可以对暂存区或工作区进行重置。来看一看不同的参数对第二种重置语法的影响。
    1. 使用参数--hard，如git reset --hard <commit>
        1. 替换HEAD的指向。HEAD指向<commit>。
        2. 替换暂存区。替换后，暂存区的内容和引用指向<commit>的目录树一致。
        3. 替换工作区。替换后，工作区的内容变得和暂存区一致，也和<commit>所指向的目录树内容相同。
    2. 使用参数--soft，如 git reset --soft <commit>
        1. 只替换HEAD的指向，不改变暂存区和工作区。
    3. 使用参数--mixed或者不使用参数（默认为--mixed），如 git reset <commit>
        1. 替换HEAD的指向。HEAD指向<commit>
        2. 替换暂存区。替换后，暂存区的内容和引用指向<commit>的目录树一致。不改变工作区。

将版本库HEAD引用指向往前移动。
```Bash
git reset --soft commit_id 
```

将版本库HEAD引用指向往前移动，暂存区内容替换。
```Bash
git reset HEAD^
#相当于
git reset --mixed HEAD^
```

将版本库HEAD引用指向往前移动，暂存区内容替换，工作区替换。
```Bash
git reset --hard HEAD^ 
```

## 本地版本库操作
### 分支
将版本库中最新版的文件checkout到工作区
    git checkout -- [files]
### 标签

### 归档

# Github
## 注册github账号

## 创建SSH Key
[官方文档](https://help.github.com/articles/generating-ssh-keys/) 

    ssh-keygen -t rsa -C "tanyingyu@163.com"

在用户主目录~/.ssh目录中有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥。公钥需要上传到github服务器。

## 上传SSH public Key

登陆GitHub，打开“Account settings”，“SSH Keys”页面。然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。

    cat ~/.ssh/id_rsa.pub|pbcopy

## 创建远程库

在github上建名为notes的库。notes这个名字你可以自己定。

## 关联本地库与github远程库
### 使用https关联
https写入（push）需要每次使用用户和密码。

    git remote add ghhttps https://github.com/tanyingyu/notes.git

### 使用ssh关联
使用公钥密钥机制，无需输入用户和密码。

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


