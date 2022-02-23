#### Git安装配置

1. 安装

2. 配置

       - `/etc/gitconfig`：所有用户适用；`git config --system`
       - `~/.gitconfig`：该用户适用；`git config --global`
       - `.git/config`：当前项目；`git config`

   ```txt
   $ git config --global user.name "test"
   $ git config --global user.email test@qq.com
   $ git config --list #检查已有配置信息
   $ git config user.name #查阅某个环境变量
   ```

3. ssh连接Github

   ```txt
   $ ssh-keygen -t rsa -C "your_email@youremail.com"
   ```
   
   确认路径和输入密码时，默认回车就好。生成的key在`~/.ssh.id_rsa.pub`，复制出来在github中添加一下。
   
   ![alt ssh-key](.\Git-establish-pic\sshkey.PNG)

​		下一步验证是否成功，输入

​		`$ ssh -T git@github.com`

![alt ssh-connect-confirm](.\Git-establish-pic\ssh-connect-comfirm.PNG)

#### 新建repository

1. 本地新建，推到远程库

   - 登录GitHub，新建repository

   - ```txt
     $ git init
     $ git remote add origin git@github.com:yourName/yourRepo.git
     ```

     看看GitHub中repository的地址是怎样的

     ![alt repo-addr-pattern](.\Git-establish-pic\clone-addr-pattern.PNG)

   - `$ git push -u origin master `

2. 克隆已有repository

#### 时光穿梭机

###### 工作区、暂存区、版本库

![alt space](.\Git-establish-pic\space.jpg)

**工作区：**电脑中看到的目录<br>**暂存区：**（stage或index）在`.git/index`文件中，所以有时也叫索引<br>**版本库：**隐藏目录`.git`，这个不算工作区

##### 常用命令

![alt command](C:\Learn\Markdown&Git\TheFirstRepo\Git-establish-pic\git-command.jpg)

**`git status`** <br>**`git diff`**<br>	- git diff：查看working tree与index的差别<br>	- git diff --cached：查看index与repository的差别<br>	- git diff HEAD：查看working tree和repository的差别（所以肯定也能对比之前版本的差别）<br>	还可以对比不同版本间的差异：`git diff HEAD^ HEAD^^ --stat`<br>**`git add`**<br>	- git add [file1] [file2]<br>	- git add [dir]	添加指定目录，包括子目录<br>	- git add .	添加当前目录所有文件<br>**`git restore`**<br>	-S, --staged		 restore the index<br>	-W, --worktree	restore the working tree(default)（注意这俩是大写）<br>**`git commit -m "append blabla"`**<br>**`git log`**显示从最近到最远的提交日志，可以看到commit_id<br>	--pretty=oneline参数<br>	commit id 很长，使用的时候可以只写前四五位<br>**`git reflog`**<br>**`git reset`**<br>	git reset --hard commit_id<br>	git reset --hard HEAD^<br>	本质：移动HEAD以及它所指向的branch<br>	这个网站讲的很好：https://www.jianshu.com/p/c2ec5f06cf1a![alt reset-param-word](C:\Learn\Markdown&Git\TheFirstRepo\Git-establish-pic\reset-param-word.PNG)

![alt reset-param-pic](C:\Learn\Markdown&Git\TheFirstRepo\Git-establish-pic\reset-param-pic.webp)

###### 撤销修改的神奇操作，深入探究`restore,checkout,reset`

`git restore`命令可以撤销修改，在老版本中，这个功能是由`git checkout`实现的，但具体效果有些许不同。

`git checkout -- <file>`可以撤销工作区的修改，分两种情况<br>（1）修改后没放到stage，撤销修改后和版本库一样<br>（2）放到了stage，然后又修改了，那么撤销修改就和stage里的一样<br>需要注意，命令里的`--`很重要，不然就变成“切换分支”了。

用命令`git reset HEAD <file>`可以把stage中的修改撤销，放回工作区。<br>看看这个命令，`gir reset`默认参数`--mixd`，效果是把原节点和reset节点的差异放到working tree当中。所以其实这个命令就是对比了一下当前修改内容和当前版本库的差异，放回到了工作区。

**`HEAD`**<br>	当前版本：HEAD<br>	上一个版本：HEAD^	HEAD~1<br>**`git rm`**

**`git remote add origin git@github.com:huangsj18/TheFirstRepo.git`**<br>**`git push -u origin master`**<br>**`git push origin master`**<br>**`git remote -v`**<br>**`git remote rm origin`**（“删除”是解除本地和远程的绑定关系）

#### 分支管理

##### 合并分支，解决冲突

`git checkout -b dev` (`git switch -c dev`)相当于<br>		`$ git branch dev`<br>		`$ git checkout dev`(`git switch dev`)<br>`git branch` 查看分支<br>`git merge` 合并指定分支到当前分支<br>		冲突情况下，手动编辑，commit之后如果不冲突了会自动继续合并。<br>`git branch -d dev`	delete branch<br>`git branch -D dev`	强制删除，没合并的分支不能删除（除非只新建了空文件）

`git merge --no-ff -m "merge with no-ff" dev`	强制禁用Fast forward模式<br>`git log --graph --pretty=oneline --abbrev-commit`

##### Bug分支

`git stash`	“储藏”当前工作现场（可以多次）<br>`git stash list`	查看<br>`git stash apply`	恢复（但不删除）<br>`git stash drop`<br>`git stash pop`	恢复并删除<br>`git cherry-pick <commit_id>`	复制特定的提交到当前分支。比如说：master分支改了一个bug，我在dev也要改，用`cherry-pick`可以避免重复劳动。

##### 多人协作

`git remote -v`<br>`git checkout -b <branch-name> origin/<branch-name>`<br>`git branch --set-upstream-to <branch-name> origin/<branch-name>`<br>`git pull`<br>`git push origin <branch-name>`

#### 标签管理

有人比喻成IP和域名的关系

`git tag <name>`	默认打在最新提交的commit上，注意是哪个分支<br>`git tag <name> <commit-id>`<br>`git tag`	查看所有标签，是按照字母顺序给出的，不是时间顺序<br>`git show <tagname>`	查看标签信息<br>`git tag -a <name> -m "message" <commit-id>`<br>`git tag -d <tagname>`<br>`git push origin <tagname>`<br>`git push origin --tags`<br>`git push origin :ref/tags/<tagname>`	删除远程库的标签

#### 自定义Git

##### 忽略特殊文件

`.gitignore`<br>`$ git add -f <file>`	强制添加<br>`git check-ignore -v <file>`	找不能加的原因

##### 配置别名

`$ git config --global alias.ci commit	$git ci -m "blabla"`<br>`$ git config --global- alias.last 'log -l'	$ git last`<br>`$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"	$ git lg`

前面有说`--global`针对当前用户，配置文件在`.git/config`?

##### 自己搭建Git服务器

#### 最后

##### ssh是什么

##### LF和RCLF

CR(Carriage Return),'\r'<br>LF(Line Feed),'\n'

windows	CRLF<br>Linux	LF

`git config --global core.autocrlf [true|false|input]`

true:默认，push CRLF->LF; pull LF->CRLF<br>false:不转换，不推荐<br>input:	push CRLF->LF;	pull 不变



