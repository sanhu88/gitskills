# gitskills


##初始设置
	git config --global user.name "Joe Smith"
	git config --global user.email "name@mail.com"
	git config --global <配置名称> <配置的值>
	git config --global core.autocrlf false  windows中的换行符为 CRLF， 而在linux下的换行符为LF
<br>

成立仓库（克隆或者新建）
	克隆
	git clone https://github.com/shiyanlou/gitproject
	cd gitproject

新建
cd project
git init

git clone /home/shiyanlou/gitproject myrepo 	克隆后并重命名
git pull /tmp/myrepo master			
git pull命令执行两个操作: 它从远程分支(remote branch)抓取修改git fetch的内容，然后把它合并git merge进当前的分支
git remote add myrepo /tmp/myrepo		添加远程分支并给出缩写



基本日常操作

git status		查看状态
git log --oneline --garph		一行 图表查看log
git log --stat		显示每次提交修改过的文件
git log --pretty=short		跟格式化输出 oneline medium,full,fuller,email 或raw
git log --reverse 		升序时间展示log
git log --pretty=format:'%h : %s' --topo-order --grap 	


git add file1 file2 file3		可以提交多个文件
git diff				查看工作区中没有add提交到暂存区的修改
git diff --cached		查看暂存区被修改的文件 git diff --staged ，synonym同义词



git add *		添加所有文件 git add .
git diff master test		查看连个分支的区别，和前者相比，后者相对变化的
git diff  test			切换到master后可以直接比较两个分支
git diff test file1		比较两个分支中的某一个文件
git diff test --stat 	统计参数



git commit -m ""
git commit -a -m "add 3 files"		省去add提交，但是不会提交新建文件

git rm file1		删除文件，并且已经add到暂存区，commit之后就会删除

git remote add origin https://github.com/urname/shiyanlou.git 		为init的本地仓库添加远程主机

git push origin master

1.touch file1 file2 file3		创建3个文件
2.echo "test" >> file1		使用echo往文件写入，wim 退出：q 不保存
3.cat file1			查看文件内容

分支

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


标签

git tag stable-1 8c315325		为莫格提交创建轻量级的标签


远程仓库
	github
	ssh -T git@github.com
	pushd 时候提示Everything up-to-date 可能是还没有commit