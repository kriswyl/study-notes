# git学习

### 一、首次配置（只做一次）

#### 1.设置用户名和邮箱地址。

`git config --global user.name "github用户名"`

`git config --global user.email "github邮箱名`

#### 2.查看配置

`git config --list`

### 二、把本地文件夹上传到 GitHub

#### 1.用git终端进入文件夹

`cd 文件名`

#### 2.初始化为git仓库

`git init`

#将普通文件夹转化为可以被git记录，追踪，控制版本的文件夹，变化是文件夹中多了.git文件

#### 3.将文件夹关联到对应的github仓库

`git remote remove origin`	#清空旧关联

`git remote add origin "https://github.com/github关联仓库名字.git"`   #建立新关联

#### 4.上传到本地仓库

`git add .`#需要上传更新的文件，"."代表所有文件

`git commit -m "备注"`#上传到本地仓库

#### 5.上传到github

`git branch -m main `#重命名分支

`git push -u origin main`

### 三、日常更新

`git status `#查看那些文件修改了

`git add .` #加入暂存

`git commit -m "写更新内容，备注"`# 上传到本地仓库

`git push`#推送到github上

### 四、常用命令

`git status`#查看文件状态

`git log`#查看记录



















