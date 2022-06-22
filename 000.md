1. 配置用户信息

   `git config --global user.name 'your name'`

   `git config --global user.email 'your email'`

2. 全局配置信息
   1. `C:/Users/用户名文件夹/.gitconfig`
   2. `git config --list --global`查看所有配置信息
   3. `git config user.name`
   4. `git config user.email`

3. 获取帮助信息
   1. `git help config`
   2. `git config -h`  简洁的输出信息

4. 如何创建本地仓库

   1. 目标：将本地项目转化为git仓库
      1. 将本地目录转化为git：切换到对应目录下面运行命令`git init`
         * 手动切换到目录该目录下面
         * 在目录下面右键，点击`git bash`菜单
         * 命令行里面输入`git init`回车即可

   1. clone远程仓库

5. 查看仓库状态

   1. `git status`
   2. 简洁的方式查看仓库状态 `git status -s`

6. 让git跟踪新文件

   **git add 会把文件提交到暂存区**

   1. `git add <文件名>`
   2. ❤️`git add .`跟踪所有文件

7. 提交git本地仓库

   1. `git commit -m '提交信息'`

8. 撤销对文件的修改

   1. 🍎撤销工作区的修改`git checkout -- 要撤销的文件`
   2. 撤销暂存区的改动`git reset HEAD 文件名` `git reset HEAD .`

9. 直接从工作区 ==> git仓库

   1. `git commit -a -m '提交信息'`

10. **从git仓库删除文件**

    1. 删除git仓库的文件，并且不保存本地工作区(仓库里的文件这时候还没有删除，下次commit才会真正删除)

       `git rm -f 文件`

    2. 删除git仓库文件，并且文件保存在工作区

       `git rm --cached 文件`

       

11. 查看提交记录

       1. `git log`

       2. `git log -2`

       3. `git log -2 --pretty=oneline`

       4. `%h 提交的简写哈希值  %an 作者名字  %ar 作者修订日志  %s 提交说明`

          `git log -2 --pretty=format:"%h | %an | %ar | %s"`

12. 回退到指定版本

        1. `git reset --hard <commitID>`回退到指定版本代码
        2. `git reflog --pretty=oneline` 查看所有提交记录
    
13. 绑定远程仓库
	
    * 本地仓库关联远程仓库`git remote add origin 远程仓库地址 `
    * 删除远程仓库 `git remote rm origin`
    * 查看远程仓库地址 `git memote -v`
    * 第一次提交远程仓库 `git push -u origin master`
    * `git push` 已经有过提交之后只需要使用git push提交即可
14. 分支管理

    * 查看分支 `git branch`
    * 创建分支`git branch 分支名`
    * 切换分支`git checkout 分支名`
    * 快速创建并切换分支`git checkout -b 分支名`
    * 删除分支`git branch -d 分支名`
    * 分支合并`git merge 分支名`把其他分支代码合并到当前分支
    * 查看远程分支名`git remote show origin`
    * 切换远程分支`git checkout 远程分支名`直接可以切换
    * 拉取远程分支最新代码`git pull`
    * 删除远程分支`git push origin --delete 远程分支名`