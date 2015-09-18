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
git add ［files］
git commit -m '备注信息'
将版本库最新版本往前推一个版本。相当于最近一次没有提交。工作区没有修改。
git reset HEAD^
相当于git reset --mix HEAD^
将版本库，缓冲区，工作区一起会退到commit_id时。
git reset --hard commit_id 

