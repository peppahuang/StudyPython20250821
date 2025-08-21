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
