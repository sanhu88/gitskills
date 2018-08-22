# gitskills

Creating a new branch is quick and simple.

初始设置
git config --global user.name "Joe Smith"
git config --global user.email "name@mail.com"
git config --global <配置名称> <配置的值>


成立仓库（克隆或者新建）
	克隆
	git clone https://github.com/shiyanlou/gitproject
	cd gitproject

	新建
	cd project
	git init

基本日常操作
git status		查看状态
git log --oneline --garph		一行 图表查看log
git add file1 file2 file3		可以提交多个文件
git diff				查看工作区中没有add提交到暂存区的修改
git diff --cached		查看暂存区被修改的文件 git diff --staged
git commit -m ""
git push

	1.touch file1 file2 file3		创建3个文件
	2echo "test" >> file1		使用echo往文件写入，wim 退出：q 不保存

分支

git branch -b dev 快速创建并切换到dev分支

git branch		查看所有分支列表

git merge dev		合并dev到当前分支

git merge --abort		撤销分支合并**

git branch -d dev		删除dev分支
