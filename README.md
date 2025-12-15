# Github 与 Git 的区别：

- Git是一个版本控制软件，电脑不联网的情况下也可以使用，用于处理本地的“仓库”
- Github是一个托管平台，我们可以将我们本地的“仓库”上传至该平台储存，可以看作是一个云盘，只不过这个云盘上对公众开放的（开源）
- 我们托管在Github上的“仓库”和本地的“仓库”是一一对应的关系，我们可以使用Git作为连接两个“仓库”的媒介（使用Git管理本地仓库、使用Git将本地仓库推送、更新到Github、将Github仓库克隆到本地、使用Git从Github仓库更新本地仓库）

# Tips

- 所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。Microsoft的Word格式是二进制格式，版本控制系统是没法跟踪Word文件的改动的。如果要真正使用版本控制系统，就要以纯文本方式编写文件。

# 常用命令

- `git init`：在当前文件夹内初始化一个Git仓库
- `git status`：查看仓库当前状态
- 添加文件到Git仓库，分两步：
    1. `git add 文件名`：添加文件到暂存区(Stage)  
    示例：  
    git add file1.txt # 添加单个文件  
    git add file2.txt file3.txt # 添加多个文件  
    git add . # 添加当前目录的所有文件到暂存区(Stage)  
  2. `git commit -m "提交说明" `：将暂存区(Stage)的文件提交到git仓库
- `git remote add origin REMOTE-URL`：建立git仓库与远程仓库的链接关系,关联一个远程仓库时必须给远程库指定一个名字，origin是默认习惯命名
- `git remote -v`：验证远程 URL 设置是否正确，设置正确则会出现以下提示
  ```
  origin  git@github.com:username/repository.git (fetch)
  origin  git@github.com:username/repository.git (push)
  ```
- `git remote set-url origin REMOTE-URL`：更新远程仓库地址
- `git remote rm origin`：解除本地仓库和远程仓库的链接关系，删除后，运行 `git remote -v` 检查是否已成功解除，输出应该为空。
- `git push -u origin main`：将本地 main 分支推送至远程仓库 origin  
  加了参数-u后，以后即可直接用`git push`代替`git push origin master`，相当于记录了push到远端分支的默认值，这样当下次我们还想要继续push的这个远端分支的时候推送命令就可以简写成`git push`即可。但是前提是，第一次提交需要加 -u参数，后面的提交就直接可以 `git push`
- `git clone [<选项>] <远程仓库地址> [<本地目录>]`：git clone 是 Git 中用于从远程仓库复制代码到本地的命令。它不仅会下载整个代码库的内容，还会包括**所有的版本历史记录（.git 元数据）**。克隆完成后，本地仓库将自动与远程仓库关联。不制定`[<本地目录>]`将会自动复制到当前目录。
  ```
  git clone --branch branch_name <远程仓库地址> [<本地目录>] : 默认情况下，git clone 会克隆默认分支（通常是 main 或 master）。要克隆特定分支，可以使用 --branch 或 -b 选项
  git clone --depth 1 <远程仓库地址> [<本地目录>] : 只克隆当前仓库的代码，而不需要完整的版本历史
  ```
- `rm -rf .git`:删除本地 git 仓库
- `git diff`：查看工作区和暂存区差异
- `git diff --cached`：查看暂存区和仓库差异
- `git diff HEAD`：查看工作区和仓库的差异
- `cat 文件名`：可以查看文件内容
- `git log`：显示从最近到最远的提交日志,如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数
- `git reflog`：显示对版本的操作记录，可用于查看 commit_id
- `git reset --hard HEAD^`：从当前版本回退到上一个版本。HEAD指向的版本就是当前版本，往上100个版本写100个^比较容易数不过来，所以写成HEAD~100，也可以使用git reset --hard commit_id

## .gitignore 文件——如何在 Git 中忽略文件和文件夹

通常，一个 `.gitignore` 文件会被放在仓库的根目录下。

- 忽略文件和文件夹

  ``` 
  # 忽略所有.a文件 
  *.a 
  # 但不忽略 lib.a 
  !lib.a 
  # 只忽略项目根目录下的 TODO 文件，不包括子目录 
  /TODO 
  # 忽略 build/ 目录下的所有文件 
  build/ 
  # 忽略 doc/notes.txt 
  doc/notes.txt 
  忽略所有 .log 文件
  *.log：
  ```

- 忽略已提交的文件  
  如果文件已经被 Git 追踪，需要两步：
  - 从索引中移除 (保留本地文件):
    ```
    git rm --cached <文件名或目录名>
    ```
  - 将该文件/目录添加到 .gitignore 中，再提交 .gitignore。
    ```
    echo "*.log" >> .gitignore
    git add .gitignore
    git commit -m "Stop tracking log files"
    ```

# 如何将一个本地已有文件夹的内容上传到 Github
Git的下载安装与配置请参考其他教程  

1. 在 Github 上建立同名 repository  
为避免错误，请勿使用 README、许可或 gitignore 文件初始化新存储库。([参考：使用 Git 将本地存储库添加到 GitHub](https://docs.github.com/zh/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github))

2. 打开终端，切换到文件夹目录
    ```
    cd 文件夹地址
    ```
3. 初始化 Git 仓库
    ```
    git init
    ```
4. 添加文件到 Git暂存区  
    ```
    git add 文件名  
    示例：
    git add file1.txt # 添加单个文件
    git add file2.txt file3.txt # 添加多个文件 
    git add . # 添加当前目录的所有文件到暂存区
    ```
5. 提交到本地仓库
   ```
   git commit -m "提交说明"
   ```
6. 链接远程仓库(将 REMOTE-URL 替换为 GitHub 上的存储库完整 URL)
   ```
   git remote add origin REMOTE-URL 
   ```
   使用 git remote -v 验证远程 URL 设置是否正确
7. 将本地仓库推送到 Github
   ```
   git push -u origin main # 第一次推送，后续推送只需 git push
   ```