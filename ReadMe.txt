learn content:
git add filename
git commit -m "***"//注释
git status //查看当前文件的状态
git diff//查看不同
git diff HEAD -- filename //可以查看工作区和版本库之间的差别，HEAD位于版本库
git reset --hard HEAD^//回到前一个版本
git reset --hard HEADID//回到指定的版本
git log //查看当前的所有操作
git reflog //查看所有操作
git config global core.autocrlf true //将windows下的回车+换行CRLF自动改成linux下的LF
git config --global core.ui true
git checkout -- filename//将文件在工作区中的修改全部都撤销，撤销后回到版本库一模一样的状态；
git reset HEAD filename //将放入暂存区的修改撤销重新放回工作区
git rm filename //在工作区中删除文件

ssh-keygen -t rsa -C "youremail@example.com" //生成一个SSH密钥
//将密钥加入到github本地的ssh key中
git remote add origin git@github.com:Akirualuka/learngit.git//在github创建一个远程库
git push -u origin master//(第一次)将本地库的内容推送到远程库
git push origin master//之后推送

git remote rm <name>//该名字是远程库的名字，为之前远程创建远程库的名字
git remote -v //显示当前存在的远程库信息

git clone git@github.com:Akirualuka/<库名字>.git//将远程库克隆到本地库的当前位置
git checkout -b dev origin/dev将远程库中的dev分支下载到本地库中

分支：
git branch name //创建一个分支name
git checkout name //切换到name这个分支
上两个指令相当于
git checkout -b name

还有一种创建分支的方法：
git branch name  创建分支
git switch name  切换分支
git switch -c name 创建并切换到分支name

git branch 查看当前的分支和当前所在的分支
在master分支中输入git merge dev将dev分支合并到master中
相当于master直接指向devHEAD指向master

git branch -d dev 删除dev分支

分支解决冲突问题：
问题描述：创建一个分支，在分支中修改了文件后在master分支中同样修改了文件，
最后在merge合并分支时两个分支产生了冲突
需要将更改的内容一致才能使用merge合并两个分支
查看分支的创建和处理过程
git log --graph --pretty=oneline --abbrev-commit
git log --graph  图形化log过程

gitee 与git的管理使用remote这些

原理讲解：
git的版本库是什么东西
所有的git操作都是基于版本库，版本库不是工作区，类似于功能区
版本库中有一个重要的东西
叫做stage的暂存区，暂存区中有git为我们自动创建的分支master
，指向master的指针就是HEAD

把文件写入版本库中一共有两步
1：使用git add 将文件放入暂存区中
2:git commit将暂存区中的内容提交到当前的分支中
git 将所有修改的文件都存在暂存区中，通过commit一次性将所有内容提交上去

git 跟踪和管理的是修改并不是文件


问题描述：
在dev执行工作时出现突发的事情，但是工作没做完不能提交，这是需要将当前工作区存储起来在别的分支进行其他事情
git 提供了stash功能，能将工作现场存储起来，等将来要用时继续恢复工作
git stash //把当前工作区存储起来等以后恢复现场再继续工作
git stash apply //将stash内容恢复但是被删除stash
git stash drop //删除该stash
前两行代码可以等效为
git stash pop

git stash list//查看当前存在的stash

有多个stash时使用git stash apply stash@{2}可以恢复指定的stash内容
如果有多个分支都存在bug但是只提交了master这个分支，如何将这个修改同步到其他存在相同问题的分支中呢？？
git中使用cherry-pick来同步分支的部分修改而不将整个分支merge过来
git cherry-pick <commit ID>

当在一个分支上commit后，回到dev没有合并分支删除时会不让我们删
这是需要使用 git branch -D branchname

分支概念的引入
分支：每一次版本变化构成一个时间线，一个时间线就是一个分支。
主分支为master，HEAD严格来说是指向master的指针，
git用master指向最新的提交点，再用HEAD指向这个master，每次提交master都会向前移动一步

创建新的分支：
再master的位置创建一个分支dev，再把HEAD指向dev这就创建了一个分支
此时有两个分支，HEAD指向哪里旧表示在那个分支
，如果在dev分支上继续修改版本的操作就是：dev指针往前移动，HEAD指针指向dev分支的最新的修改位此时有两个分支，HEAD指向哪里旧表示在那个分支
，如果在dev分支上继续修改版本的操作就是：dev指针往前移动，HEAD指针指向dev分支的最新的修改位置

如何将分支合并
只需要将master指针指向dev当前的位置就可以实现分支合并，最后将dev的指针删除就只剩下一个master分支

分支管理策略：
在合并分支时使用的是git merge name,这是一种Fast forward 模式，
这种模式在删除分支时会丢掉分支信息
使用git merge --no-ff -m "  " dev本次合并后提交一个commit

一般情况下，在dev分支上修改，master分支作为发布版本
工作分支合并到dev分支中，发布时将dev分支合并到master中
使用git merge --no-f -m "dasdasd" dev

