Git 高级操作
===========

## 冲突合并

当两个开发者修改了同一个文件的同一行时，一人先提交了本地版本后；另一人先在本地提交了修改，然后在拉取（pull或pull rebase时）远程版本时，这时发生冲突。

### 合并工具

#### TortoiseGit

参见系列截图`TortoiseGit/merge`，说明如下：

- TortoiseGit_merge_step1.png  
  拉取时产生冲突，Explorer项目文件夹上出现三角警示图标
  
- TortoiseGit_merge_step2.png  
  在项目文件夹中，找到带有三角警示图标的文件（包含冲突的文件），右键菜单`TortoiseGit`子菜单选择`编辑冲突`
   
- TortoiseGit_merge_step3.png  
  在TortoiseGit冲突合并工具中，在每一处冲突处，在下方（合并结果编辑区）的红色区域右键菜单选择：
  - 使用“他们的文本块”：这一处冲突采用远程版本
  - 使用“我的文本块”：这一处冲突采用本地版本
  
  ***也可直接手工编辑产生合并结果。一处冲突解决后，移动到下一处冲突同样处理，直到完成。***

- TortoiseGit_merge_step4.png  
  当一个文件内的冲突编辑好后，点左上角的保存按钮，此时会弹出一个对话框，询问“你是否想标记文件……为已解决的”，此时建议选择`No`。
  
- TortoiseGit_merge_step5.png  
  当所有冲突文件全部编辑好后，此时回到项目文件夹，右键菜单`TortoiseGit`子菜单选择`解决冲突`
  
- TortoiseGit_merge_step6.png  
  点击解决冲突后，就可以提交合并以后的版本了，本地提交后可以直接把这个合并后的版本推送（push）到远端

## 衍合（Rebase）

### 1 定义
Rebase，顾名思义，就是重新定义（re）基准（base）的作用，即**重新定义某个分支的参考基准**。这里的基准（base）是指产生分支的那个commit对象，rebase也就是对分支而言，把它的base修改成其他commit对象。

### 2 命令

- rebase的基本指令是`git rebase <commit ID>`，也就是把当前分支的分叉点改为一个指定的commit对象。

- 另一种形式是`git rebase <branch name>`，这种格式时，commit对象是用分支名称来指定——即使用指定分支的HEAD commit对象。

### 3 过程

要搞清楚这个东西，要先看看版本库状态切换的两种情况：

1. 我们知道，在某个分支上，我们可以通过`git reset`，实现将当前分支切换到本分支以前的任何一个版本状态，即所谓的“回溯”。即实现了本分支的“后悔药”。也即版本控制系统的初衷。

2. 还有另一种情况，当我们的项目有多个分支的时候。我们除了在本地开发的时候可能会“回溯”外，也常常会将和自己并行开发的别人的分支修改添加到自己本地来。这种情况下很常见。作为项目管理员，肯定会不断的合并各个子项目的补丁，并将最新版本推送到公共版本库，而作为开发人员之一，提交自己的补丁之后，往往需要将自己的工作更新到最新的版本库，也就是说把别的分支的工作包含进来。

例如，如果我要让test分支（从与master分支处开始）所有的改变都添加到master分支来，使得master分支包含test分支的所有修改：

	git checkout master
	git rebase test
	
***这个过程，git都做了些什么呢？***
>1. 先将test分支的代码checkout出来，作为工作目录
>2. 然后将master分支从test分支创建起的所有改变的补丁，依次打上。如果打补丁的过程没问题，rebase就搞定了
>3. 如果打补丁的时候出现了问题，就会提示你处理冲突。
处理好了，可以运行`git rebase --continue`继续直到完成

>4. 如果你不想处理，你还是有两个选择，一个是放弃rebase过程（运行`git rebase --abort`），另一个是**直接用test分支的取代当前分支**的（`git rebase –-skip`）。

## 衍合、合并分支的常用选项

### rebase的交互模式

`git rebase -i <commit ID>`

在此模式下，可以对rebase过程中进行干预，从而修改版本的历史，包括提交内容和提交的说明都可以改。


### onto选项

`git rebase --onto  <new base-commit> <current base-commit>`

将当前分支的从*current base-commit*开始后的commit序列改到基于*new base-commit*上

### no-ff选项

`git merge --no-ff newfeature`

这一选项使得合并时总是创建一个新的提交对象, 即使在这种合并可以在当前分支上以快进方式（ff，fast-forward）完成时。这样做的好处是确保记录下所有分支创建——合并的历史信息。
