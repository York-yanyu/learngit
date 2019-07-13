# git 学习

> 学习资源为**廖雪峰官方网站的git教程**

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

15. 分支的具体应用场景：

    （1）冲突
    分支和主干同时修改同一个东西，然后merge，肯定会出现问题，那么它会提醒，然后自己具体问题具体分析，解决冲突，再提交就OK了。
    （2）分支管理
    如果用git merge <name>，会使用fast forward进行合并，这样导致合并以后丢失分支信息；可以使用git merge --no-ff -m "xxxxx" <name>进行合并，在用较好的格式查看log的时候，能看到比较清晰的合并路线。
    （3）分支管理策略

    在实际开发中，我们应该按照几个基本原则进行分支管理：

    首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

    那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

    你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

    所以，团队合作的分支看起来就像这样：

    ![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

    （4）bug管理

    现在操作都明白了，关键是要熟悉逻辑：
    1 发现一个bug，但是手头的工作只进行了一半，没有提交；

    2 git stash把当前的工作存起来；

    3 看要在哪个分支上修复bug，切换到那条分支，创建一个新的bug分支（起一个名字）进行bug修复，add，提交；

    4 再把修改好的bug，合并到该分支，bug修复完成；

    5 回到之前自己工作的分支，要把刚才存储起来的工作释放出来，先查看git stash list；再释放，git stash pop（释放并且删除存进去的）或者 git stash apply ...(具体list中的哪个，但是还在list上，要用git stash drop将信息删除)

    （5）开发新的feature

    新建一个分支来开发新的特征，完了，再合并到一个较为主要的分支上去。

    没有合并过的分支可以通过 ' git branch -D <name> ' 强行删除。

    （6）多人协作的逻辑：

    1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
    2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
    3. 如果合并有冲突，则解决冲突，并在本地提交；
    4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

    如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

    这就是多人协作的工作模式，一旦熟悉了，就非常简单。

    小结：

    - 查看远程库信息，使用`git remote -v`；
    - 本地新建的分支如果不推送到远程，对其他人就是不可见的；
    - 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
    - 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
    - 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
    - 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

16. 标签
    为什么要设定标签，因为标签比commit号更直观，方便管理和查看。但其实就是和commit的id号相关联。
    关于标签的命令操作：

    * 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
    * 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
    * 命令`git tag`可以查看所有标签；
    * 命令`git push origin <tagname>`可以推送一个本地标签；
    * 命令`git push origin --tags`可以推送全部未推送过的本地标签；
    * 命令`git tag -d <tagname>`可以删除一个本地标签；
    * 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签；

17. 如何参与github上的开源项目：

    1. 可以访问它的项目主页<https://github.com/twbs/bootstrap>，点“Fork”就在自己的账号下克隆了一个bootstrap仓库
    2. 然后，从自己的账号下clone：
    3. 一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址`git@github.com:twbs/bootstrap.git`克隆，因为没有权限，你将不能推送修改。
    4. Bootstrap的官方仓库`twbs/bootstrap`、你在GitHub上克隆的仓库`my/bootstrap`，以及你自己克隆到本地电脑的仓库，他们的关系就像下图显示的那样：

    ```ascii
    ┌─ GitHub ────────────────────────────────────┐
    │                                             │
    │ ┌─────────────────┐     ┌─────────────────┐ │
    │ │ twbs/bootstrap  │────>│  my/bootstrap   │ │
    │ └─────────────────┘     └─────────────────┘ │
    │                                  ▲          │
    └──────────────────────────────────┼──────────┘
                                       ▼
                              ┌─────────────────┐
                              │ local/bootstrap │
                              └─────────────────┘
    ```

    5. 如果你想修复bootstrap的一个bug，或者新增一个功能，立刻就可以开始干活，干完后，往自己的仓库推送。
    6. 如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。

18. 一些关于git配置的一些小技能，可以帮助简化git的使用，并且让自己库看上去更加美观整洁。