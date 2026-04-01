## Github 仓库使用

### 关联本地仓库与 GitHub 远程仓库

如果已经有一个本地项目，需要将其与 GitHub 上创建的仓库进行关联。<br>

1.在 GitHub 上创建一个新仓库<br>
- 登录 GitHub，点击右上角的 + 号，选择 New repository。<br>
- 填写仓库名称（例如 my-project），然后点击 Create repository。<br>
- 请勿勾选 "Initialize this repository with a README"，因为我们将在本地初始化并推送。<br>
<br>
2.将本地项目与远程仓库关联<br>
- 打开你的项目所在的本地文件夹，在终端（或命令行）中执行以下命令：
- 初始化本地 Git 仓库 (如果尚未初始化): bash终端符> git init
- 添加远程仓库地址:<br>
- 在 GitHub 仓库页面，点击绿色的 Code 按钮，复制 HTTPS 或 SSH 地址。
- bash终端符> git remote add origin https://github.com/你的GitHub用户名/my-project.git
<br>
<br>
<br>


### 本地修改内容并推送到 GitHub

当你对本地代码进行了修改，可以按照以下流程将更改同步到 GitHub。<br>

##### 1.查看文件状态 / 查看哪些文件被修改了。<br>
bash终端符> git status<br>

##### 2.添加文件到暂存区
将你修改过的文件添加到 Git 的暂存区，准备提交。<br>
添加单个文件: git add <文件名><br>
添加所有修改过的文件: git add .   或者  git add -A<br>

##### 3.提交更改
将暂存区的文件正式提交到本地仓库，并附上本次提交的说明信息。<br>
git commit -m "这里写本次提交的描述，例如：修复了一个bug，或者添加了新功能"<br>

### 后续推送
以后再有修改，重复 第 2 步 (add) -> 第 3 步 (commit) -> git push 即可。<br>
git bash终端执行
git add .<br>
git commit -m "更新了文档"<br>
git push # 因为之前用 -u 关联过，所以现在可以直接用 git push 推送<br>


### 拉取同步
如果直接在 GitHub 网页上修改了内容（例如编辑了文件、合并了 Pull Request 等），<br>
这些更改会反映在远程仓库中，<br>
而本地仓库并没有自动同步这些变化。<br>
为了保持本地仓库与远程仓库的一致性，你需要手动从远程仓库拉取（Pull）最新的更改。<br>

在本地项目目录中打开终端或命令行工具（Git Bash），然后运行以下命令：
git push

<br>
