# Git Notes
初次学习Git记下的笔记，供日后查询使用。

## 基本操作
	git bush here; //创建新的版本库,会有.git隐藏文件出现
	git status; //查看当前状态
	git log; //查看历史记录
	cat readme.txt //查看工作区该文件内容

## 添加操作
	git add. //添加工作区所有文件到暂存区
	git add readme.txt; //将readme添加到暂存区
	git commit - m "注释";//一次性将暂存区所有东西提交到版本库
	
## 回退与撤销
	git reset --hard 1094 ab; //将版本回退到过去，后面的数字字母为版本号
	git checkout--readme.txt; //撤销工作区的修改(还未add)
	git reset HEAD readme.txt; //撤销暂存区的修改，注意撤销完暂存区，还得撤销工作区，就是上行操作（已经add，还未commit）
	git reset --hard 1094 ab; //撤销已经提交到版本库的修改，使用版本回退（已经commit，还未上传远程）

## 删除
	rm readme.txt;//删除该文件
	git commit -m "删除";//提交删除操作到版本库
	git checkout -- readme.txt;//取消删除该文件
	
## 关于github
	git remote add origin https;//连接到自己的仓库url
	git push -u origin master;//如果当前分支与多个主机存在追踪关系，则可以使用-u参数指定一个默认主机，这样后面就可以不加任何参数使用git push
	git push -f origin master;//强制性的把本地库上传到远程库并覆盖
	git pull;//从远程获取最新版本并合并到本地
	git clone https;//远程克隆库
	git remote remove origin;//断开连接
	连接冲突//https://blog.csdn.net/u013120247/article/details/53263169

## Branch
	git branch;//查看分支，*为当前分支
	git branch dev;//创建分支dev
    git checkout dev;//切换当前分支到dev
	git checkout -b dev;//相当于上述两条操作
	git merge dev;//切回master后，将dev合并到当前分支（master）
	git branch -d dev;//删除dev分支，注意（fast forward模式下删除分支后，会丢失掉该分支信息）
	conflict//https://www.liaoxuefeng.com/wiki/896043488029600/900004111093344