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

1. 状态与查看

`git status`#查看文件状态

`git log`#查看记录

`git diff` #查看具体改动

2. 本地提交

`git add .`  #提交所有文件假如暂存

`git add 文件名`#提交单个文件

`git commit -m "说明"`#提交到本地仓库

3. 远程同步

`git push`# 上传，本地-》网站

`git pull`# 拉取，网站（最新）-》本地

4. 分支

`git branch`#查看分支

`git branch 新分支名`#创建分支

`git checkout 分支名`#切换分支

5. 撤销

`git reset --soft HEAD~1`#撤销最后一次提交

回退到git commit之前，若不修改文件提交不用再git add ，若修改了文件，需要重新git add到缓存区

`git checkout`#撤销工作区的所有改动，返回到上一次之前	

### 五、个人理解

1. git 和github是分开的2个部分，可以只用git进行本地管理。

































