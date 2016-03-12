新手必读
=======

## 1. 本机安装Git软件

### Windows用户

#### 基本安装 
Windows用户首先需安装Git官方的Git for Windows（msysgit），[下载地址](http://msysgit.github.io)

#### 图形界面
Windows如需使用图形界面进行Git操作的，建议在完成上一步后安装

- TortoiseGit，[下载地址](https://code.google.com/p/tortoisegit/wiki/Download)

- SourceTree，[下载地址](http://www.sourcetreeapp.com)



### 其他系统用户

Linux/Unix系统用户建议用包管理器安装，包管理器不可用者下载Git源码构建。 

- Ubuntu/Debian: `sudo apt-get install git git-core`
- RedHat/CentOS/Fedora: `sudo yum install git`
- Mac OS X: 系统自带，但不是最新版本，建议用第三方包管理器安装最新版

	- 如安装了HomeBrew包管理器，执行：`brew install git`
	- 安装了MacPorts包管理器，执行：`sudo port install git`

## 2. 配置Git环境

以下命令请在一个Bash窗口内执行，Windows用户请打开msysgit安装的Git Bash程序。 

1. `git config --global user.name "你的用户名"`
2. `git config --global user.email "你的邮件地址"`
3. `git config --global color.ui "auto"`
4. `git config --global push.default simple`
5. `git config --global core.editor 用来写提交备注的编辑器` ，例如：  

使用Vim：

     git config --global core.editor  vim
     
或：

     git config --global core.editor  emacs

**特别**：对于Windows用户，建议安装Notepad++，然后设置notepad++为Git默认编辑器：

     git config --global core.editor  notepad++

**注**：

1. 首先要安装Notepad++  
2. 打开Notepad++，首选项->新建，格式选Unix，编码选UTF-8（无BOM），勾选“应用于打开ASCII文件”，关闭退出
3. 使notepad++在Git Bash的执行路径中可找到，假如Notepad++安装在默认路径，则配置方法如下：

     echo 'export PATH="/c/Program Files/Notepad++":$PATH' >> /etc/profile
     

## 3. 配置冲突解决工具

推荐使用DiffMerge作为冲突解决工具，[下载地址](http://www.sourcegear.com/diffmerge/downloads.php)  
具体配置如下。

### Windows环境下配置


    git config --global merge.tool diffmerge
    $ git config --global mergetool.diffmerge.cmd "'C:/Program Files/SourceGear/Common/DiffMerge/sgdm.exe' -merge -result=\"\$MERGED\" \"\$LOCAL\" \"\$BASE\" \"\$REMOTE\""
    git config --global mergetool.keepBackup false
    git config --global diff.tool diffmerge
    git config --global difftool.diffmerge.cmd "'C:/Program Files/SourceGear/Common/DiffMerge/sgdm.exe' \"\$LOCAL\" \"\$REMOTE\""
	
**注**：有时因Bash命令书写问题导致向配置文件中写入错误，请查看`~/.gitconfig`（即用户主目录下`.gitconfig`）文件，直接修改有关部分，对照如下：

	[merge]
		tool = diffmerge
	[mergetool "diffmerge"]
		cmd = 'C:/Program Files/SourceGear/Common/DiffMerge/sgdm.exe' -merge -result=\"$MERGED\" \"$LOCAL\" \"$BASE\" \"$REMOTE\"
		keepBackup = false
	[diff]
		tool = diffmerge
	[difftool "diffmerge"]
		cmd = 'C:/Program Files/SourceGear/Common/DiffMerge/sgdm.exe' \"$LOCAL\" \"$REMOTE\"
 


### Mac OS X下配置

    git config --global merge.tool diffmerge
	git config --global mergetool.diffmerge.cmd "/Applications/DiffMerge.app/Contents/MacOS/diffmerge --merge --result=\$MERGED \$LOCAL \$BASE \$REMOTE"
	git config --global mergetool.keepBackup false
 	git config --global diff.tool diffmerge
	git config --global difftool.diffmerge.cmd "/Applications/DiffMerge.app/Contents/MacOS/diffmerge \$LOCAL \$REMOTE"
	

### DiffMerge默认语言设为UTF-8

1. 打开DiffMerge程序
2. 进入Tools -> Options菜单，编辑Default Ruleset
3. Character Encodings项，去掉“Search for unicode BOM”的勾选，选中“Use Named Character Encoding Below”，下拉框选择UTF-8，确定退出

### SourceTree与DiffMerge集成设置

#### 设置

打开Sourcetree应用，主菜单选择：`工具`->`选项`->`比较`->`外部差异比对/合并`，在此设置处，`外部比对工具`和`合并工具`两个下拉选择框，都选中`DiffMerge`

#### 用法

当用SourceTree进行操作，出现冲突文件时，在文件变更列表窗口中会出现带有惊叹号标记的文件，右键点击这种文件，在右键菜单中选择：`解决冲突`->`打开外部合并工具`

## 4. 配置SSH通信密钥

在Bash窗口内执行： 
 
     ssh-keygen -q -N '' -t rsa -f ~/.ssh/id_rsa


## 5. 验证环境可用

### (1)Git服务器HTTP可访问

1. 登录[http://192.168.1.12:8080](http://192.168.1.12:8080)，Windows用户建议使用Firefox或Chrome浏览器最新版。
2. 顶部菜单点击`Your Profile` --> `SSH Keys` --> `Add new`,  然后把以下文件内容粘贴进去提交：

> 你的用户HOME目录/.ssh/id_rsa.pub

###  (2)Git服务器SSH可访问

3. 在Bash窗口中执行以下命令，全部成功表明环境OK：


		git clone git@192.168.1.12:frank/git-tutorial.git
        cd git-tutorial
        touch 你的git服务器登录名.txt
        git add .
        git commit -a
        (这里应该打开你前面设置的编辑器，随便写一句话，保存退出)
        git push
        git rm 你的git服务器登录名.txt
        git commit -a -m "Delete test file"
        git push


4.  请阅读git-tutorial项目中的git_commands.md文件（Markdown格式），特别是注意`文件忽略`部分


##  附：Git学习资料

使用本系统，需要以下知识： 

- Git
- Markdown