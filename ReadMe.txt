learn content:
git add filename
git commit -m "***"//注释
git status //查看当前文件的状态
git diff//查看不同
git reset --hard HEAD^//回到前一个版本
git reset --hard HEADID//回到指定的版本
git log //查看当前的所有操作
git reflog //查看所有操作
git config global core.autocrlf true //将windows下的回车+换行CRLF自动改成linux下的LF

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
//该行是测试
