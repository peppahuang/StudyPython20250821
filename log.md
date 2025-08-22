在编辑框中直接输入文字，并通过 Markdown 语法格式化，例如：  
标题：用 # 开头（# 一级标题、## 二级标题 等）  
列表：用 - 或 * 开头（- 列表项1）  
链接：[显示文本](链接地址)（如 [GitHub](https://github.com)）  
代码块：用 包裹（python 开头可指定语言高亮）  
粗体 / 斜体：**粗体**、*斜体*  
[官方教程](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

# 20250821
## Git  
[liaoxuefeng](https://liaoxuefeng.com/books/git/install-git/index.html)  
### 1. 配置git
- 查看git版本 in terminal`git -v`
- 配置git  
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
- build repository  
1. mkdir  
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```  
2. turn dir to git repository`git init`
then 
> Initialized empty Git repository in E:/FanweiCode/LearningCode/.git/


### 2. 文件add和修改
#### a. 添加文件  
- add file to git repository`git add readme.txt`  
then write commit`git commit -m "wrote a readme file"`  
then  
> [master (root-commit) eaadf4e] wrote a readme file  
 1 file changed, 2 insertions(+)  
 create mode 100644 readme.txt
> 可以add多次，commit一次
- 查看当前库状态`git status`  
- 查看文件修改情况`git diff filename`
#### b. 版本回滚  
- 查看记录`git log`
- 版本回退`git reset --hard HEAD^`  

> 1. HEAD: 当前版本  
> 2. HEAD^: 上一版本  
> 3. HEAD~n: 前n个版本  

上一个版本的已提交状态`--hard`  
上一个版本未提交状态`--soft`  
上一个版本已添加但未提交状态`--mixed`  

> 其实状态的回滚只是指针的移动  

记录每一次命令: `git reflog`  

#### c. 版本库repository & 工作区 working directory
- 工作区->add->暂存区->commit->版本库
- 查看工作区和版本库里面最新版本的区别`git diff HEAD -- readme.txt`
- 丢弃工作区的修改`git checkout -- file`
> 如果修改后没有放到暂存区，就撤回到和版本库一样的状态  
> 如果已经add到暂存区之后又修改了，这句话是撤回到暂存区后面的状态  
- 如果已经add没有commit，可以使用一下命令先把暂存区的数据回退到工作区：  
`git reset HEAD <file>`  
- 然后再使用`git checkout -- <file>`丢弃工作区的修改  

#### d. 删除文件  
- 系统中删除  `rm <filename>`
- 系统中删除后从版本库中删除  `git rm <filename>` 并且需要commit  
- 本地误删文件后恢复  `git checkout -- <filename>`


### 3. 远程仓库
- 创建SSH KEY（和远程仓库通过SSH加密）  
`ssh-keygen -t rsa -C "youremail@example.com"`

- 把本地内容推送到库里
`git remote add origin git@github.com:youername/learngit.git`
- 远程库名字默认为origin  推送本地库的内容到远程库上
`git push -u origin master`
- 推送最新修改至github
`git push origin master`
- 克隆一个库到本地
`git clone git@github.com:michaelliao/gitskills.git`


### 4. 分支  
- 创建并切换到dev分支  `git checkout -b dev`  （-b参数表示创建并切换）
- 创建分支  `git branch <branchname>`
- 切换分支 `git checkout <branchname>`
<img width="808" height="98" alt="image" src="https://github.com/user-attachments/assets/0ed33d20-150d-412d-ac92-4e7a0f4a8a27" />  

- 查看所有分支`git branch`
- 把分支dev工作成果合并到master上  `git merge dev`
- 删除dev分支  `git branch -d dev`
#### switch操作（切换和新建分支）  
新建并且切换分支  `git switch -c dev`  
切换到已经有的分支  `git switch master`  
#### 解决冲突  
在两个分支上面的修改不同出现冲突，merge就出错  
使用  `git status`  查看冲突  
查看分支合并情况  `git log --graph --pretty=oneline --abbrev-commit`  

- fast forward模式在删除分支之后会丢掉分支信息
如果强制禁用了ff模式，就会在merge的时候生成一个新的commit，从分支历史上可以看到分支信息
`git merge --no-ff -m "merge with no-ff" dev`


#### bug分支  
储藏当前工作现场  `git stash`  
> Saved working directory and index state WIP on master: 0c4ab1a merge with no-ff
查看工作现场  `git stash list`
恢复工作现场：
> `git stash apply`  恢复不删除，用  `git stash drop`  删除
> `git stash pop`  恢复且删除
> 恢复指定的stash  `git stash apply stash@{0}`
> 复制master分支下修复的bug到dev分支：`git cherry-pick 4c805e2`


# 20250822
## Git  
[https://liaoxuefeng.com/books/git/install-git/index.html](https://liaoxuefeng.com/books/git/branch/feature/index.html)  
### 4. 分支  
- feature分支  
强行删除分支
`git branch -D <branch name>`  
- 多人协作
查看远程库内容  `git remote`
查看远程库内容（详细）  `git remote -v`
推送分支  `git push <remote branch> <要推送分支>`
- 创建和远程一样的分支
`git checkout -b dev origin/dev`
- 建立本地分支和远程分支的关联  `git branch --set-upstream branch-name origin/branch-name`
- 本地分支提交历史整理成直线  `git rebase`  

### 5. 标签管理tag  
tag:把一个名字和commit进行绑定  
1. 切换到需要打标签的分支
2. 打标签  `git tag <tagname>`  默认打在最新的commit  
3. 查看所有标签  `git tag`
4. 对某个id 的commit打标签  `git tag <tagname> <commit id>`
5. `-a`：指定标签名  `-m`：指定说明文字  `git tag -a v0.1 -m "version 0.1 released" 1094adb`
6. 查看标签信息  `git show <tagname>`
7. 删除未推送标签  `git tag -d <tagname>`
8. 推送标签到远程  `git push origin <tagname>`
9. 推送所有标签到远程  `git push origin --tags`
10. 删除已推送标签  `git tag -d <tagname>`  再删除远程的  `git push origin :refs/tags/<tagname>`


### 6. gitee
同时关联两个远程 `git remote add <name1> ssh1`  `git remote add <name2> ssh2`  
删除远程  `git remote rm <name>`
