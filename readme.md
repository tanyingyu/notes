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

# 基本用法
## 初始化新版本库
在HOME\project1目录下新建一个项目，生成一个.git的文件夹。
```Bash
cd ~
mkdir project1 && cd project1
git init
```
## 设置忽略的文件
在项目更目录下新建.gitignore文件，填写忽略文件列表。然后提交到版本库即可。
>配置语法：
  git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；
* 以斜杠“/”开头表示目录；
* 以星号“*”通配多个字符；
* 以问号“?”通配单个字符
* 以方括号“[]”包含单个字符的匹配列表；
* 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；


将工作区文件添加到stage暂存区。
```Bash
git add [files]
```

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

`使用git reset一定要*非常小心*，因为会清除工作区的修改。该操作不可逆。`

将版本库中最新版的文件checkout到工作区

    git checkout -- [files]

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


