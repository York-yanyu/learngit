# git 学习

1. git 是最先进的分布式文件管理系统

2. git config 进行全局设置，比如名称，电子邮件

3. 创建一个目录，然后在这个目录里面进行git init初始化，让git来跟踪管理版本库

4. git add  在里面添加文件，可以添加多个

5. git commit -m “abcd” 用这个命令告诉git，把文件添加到仓库，**引号里面要对文件进行说明，方便自己和他人阅读**

6. git status 可以查看文件的状态，文件修改之后会在这个status里面进行显示。

7. git diff 可以查看具体修改了哪些东西。

8. 那么修改完成了，并且通过6，7的命令确认了自己所做的修改，就可以放心进行提交了。用4，5的命令提交，记住一定要在认真填写自己对文件做的修改的说明，这很重要！

9. git log 可以查看，顾名思义就行。（未完待续，“版本回退”）

10. git reset --hard xxxxx    这里如果要回退到上一个版本，应该写HEAD^；上上一个版本，HEAD^^；以此类推。
    如果又反悔了，可以找到修改版本的id号，前5位或更多，就可以回到那个版本；如果不小心关掉了，可以通过git reflog 看到自己所有的操作，里面有自己想要的id信息。

11. 工作区、暂存区、版本库

12. 将本地库和远程库（github）关联起来，才能发挥git的最大优势。

13. git remote add origin  https://github.com/York-yanyu/learngit.git
    git push -u origin master
    以后每次提交只需要输入git push origin master，就可以将本地做的修改什么的都提交到远程库

    也可以现在远程端新建一个repository，然后克隆到本地

    git@github.com:York-yanyu/gitskill.git

    说明：http和ssh都可以用，但是http会比较慢，使用ssh协议的会比较快，这要看具体情况而定。

14. 查看分支：git branch

    创建分支：git branch <name>

    切换分支：git checkout <name>

    创建+切换分支：git checkout -b <name>

    合并某分支到当前分支：git merge <name>

    删除分支：git branch -d <name>

    分支的作用及逻辑说明：创建一个分支，在分支上做修改或者进行添加。当你从分支切换回到master上时，master上还是原来的。也就是说，比如我工作做到一个点A，接下来我要到B，我不在master这个分支上做，而是另外开一个分支，在那个分支上做完没问题，把分支合并到master上，那么master就到了B，Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。