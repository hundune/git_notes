# Git			 

git config --global user,name "JW" 配置用户名

git config --global user.email 3421449006.qq.com 配置邮箱

git config --global credential.helper store 存储用户名和密码

省略（local）本地配置，只对本地仓库有效

--global：全局配置，所有的仓库有效

--system：系统配置，对所有用户生效



## 新建版本库（仓库）

方式一：git init



方式二：git clone 远程仓库克隆



## 工作区域和文件状态

工作区：.git 所在的区域 实际操作的目录

暂存区：一个中间区域，用于临时存放即将提交的修改内容

本地仓库：Git存储代码和版本信息的主要位置

工作区  ---git add ----》 暂存区 --- git commit ---》本地仓库

![1698152513554](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\1698152513554.png)



## 添加和提交文件

git提交的·时候只会提交暂存区中的文件

git stauts查看仓库的状态

git add将文件添加到暂存区中 可以使用通配符 git add *.txt（将所有的.txt的文件添加到暂存区中）

gitcommit 将文件提交到本地仓库中 如果不使用 -m 就会进入vim

git log查看仓库提交历史记录 可以使用 --oneline 参数来查看简介的提交记录



## 回退版本

 git reset 的三种模式

git reset -- soft 回退到某一个版本 保存工作区和暂存区中的内容

git reset --hard 回退到摸一个版本 工作区和暂存区中的所有内容不保存

git reset --mixed 会退到某一个版本 只保留工作区的内容，不保留暂存区的内容（默认）

 git reflog 查看操作

git reset --*** 版本号可以回退

只有提交的内容才能恢复，本次修改还没提交的内容会丢失



## 使用 git diff 查看差异

git diff 默认查看工作区和暂存区中的差异

git diff HEAD 工作区 + 暂存区中的内容和本地仓库中的差异

git diff --cached 暂存区和本地仓库的差异

git diff 版本号1 版本号2 比较两个版本的差异

HEAD~ 或者 HEAD^  HEAD的前一个版本

HEAD~数字 HEAD的前几个版本

git diff 跟上文件名 就比较这个文件的差异

git diff 分支名1 分支名2 两个分支的差异



## 从版本库中删除文件

git rm 文件名

![1698155743018](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\1698155743018.png)

要提交 git commit -m 



## .gitignore忽略文件

忽略掉一些不应该加入到版本库中的文件

系统或工具自动删除的文件

编译产生的中间文件和结果文件

运行时生成日志文件，缓存文件、临时文件

涉及身份、密码、口令、密钥等敏感信息文件

git 会监控所有加入暂存区的文件

如果有空的文件夹 git 不会将其添加到仓库中

可以编辑仓库中的 .gitignore 文件如：

```
*.txt //忽略所有txt文件
/doc //忽略doc目录下的文件，不忽略 ccc/doc 下的文件
!oo.txt //不忽略oo.txt文件
doc/  //忽略任何目录下的doc目录中的文件
doc/*.txt //忽略所有doc目录下的 .txt 文件 不忽略 doc/gg/***.txt 文件
doc/**/*.txt //忽略所有的doc目录及其子目录下的 *。txt 文件

```



## SSH配置和克隆仓库

![1698158684796](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\1698158684796.png)



## 本地仓库与远程仓库关联

git remote add 远程仓库的别名 url（远程仓库的地址）

git remote -v 查看当前仓库对应的远程仓库的别名和地址

git branch -M main 指定分支的名称为main

git push -u  远程仓库的别名  本地分支名：远程分支名 如果名称相同只用写一个分支名

git pull 远程仓库别名 远程分支名：本地分支名 （仓库名和分支名可以省略 默认为 origin main）

git fetch 获得远程仓库的修改 不会合并



## 其他平台

Gitee 步骤与 github 基本一致

GitLab 步骤一致 ；私有仓库：



## GUI工具

github desktop 时github官方出品的图形化工具

sourcetree



## Vscode中使用git

无解



## 分支及其基本操作

git branch 查看当前仓库的所有分支

git branch 分支名 创建新的分支

git checkout 分支名 切换分支（还可以用于恢复文件，可能出现歧义）

git switch 分支名 专门切换分支

git merge 将要被合并的分支名 （当前所在的分支就是合并后的目标分支）

git branch -d 分支名 如果一个分支被合并了就删除

git branch -D 分支名 强制删除这个分支



## 解决合并冲突

如果两个分支修改了同一个文件的同一行代码，就会产生冲突

想中断合并 git merge --abort

手动解决冲突：手动选择要保留的内容

修改完后要提交



## 回退和rebase（变基）

找到两个分支的公共祖先 根据选择的分支不同有不同的合并方式（选择的分支 合并到目标分支的最新提交后）

![1698162255073](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\1698162255073.png)

git checkout -b 想要恢复的分支名 提交的id 恢复到这个分支的这一时间点的状态

git log --oneline --graph --decorate -all 查询出提交和合并的记录

alias graph = “git log --oneline --graph --decorate -all“ alias可以设置快捷的git代码



rebase和merge的区别

merge 优点：不会破坏原分支的提交历史，方便回溯和查看

缺点：会产生额外的提交节点，分支图比较复杂



rebase优点：不会新增额外的提交记录，形成线性历史，比较值观和干净

缺点：会改变提交历史，改变了当前分支branch out的节点。

避免在共享分支使用，不会在共分支上使用



## git的工作流模型

![1698162953458](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\1698162953458.png)

![1698163056055](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\1698163056055.png)