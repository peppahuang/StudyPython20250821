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
- 查看git版本 in terminal  
`git -v`
- 配置git  
```
$ git config --global user.name "Your Name"
`$ git config --global user.email "email@example.com"
```
- build repository
1. mkdir  
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```  
2. turn dir to git repository
```
git init
```
then 
> Initialized empty Git repository in E:/FanweiCode/LearningCode/.git/  
3. add file to git repository
`git add readme.txt`
then write commit  
`git commit -m "wrote a readme file"`
then  
> [master (root-commit) eaadf4e] wrote a readme file  
 1 file changed, 2 insertions(+)  
 create mode 100644 readme.txt
> 可以add多次，commit一次
- 查看当前库状态
`git status`  
- 查看文件修改情况  
`git diff filename`  
- 查看记录
`git log`
- 版本回退
