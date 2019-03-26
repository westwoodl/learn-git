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

分支：
	Git鼓励大量使用分支：
		因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
	查看分支：git branch
	创建分支：git branch <name>
	切换分支：git checkout <name>
	创建+切换分支：git checkout -b <name>
	合并某分支到当前分支：git merge <name>
	删除分支：git branch -d <name>

分支冲突：
	当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
	解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
	用git log --graph命令可以看到分支合并图。

fast forwoard：
	合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

保留现场：
	修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
	当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

删除分支：
	如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

多人协作：
	多人协作的工作模式通常是这样：
		首先，可以试图用git push origin <branch-name>推送自己的修改；
		如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
		如果合并有冲突，则解决冲突，并在本地提交；
		没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
		如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
		这就是多人协作的工作模式，一旦熟悉了，就非常简单。

	小结
		查看远程库信息：git remote -v；
		本地新建的分支如果不推送到远程，对其他人就是不可见的；
		从本地推送分支，使用：git push origin branch-name  如果推送失败，先用  git pull 抓取远程的新提交；
		在本地创建和远程分支对应的分支，使用：git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
		建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
		从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

标签：
	命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
	命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
	命令git tag可以查看所有标签。
 
 操作标签：
 	命令git push origin <tagname>可以推送一个本地标签；
	命令git push origin --tags可以推送全部未推送过的本地标签；
	命令git tag -d <tagname>可以删除一个本地标签；
	命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

GitHub：
	在GitHub上，可以任意Fork开源仓库；clone到本地加以修改
	自己拥有Fork后的仓库的读写权限；
	可以推送pull request给官方仓库来贡献代码。