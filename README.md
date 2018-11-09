# gitskills


##      初始设置
	git config --global user.name "Joe Smith"
	git config --global user.email "name@mail.com"
	git config --global <配置名称> <配置的值>
	git config --global core.autocrlf false  windows中的换行符为 CRLF， 而在linux下的换行符为LF
	git config --list	查看配置
<br>

##      成立仓库（克隆或者新建）
	克隆
	git clone https://github.com/shiyanlou/gitproject
	cd gitproject
	新建
	cd project
	git init
<br>

	git clone /home/shiyanlou/gitproject myrepo 	克隆后并重命名
	git pull /tmp/myrepo master			
	git pull命令执行两个操作: 它从远程分支(remote branch)抓取修改git fetch的内容，然后把它合并git merge进当前的分支
	git remote add myrepo /tmp/myrepo		添加远程分支并给出缩写



##     基本日常操作
	git status		查看状态
	git log --oneline --garph		一行 图表查看log
	git log --stat		显示每次提交修改过的文件
	git log --pretty=short		跟格式化输出 oneline medium,full,fuller,email 或raw
	git log --reverse 		升序时间展示log
	git log --pretty=format:'%h : %s' --topo-order --grap 	
<br>

	1.touch file1 file2 file3		创建3个文件
	2.echo "test" >> file1		使用echo往文件写入，wim 退出：q 不保存
	3.cat file1			查看文件内容
	git add file1 file2 file3		可以提交多个文件
	git diff				查看工作区中没有add提交到暂存区的修改
	


<br>

	git add *		添加所有文件 git add .
	git diff master test		查看连个分支的区别，和前者相比，后者相对变化的
	git diff  test			切换到master后可以直接比较两个分支
	git diff test file1		比较两个分支中的某一个文件
	git diff test --stat 	统计参数
	git diff HEAD 			已缓存的与未缓存的所有改动
	git diff HEAD^ HEAD	

	
	git diff commit_id_1 commit_id_2  	用来比较2个commit之间区别，以前面的id视角比较后面的id
	git diff --staged   	暂存与仓库的差异【add之后，commit之前】
	git diff --cached		查看暂存区被修改的文件 git diff --staged ，synonym同义词
<br>

	git commit -m ""
	git commit -a -m "add 3 files"		省去add提交，但是不会提交新建文件

	git rm file1		删除文件，并且已经add到暂存区，commit之后就会删除
	git rm -f <file> 	删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f
	git rm --cached <file> 	从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 --cached 选项

##     远程程仓库

	git remote add origin https://github.com/urname/shiyanlou.git 		为init的本地仓库添加远程主机
	git push origin master
	
	github
	ssh -T git@github.com
	pushd 时候提示Everything up-to-date 可能是还没有commit

	git pull origin 分支名称 	拉取远程到本地
	git pull <远程库名> <远程分支名>:<本地分支名>
	git pull origin		建立了关系后，可以省略
	git pull 命令等同于先做了git fetch ，再做了git merge
	<br>


	fatal: remote origin already exists
	1.git remote rm origin 		删除远程仓库绑定
	2.git remote add origin git@github.com:sanhu88/gitskills.git 	重新绑定
	3.git push -u origin master 	再次提交


	
##     分支

	git branch -b dev 快速创建并切换到dev分支
	git branch		查看所有分支列表
	
	git merge dev		合并dev到当前分支
	
	git merge -m 'merge experimental branch' experimental		-m是备注信息
	--ff  --ff--only  快速合并    只快速合并（如果有冲突就失败）
	--no-ff   非快速合并
	--squash  将合并过来的分支的所有不同的提交，当做一次提交，提交过来
	--ff和--no-ff的区别是，当解决完冲突后，no-ff会生成一次commit
		解决（Resolve）
		递归（Recursive）
		章鱼（Octopus）

	git diff		可以查看合并的冲突内容，也就是没有add的修改


	git merge --abort		撤销分支合并，commit之后就无法使用了
	git reset --hard HEAD^ 	返回合并前master的前一个提交id，觉得没问题可以git checkout id回去

	git branch -d dev		删除已经合并过的dev分支
	git branch –D deve		强制删除没有合并的分支


##     标签
	tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起
	git tag stable-1 8c315325		为某个id提交创建轻量级的标签
	git tag -a v1.0 				给最新一次提交打上（HEAD）"v1.0"的标签
	git tag -d v1.1 				删除标签

##     撤销
		1.撤销本地修改 没有add 更没有commit的
		git checkout -- filepathname


		2.已经add 还没commit
		git reset --hard HEAD^
		git diff --cached		先检查看下add了什么
		git reset HEAD readme.md
		git checkout --readme.md 	也就是上面第一步

		3.已经用 git commit  提交了代码
		git reset --hard HEAD <file>		最近一次的旧版本
		git revert HEAD^ 				撤销上上次的修改
		git reset --hard  commitid 		返回特定的id版本

		4.查看log
		git log
		git reflog		包含跳到老版本之前的commit id ，还可以看到之前id

## 		忽略
		使用.gitignore来实现
		windows 必须键入文件名 的解决办法： .gitignore. 
				or 按住shift 邮件CMD下 echo test > .gitignore
		官网推荐 https://github.com/github/gitignore
			比如magento的https://github.com/github/gitignore/blob/master/Magento.gitignore
		! 感叹号 不排除，跟踪 比如：
			/media/*
			!/media/.htaccess
			上面表示除了media下的.htaccess都排除
		# Windows:
			Thumbs.db
			ehthumbs.db
			Desktop.ini
		# Python:
			*.py[cod] --[cod]匹配区间，即pyc pyo pyd 都排除
			*.so
			*.egg
			*.egg-info
			dist
			build
		Use -f if you really want to add them. 	使用-f强制add和commit
		可以对.gitignore做版本管理

## 		储藏
		git stash save "work in progress for foo feature" 	保存一个储藏
		git stash apply		调用储藏
		git stash list		储藏列表
		git stash apply stash@{1} 		恢复到某一个储藏
		git stash clear		清空储藏列表

## 		维护
		git gc 	压缩仓库
		git fsck	一致性检查

## 		gitlab
		https://about.gitlab.com/product/
