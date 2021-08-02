[Git Cherry Pick](https://www.atlassian.com/git/tutorials/cherry-pick)
 

git cherry-pick is a powerful command that enables arbitrary Git commits to be picked by reference and appended to the current working HEAD. Cherry picking is the act of picking a commit from a branch and applying it to another. git cherry-pick can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.

When to use git cherry pick
git cherry-pick is a useful tool but not always a best practice. Cherry picking can cause duplicate commits and many scenarios where cherry picking would work, traditional merges are preferred instead. With that said git cherry-pick is a handy tool for a few scenarios...

Team collaboration.
Often times a team will find individual members working in or around the same code. Maybe a new product feature has a backend and frontend component. There may be some shared code between to two product sectors. Maybe the backend developer creates a data structure that the frontend will also need to utilize. The frontend developer could use git cherry-pick to pick the commit in which this hypothetical data structure was created. This pick would enable the frontend developer to continue progress on their side of the project.

Bug hotfixes
When a bug is discovered it is important to deliver a fix to end users as quickly as possible. For an example scenario,say a developer has started work on a new feature. During that new feature development they identify a pre-existing bug. The developer creates an explicit commit patching this bug. This new patch commit can be cherry-picked directly to the main branch to fix the bug before it effects more users.

Undoing changes and restoring lost commits
Sometimes a feature branch may go stale and not get merged into main. Sometimes a pull request might get closed without merging. Git never loses those commits and through commands like git log and git reflog they can be found and cherry picked back to life.

How to use git cherry pick
To demonstrate how to use git cherry-pick let us assume we have a repository with the following branch state:

    a - b - c - d   Main
         \
           e - f - g Feature
git cherry-pick usage is straight forward and can be executed like:

git cherry-pick commitSha
In this example commitSha is a commit reference. You can find a commit reference by using git log. In this example we have constructed lets say we wanted to use commit `f` in main. First we ensure that we are working on the main branch.

git checkout main
Then we execute the cherry-pick with the following command:

git cherry-pick f
Once executed our Git history will look like:

    a - b - c - d - f   Main
         \
           e - f - g Feature
The f commit has been successfully picked into the main branch

Examples of git cherry pick
 git cherry pick can also be passed some execution options.

-edit
Passing the -edit option will cause git to prompt for a commit message before applying the cherry-pick operation

--no-commit
The --no-commit option will execute the cherry pick but instead of making a new commit it will move the contents of the target commit into the working directory of the current branch.

--signoff
The --signoff option will add a 'signoff' signature line to the end of the cherry-pick commit message

In addition to these helpful options git cherry-pick also accepts a variety of merge strategy options. Learn more about these options at the git merge strategies documentation.

Additionally, git cherry-pick also accepts option input for merge conflict resolution, this includes options: --abort --continue and --quit this options are covered more in depth with regards to git merge and git rebase.

Summary
Cherry picking is a powerful and convenient command that is incredibly useful in a few scenarios. Cherry picking should not be misused in place of git merge or git rebase. The git log command is required to help find commits to cherry pick.



一、基本用法
git cherry-pick命令的作用，就是将指定的提交（commit）应用于其他分支。


$ git cherry-pick <commitHash>
上面命令就会将指定的提交commitHash，应用于当前分支。这会在当前分支产生一个新的提交，当然它们的哈希值会不一样。

举例来说，代码仓库有master和feature两个分支。


    a - b - c - d   Master
         \
           e - f - g Feature
现在将提交f应用到master分支。


# 切换到 master 分支
$ git checkout master

# Cherry pick 操作
$ git cherry-pick f
上面的操作完成以后，代码库就变成了下面的样子。


    a - b - c - d - f   Master
         \
           e - f - g Feature
从上面可以看到，master分支的末尾增加了一个提交f。

git cherry-pick命令的参数，不一定是提交的哈希值，分支名也是可以的，表示转移该分支的最新提交。


$ git cherry-pick feature
上面代码表示将feature分支的最近一次提交，转移到当前分支。

二、转移多个提交
Cherry pick 支持一次转移多个提交。


$ git cherry-pick <HashA> <HashB>
上面的命令将 A 和 B 两个提交应用到当前分支。这会在当前分支生成两个对应的新提交。

如果想要转移一系列的连续提交，可以使用下面的简便语法。


$ git cherry-pick A..B 
上面的命令可以转移从 A 到 B 的所有提交。它们必须按照正确的顺序放置：提交 A 必须早于提交 B，否则命令将失败，但不会报错。

注意，使用上面的命令，提交 A 将不会包含在 Cherry pick 中。如果要包含提交 A，可以使用下面的语法。


$ git cherry-pick A^..B 
三、配置项
git cherry-pick命令的常用配置项如下。

（1）-e，--edit

打开外部编辑器，编辑提交信息。

（2）-n，--no-commit

只更新工作区和暂存区，不产生新的提交。

（3）-x

在提交信息的末尾追加一行(cherry picked from commit ...)，方便以后查到这个提交是如何产生的。

（4）-s，--signoff

在提交信息的末尾追加一行操作者的签名，表示是谁进行了这个操作。

（5）-m parent-number，--mainline parent-number

如果原始提交是一个合并节点，来自于两个分支的合并，那么 Cherry pick 默认将失败，因为它不知道应该采用哪个分支的代码变动。

-m配置项告诉 Git，应该采用哪个分支的变动。它的参数parent-number是一个从1开始的整数，代表原始提交的父分支编号。


$ git cherry-pick -m 1 <commitHash>
上面命令表示，Cherry pick 采用提交commitHash来自编号1的父分支的变动。

一般来说，1号父分支是接受变动的分支（the branch being merged into），2号父分支是作为变动来源的分支（the branch being merged from）。

四、代码冲突
如果操作过程中发生代码冲突，Cherry pick 会停下来，让用户决定如何继续操作。

（1）--continue

用户解决代码冲突后，第一步将修改的文件重新加入暂存区（git add .），第二步使用下面的命令，让 Cherry pick 过程继续执行。


$ git cherry-pick --continue
（2）--abort

发生代码冲突后，放弃合并，回到操作前的样子。

（3）--quit

发生代码冲突后，退出 Cherry pick，但是不回到操作前的样子。

五、转移到另一个代码库
Cherry pick 也支持转移另一个代码库的提交，方法是先将该库加为远程仓库。


$ git remote add target git://gitUrl
上面命令添加了一个远程仓库target。

然后，将远程代码抓取到本地。


$ git fetch target
上面命令将远程代码仓库抓取到本地。

接着，检查一下要从远程仓库转移的提交，获取它的哈希值。


$ git log target/master
最后，使用git cherry-pick命令转移提交。


$ git cherry-pick <commitHash>

Origin: https://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html
