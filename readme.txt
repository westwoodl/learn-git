Git is a version control system.
Git is free software.hahahahah
caocaocaocaocaocacoa
xuxuxuxuxux

版本回退：git reset --hard HEAD^    git log    git reflog


暂存区：
	Git管理的是修改，而不是文件
	你又理解了Git是如何跟踪修改的，每次修改，如果不用git add到暂存区，那就不会加入到commit中。

撤销修改：
	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

删除文件：
	如果删除了工作区的文件
	现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm file.name 删掉，并且git commit -m "content"
	另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
		$ git checkout -- test.txt

添加远程库：
	要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
	关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
	此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

从远程库clone：
	git clone git@github.com:michaelliao/gitskills.git