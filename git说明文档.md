#Git说明
## git安装
在windows安装git：
`https://git-scm.com/download/win`

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

* 生成公匙

  * 检测.ssh文件夹是否存在

    `cd ~/.ssh/`

    如果提示No such file or directory

    `mkdir ~/.ssh`

  * 配置名称和邮箱

    `git config --global user.name "名字"`
 

    `git config --global user.email "邮箱"`

  * 生成key

    `ssh-keygen -t rsa -C "邮箱"`

    添加到账户的key在：打开Admin目录进入.ssh文件夹，用Notepad++打开id_rsa.pub，复制内容，在码云的个人设置SSH公钥，添加公钥。
##版本库
 * 创建版本库
 
     ` mkdir git ` 
     
     ` cd git`

     `git init`  把这个目录变成Git可以管理的仓库
     
     在git目录下创建文件，如git.txt

     `git status` 查看状态

     `git add .` 把文件添加到暂存区

     `git commit -m 'up'` 把文件提交到仓库，`-m`后面输入的是本次提交的说明

 * 版本回退
 
    如果你对git.txt修改多次，并提交到仓库。但想回到上一个版本：
   
    `git log` 查看历史版本
    
    `git reset --hard HEAD^`回退到上一个版本
    
     说明：上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成`HEAD~100`。

    `git reflog`查看命令历史

    `git reset --hard f2cd176` 回到未来的哪个版本，f2cd176是版本id。（前提命令行窗口还没有被关掉）
 
     **注意**（回退之后提交到远程库）：


	- 新建分支

		`git checkout -b temp`              //新建分支并切换到temp分支

		`git push origin temp:temp`         //将代码push到temp分支

	- 删除分支 
	
		`git push origin --delete feat`   //删除远端feat分支

		`git branch -d feat`              //删除本地feat分支

	- 新建分支
	
		`git checkout -b feat `           //新建feat分支并切换到feat分支

		`git push origin feat`            //提交feat分支

	- 删除暂存分支
	
		`git branch -d temp`

		`git push origin --delete temp`

	`git checkout -- git.txt` 撤销修改

    `git reset HEAD git.txt` 把暂存区的修改回退到工作区，然后在撤销修改

	`git rm git.txt` 删除文件

## 远程仓库

  `git remote add origin git@gitee.com:WuXian-Hen/demo.git` 关联本地仓库和远程库，git@gitee.com:WuXian-Hen/demo.git是码云项目SSH地址

`git remote -v` 查看关联状态

`git remote rm origin` 删除远程库

 `git push -u origin master` 把本地库的所有内容推送到远程库
    
 `git push` 提交修改

`git clone git@gitee.com:WuXian-Hen/demo.git`克隆项目,默认只有master分支，

`git checkout -b name origin/name` 创建本地分支，name为分支名
 	
`git pull` 更新

##分支管理
   * 分支
   
   	`git branch` 查看分支，*表示当前分支

	`git branch name` 创建分支；name为分支名

 	`git checkout name` 切换分支
	
    `git checkout -b name` 创建+切换分支

	`git merge name` 合并name分支到当前分支

	`git log --graph` 查看分支合并图
	
	当出现CONFLICT ，表示有冲突
	
	`git status` 查看冲突文件，`git diff git.txt `查看文件，手动解决冲突

	`git branch -d name` 删除分支

	`git push origin name` 提交分支到远程库

	如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建

	`git branch --set-upstream name origin/name`本地分支和远程分支链接

##标签管理
`git tag <tagname>` 创建标签

`git tag` 查看标签,标签不是按时间顺序列出，而是按字母排序的

`git show <tagname>` 查看标签说明信息

`git tag v0.9 6224937` 给历史提交打标签，6224937为commit id，通过`git reflog`查看

`git tag -d <tagname>` 删除本地标签

`git push origin <tagname>` 推送标签到远程

`git push origin --tags` 推送所有标签到远程

`git push origin :refs/tags/<tagname>`删除远程标签，一定要先删除本地标签

##别名配置
`git config --global alias.<简称> <命令>`配置别名

每个仓库的Git配置文件都放在.git/config文件中，别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中，配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。
