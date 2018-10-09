# 学习总结

## What is Git and Github?
Git是目前世界上最先进的分布式版本控制系统,可以对文件进行回溯，查看修改，协同编辑  

GitHub为免费的远程仓库,GitHub还是一个开源协作社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目  


## GIT: Installation, Configuration and First Commit
**到[官网](https://git-scm.com/)进行下载并安装**  

**设置用户名和邮箱**  
设置全局用户名  
`git config--global user.name "name" `  

设置电子邮箱  
`git config--global user.email "email"`  

**创建一个文件夹并切换到文件夹内**  
```
mkdir XXX   
cd XXX
```

**创建一个README.md 自述文件可以使用命令**   
`touch README.md`   

**初始化git**  
`git init `  

**添加文件到临时区域**  
`git add README.md`  

**提交文件到git仓库**  
`git commit -m""`   

**查看文件的修改**  
`git status`  

**查看文件提交历史**  
`git log`   

# GIT: Working with Branches  
**创建一个分支**
`git branch xxx`  

**切换到某分支**
`git checkout xxx`  

```
git commit -am "<message>"相当于git add和git commit -m的组合技前提是被改动文件已经是tracked
```

**查看分支**
`git branch`  

**删除分支**  
`git branch -d dev`  

```
（$ git branch dev创建分支dev，$ git checkout dev切换分支dev这两句话等同于$ git checkout -b dev 一句    )
```
# GIT: Merging and Workflow

**初始化工作流（d 参数表示接受所有默认值）**  

初始化分支 -d 表示均默认值

`git flow init [-d]`

**合并某分支到当前分支**

`git merge XXX`

```
master分支 

最为稳定功能比较完整的随时可发布的代码，即代码开发完成，经过测试，没有明显的bug，才能合并到 master 中。请注意永远不要在 master 分支上直接开发和提交代码，以确保 master 上的代码一直可用；
develop分支

用作平时开发的主分支，并一直存在，永远是功能最新最全的分支，包含所有要发布 到下一个 release 的代码，主要用于合并其他分支，比如 feature 分支； 如果修改代码，新建 feature 分支修改完再合并到 develop 分支。所有的 feature、release 分支都是从 develop 分支上拉的。



feature分支

这个分支主要是用来开发新的功能，一旦开发完成，通过测试没问题（这个测试，测试新功能没问题），我们合并回develop 分支进入下一个 release 。



release分支

用于发布准备的专门分支。当开发进行到一定程度，或者说快到了既定的发布日，可以发布时，建立一个 release 分支并指定版本号(可以在 finish 的时候添加)。开发人员可以对 release 分支上的代码进行集中测试和修改bug。（这个测试，测试新功能与已有的功能是否有冲突，兼容性）全部完成经过测试没有问题后，将 release 分支上的代码合并到 master 分支和 develop 分支。



hotfix分支

用于修复线上代码的bug。从 master 分支上拉。完成 hotfix 后，打上 tag 我们合并回 master 和 develop 分支。



注意事项：


所有开发分支从 develop 分支拉。
所有 hotfix 分支从 master 拉。
所有在 master 上的提交都必要要有 tag，方便回滚。
只要有合并到 master 分支的操作，都需要和 develop 分支合并下，保证同步。
master 和 develop 分支是主要分支，主要分支每种类型只能有一个，派生分支每个类型可以同时存 在多个。 
```

# GIT: Git Flow Feature Branch and Pushing to Github

**生成SSH密匙**

` ·ssh-keygen -t rsa -C "email"`

**连接Github远程仓库**

`git remote add orgin 你的Github仓库地址`

**查看远程库信息**

`git remote -v`

**第一次强制推送master分支的所有内容**

```
git push -u origin master 
```

**推送最新修改**

`git push origin master`

**从GITHUB上克隆一个本地库**

`git clone XXX@github.com:XXXXXX  `

**在文件未提交前查看做出哪些修改操作**

`git diff XXXX文件 `

# GIT: Git Flow and Github Pull Request

**更新本地库**

`git pull`



# supplement

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard 版本号

git reflog查看命令历史

回退到上一个版本git reset --hard HEAD^

git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

git diff HEAD -- 文件名 命令可以查看工作区和版本库里面最新版本的区别：

git checkout -- 文件名 把文件在工作区的修改全部撤销

git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区1

git checkout  test.txt误删的文件恢复到最新版本

删除文件$ git rm test.txt>>$ git commit -m "remove test.txt"

git branch查看分支

-m 注释

--no-ff参数，表示禁用Fast forward

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name

