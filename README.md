# Github 与 Git 的区别：

- Git是一个版本控制软件，电脑不联网的情况下也可以使用，用于处理本地的“仓库”（其实就是文件夹和文件夹内的文件）
- Github是一个托管平台，我们可以将我们本地的“仓库”上传至该平台储存，可以看作是一个云盘，只不过这个云盘上对公众开放的（开源）
- 我们托管在Github上的“仓库”和本地的“仓库”是一一对应的关系，我们可以使用Git作为连接两个“仓库”的媒介（使用Git管理本地仓库、使用Git将本地仓库推送、更新到Github、将Github仓库克隆到本地、使用Git从Github仓库更新本地仓库）

# Tips

- 所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。Microsoft的Word格式是二进制格式，版本控制系统是没法跟踪Word文件的改动的。如果要真正使用版本控制系统，就要以纯文本方式编写文件。

# 常用命令

- git init 初始化一个Git仓库
- git status 查看当前的状态
- git diff 查看工作区和暂存区差异
- git diff --cached 查看暂存区和仓库差异
- git diff HEAD 查看工作区和仓库的差异
- 添加文件到Git仓库，分两步：
  1. git add 文件名
  示例：
  git add file1.txt # 添加单个文件
  git add file2.txt file3.txt # 添加多个文件
  git add . # 添加当前目录的所有文件到暂存区(Stage)
  2. git commit 将暂存区(Stage)的文件提交到仓库
  示例：
  git commit -m "提交说明"
- cat &lt;文件名&gt; 可以查看文件内容
- git log 显示从最近到最远的提交日志,如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数
- git reflog 显示对版本的操作记录，可用于查看 commit_id
- git reset --hard HEAD^ 从当前版本回退到上一个版本。HEAD指向的版本就是当前版本，往上100个版本写100个^比较容易数不过来，所以写成HEAD~100，也可以使用git reset --hard commit_id。
- git checkout -- &lt;文件名&gt; 把文件在工作区的修改全部撤销，这里有两种情况：一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或git add时的状态。



- git push 推送至远程仓库
- git clone 获取远程仓库


