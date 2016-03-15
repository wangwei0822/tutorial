配置设置
=========

> git config --global user.name "用户全名" 

> git config --global user.email "邮件地址" 

> git config --global color.ui "auto" 


提交与版本列表
============


## 提交

* `git commit -a`

将全部修改过的文件提交。但注意：只会把已纳入版本控制的文件添加进去，而不会添加尚未跟踪的文件，这点与hg不同（hg commit -A 会自动添加新增文件）；注意，git 1.8以后，不会自动添加删除的文件，需要带 `--all`选项才可以

* `git log -1`
    查看版本历史，仅列出一条
    
* `git log --pretty=oneline`
    简洁显示版本历史，每行一个版本
    
* `git log <版本号>`
查看自指定版本到现在的提交

* `git log --since="5 hours"`
查看最近5小时内的提交

* `git log --before="5 hours" -1`
查看5小时之前最后一个提交

* `git log --pretty=oneline`
简洁显示

分支
=====

分支可以为要发布的代码保留一份拷贝，而无须停止正在开发的工作。

* `git branch RB_1.0 master`
    从主分支上创建RB_1.0分支（release branch，代表发布分支）
    
* `git branch RB_1.0.1 1.0`
    从标签为1.0的版本创建分支RB_1.0.1
    
* `git checkout RB_1.0`
    切换到指定分支RB_1.0，当前工作目录状态变为RB_1.0目录状态，另一分支在版本库中安全。
    
* `git tag 1.0 RB_1.0`
    将RB_1.0分支的当前头版本加标签1.0
    
* `git tag`      查看标签列表

变基
=====

* `git checkout master`
切换回主分支

* `git rebase RB_1.0`
变基，将当前头版本置于指定的分支（头版本）之后，实现分支合并。

* `git branch -d RB_1.0`
删除分支RB_1.0

打包
=====

通常形式：

* `git archive --format=tar --prefix=压缩包内根目录名称/ <标签、分支或其他ref名称> -o 输出文件名.tar` 

* `git archive --format=zip --prefix=压缩包内根目录名称/   HEAD  > release.zip`
注意prefix参数要以/结尾！

* `git archive --format=tar --prefix=压缩包内根目录名称/     HEAD | gzip > release-1.0.tar.gz`
用以上方法导出的打包不包括版本库数据！

比较差异
========

* 比较【工作目录】和【版本库】差异：
`git diff HEAD `  ___★常用！___

    HEAD表示当前分支末梢的最新版本！
* 比较【暂存区】和【版本库】差异：
`git diff --cached`
* 比较【工作目录】和【暂存区】差异：
`git diff`

移动
=====

移动工作目录文件：
`git mv 老路径 新路径`

忽略设置
=========

如果是共享版本库的人之间共用的文件忽略规则，则添加到.gitignore。如果是仅个人需要的忽略，则在.git/info/exclude文件中添加。



分支管理
=========

* `git branch -m master mymaster`
把主分支重命名为mymaster

* `git branch`
不带参数的branch命令，显示所有分支名称


*  `git checkout -b alternate master  `  
从master分支末梢创建分支alternate，并立即检出到工作目录
★常用！

## 分支典型应用场景
**典型场景就是在开发分支中工作，主分支保持一个可用来发布的版本**

* `git branch develop master`  
(从主分支创建分支develop）

* `git checkout develop`  
(切换到分支develop)

* 上述两条命令也可以合为一条：`git checkout -b develop master`

* 把本地develop分支推到服务器上：`git push origin develop`

**除团队负责人之外，其他成员的环境下，最好只保留develop分支，这样做：**

`git clone git@git.gf.com.cn:gfportal/gfportalui.git -b develop`  
这样，成员以后再提交，就会只提交到develop分支，不会影响master

## 创建分支场景

1. 试验性修改  
2. 增加新功能  
3. Bug修改  


## 分支合并方法
1. 直接合并
2. 压合合并
3. 拣选合并

### 【直接合并】
`git checkout master`  
`git merge alternate`  
切换到主分支，然后把alternate分支合并过来，这样alternate分支上的修改历史就合并到主分支了


### 【压合合并】★常用！

此时所需要的是合并某个试验（在某分支上进行的）的结果，而无需记录试验的轨迹。

* `git checkout master`

* `git merge --squash contact`  
此时contact分支上若干提交已经合并到当前工作区并暂存，需要用commit命令提交



### 【拣选合并】

* `git cherry-pick 提交标识号`
将其他分支上特定的一次提交合并到当前分支并立即提交！

* `git cherry-pick -n 提交标识号`
同上操作，但不立即提交；接着可进行下一个拣选…

* `git commit`
不带-m参数，自动使用之前拣选的若干提交的留言作为此次提交留言！


* `git mergetool`
启动冲突合并工具，会自动查找kdiff3、vimdiff或opendiff（xcode）等

## 分支删除

* `git branch -d xxxx`
删除xxxx分支。注意：只有当要删除的分支已经成功合并（直接合并）到当前分支时，此操作才会成功。

* `git branch -D xxxx`
无需合并前提，强制删除分支xxxx

## 其他

* `git branch -m 旧名称 新名称`
分支重命名

* `git log 1.0..HEAD`
列出标签为1.0的版本之后到当前的历史提交。

* `git diff --stat 1.0`
统计自标记为1.0的版本以来的变更统计


* `git commit -a --amend`
增补提交，把最新修改增补到上一个提交。★常用！

* `git fetch`
从远程版本库获取更新

* `git push origin mybranch:master`

* `git gc `
（或 `git gc --aggressive`）
整理优化版本库


反转与复位
=========

* `git revert `
在版本库中创建一个反向的新提交来抵消原来提交的改动

* `git revert -n HEAD`
反转HEAD版本，但先不自动提交反转结果

* `git reset`
撤销最近一次提交

* `git reset HEAD^`
把版本库复位到当前头版本之前的版本
【注意】复位后，工作目录与版本库的差异被自动暂存！

* `git reset --hard HEAD^`
将版本库回退到头版本之前的那个版本，并在【工作目录】中删除变更！

### ___revert命令与reset命令的区别___

>revert会产生一次反向的提交来抵消之前的提交！执行  
>`git revert HEAD `  
>后，此时会产生一个新的提交，这个提交反转了之前头版本的修改，工作目录实际状态退回同HEAD^
。  
> 
> 与此对照，执行  
> `git reset --hard HEAD^`  
>此时会将版本库退回头版本之前的版本，而且工作目录也恢复成HEAD^ 的状态，之后的改动全部消失。
>如果不带hard参数，则git会缓存工作目录与头版本因复位产生的差异，用户可修改后再次提交
>而revert如果带-n参数，则反转后并不立即提交


### 从缓存中删除

    git rm --cached <file>

标签的使用
=========

*  __标签__只代表特定的一个版本，检出一个标记的版本，修改后再提交，就不是那个标签的版本了。

* `git checkout -b from-1.0 1.0`
从标签为1.0的版本创建分支from-1.0，并立即检出该分支
* `git tag contacts/1.1 contacts`
为contacts上头版本添加标签，此标签为“contacts/1.1”（标签中可以包含“/”和“.”等字符）


冲突解决
=======

## 冲突解决命令

* `git rebase 1.0.1`
把当前HEAD变基到标记为1.0.1
假如有冲突，此时变基会挂起，需用以下

* `git mergetool` 处理冲突，完成后commit即可

* `git add` 解决了冲突的文件

* `git rebase --continue`
这样就可以使变基在解决冲突后继续

## 冲突解决工具（及Diff工具）配置

先安装一种Diff/Merge工具，这里推荐[DiffMerge](http://www.sourcegear.com/diffmerge/downloads.php)

### 在Mac上配置DiffMerge工具：

	git config --global merge.tool diffmerge
	git config --global mergetool.diffmerge.cmd "/Applications/DiffMerge.app/Contents/MacOS/diffmerge --	merge --result=\$MERGED \$LOCAL \$BASE \$REMOTE"
	git config --global mergetool.keepBackup false
 	git config --global diff.tool diffmerge
	git config --global difftool.diffmerge.cmd "/Applications/DiffMerge.app/Contents/MacOS/diffmerge \$LOCAL \$REMOTE"
	
### 在Windows上配置DiffMerge工具：

	git config --global merge.tool diffmerge
	git config --global mergetool.diffmerge.cmd "/c/Program Files/SourceGear/Common/DiffMerge/sgdm.exe --merge --result=\$MERGED \$LOCAL \$BASE \$REMOTE"
	git config --global mergetool.keepBackup false
 	git config --global diff.tool diffmerge
	git config --global difftool.diffmerge.cmd "/c/Program Files/SourceGear/Common/DiffMerge/sgdm.exe \$LOCAL \$REMOTE"
	


blame命令
=========

* `git blame 文件路径`
查看指定文件的行修订历史

* `git blame -L "/<\/body>/",+2  hello.html`
查看hello.html文件中两行的修订历史，范围是：找的匹配正则式的行开始的两行。

* `git blame -L "/<\/body>/",-2 4333289e^ -- hello.htm`
查看指定文件hello.html在4333289e之前指定行的修订历史。

* `git blame -M 文件路径`
检测一个文件内移动或复制的行

* `git blame -C -C 文件`
查看指定文件的行拷贝信息（从哪个文件复制而来）

STASH 命令 
==========

* 该命令可以将工作目录的改动保存至别处，然后将工作目录恢复为头版本状态。不带参数的git stash命令等同于save子命令

* 保存在别处的改动可用stash list列出，可用show检视

* 可用stash apply命令（恢复）执行修改

* 最新保存的存放于$GIT_DIR/refs/stash目录下，引用表示：  
`stash@{0}`  最新的存储  
`stash@{1}`  当前上一次存储  
`stash@{2.hours.ago}`  2小时前的存储  
    列表时显示的**WIP**表示***work in process***（半成品、过程中制品）
    
* 典型用例：  
`git stash`    先把工作目录状态另存别处
（此时工作目录已回退HEAD版本）

## 基于HEAD版本的紧急修改

* `git commit -a`    提交紧急修改
 
* `git stash apply`   把暂存的修改复原  

    ___注意___  
    apply时，会试图将stash存储的改动与当前目录状态进行merge

操作远程版本库
=================

## 客户端配置SSH通信密钥对

	ssh-keygen -q -N '' -t rsa -f ~/.ssh/id_rsa
	


## 同步远程版本库

* `git fetch`
把远程分支的改动取到本地，但它不会把远程分支上的修改合并到本地分支

* `git pull`
顺序完成两件事：取来，然后合并

		git pull origin branch-name  
	__从远程版本库origin拖入分支branch-name上的改动__

* `git push`，例如：  
`git push origin mybranch:master`  
将本地分支mybranch上的提交推入远程版本库master分支。___origin___是远程版本库别名，是clone操作时自动生成的。  

* 如果版本库不是clone而是本地新建的，可以给远程版本库指定别名，例如：  

		git remote add origin git@git.gf.com.cn:frank/myproject.git
		#如果remote add url有错，可以用`git remote rm`删除远程标签
				

* `git remote`
查看本地创建的全部远程版本库别名

* `git remote rm 别名`
删除指定远程版本库别名

		git remote rm bitbucket
		#但以上命令在老版本的git中不支持，老版本的git可以通过以下方式删除远程标签
		vi .git/config


* 把本地已提交的改动推入远程版本库，而___不会推入工作目录树和暂存区中的改动___


* 被推入本地版本库的改动，不会自动反映在这个版本库的工作目录上！如果想反映到工作目录，需显式运行`git checkout HEAD`，此时可能需要解决冲突。

* 将origin源的master分支设置为上游版本库，即pull/push默认目标：

		git branch --set-upstream master origin/master


文件忽略
=======

`.gitignore`文件示例如下：

	#忽略一个目录
	log
	#忽略一个目录下所有子目录及文件
	log/**/*
	tmp
	tmp/**/*
	public/picts
	public/picts/**/*
	public/download
	public/download/**/*
	db/*.sql
	Thumbs.db
	*~
	#忽略指定后缀的文件
	*.mp3