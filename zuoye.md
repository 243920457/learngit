#git
###git优点
能记录每次文件的改动，有利于文档或者代码修改回档。
###git安装
1.下载git

2.打开git bash

3.在命令行输入：

        $ git config --global user.name "Your Name"

        $ git config --global user.email "email@example.com"

4.git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置
###git版本库简介与创建
1.可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

2.寻找合适地方通过***mkdir***创建空目录再通过***git init***将目录变成可以用的仓库。

3.将文件放到仓库目录或其子目录下，再用***git add***命令将其添加到仓库。接着用***git commit***（后可跟-m +输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录）命令将所有暂存区文件上交到分支。

4.***git status***可以查看当前仓库文件是否被修改过。***git diff***命令可以查看文件被怎么修改过的详细信息
###git版本转换
1.HEAD指针指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令***git reset --hard commit_id。***（上一个版本为HEAD^上上个版本为HEAD^^）

2.穿梭前，用***git log***可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用***git reflog***查看命令历史，以便确定要回到未来的哪个版本。

3.当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令***git checkout -- file***

4.当你改乱了工作区某个文件的内容，并且已经上传到了暂存区，想丢弃修改，分两步，第一步用命令***git reset HEAD <file>***撤销暂存区，再用命令***git checkout -- file***撤销工作区。

5.已经将错误提交到了版本库但是没有提交到远程服务器则可以用1.2.步骤进行版本转换。
###工作区暂存区和分支

1.工作区就是目录仓库，通过***git add***将工作区的文件添加到暂存区再通过***git commit***将文件添加到分支，再有分支上传到服务器。

2.git文件只有先通过***add***添加到暂存器中才可以被***commit***添加到分支，git跟踪的是文件的修改而不是整个文件。

3.如果将已上传到版本区的工作去文件删除后可通过***git rm***删除版本区中文件做到彻底删除或者通过***git checkout***用版本区文件替换工作区文件，即恢复误删文件到工作区。
###远程仓库

1.通过***$ ssh-keygen -t rsa -C "youremail@example.com"***建立ssh key 再将目录下***.ssh***文件中公钥***id_rsa.pub***上传到github网站上。

2.要关联一个远程库，使用命令***git remote add origin git@server-name:path/repo-name.git***
  关联后，使用命令***git push -u origin master***第一次推送master分支的所有内容；
  此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

  3.克隆：要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
         Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。
###git分支使用

1.查看分支：git branch

  创建分支：git branch <name>

  切换分支：git checkout <name>

  创建+切换分支：git checkout -b <name>

  合并某分支到当前分支：git merge <name>

  删除分支：git branch -d <name>

  2.当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
    （解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交）

  3.合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并

  4.修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
    当手头工作没有完成时先***git stash***，然后去修复bug，修复后，再***git stash pop***，回到原工作。

  5.开发一个新feature，最好新建一个分支；
    如果要丢弃一个没有被合并过的分支，可以通过***git branch -D <name>***强行删除。

  6.查看远程库信息，使用git remote -v；

   本地新建的分支如果不推送到远程，对其他人就是不可见的；

   从本地推送分支，使用***git push origin branch-name***，如果推送失败，先用***git pull***抓取远程的新提交；

   在本地创建和远程分支对应的分支，使用***git checkout -b branch-name origin/branch-name***，本地和远程分支的名称最好一致；

   建立本地分支和远程分支的关联，使用***git branch --set-upstream branch-name origin/branch-name***；

   从远程抓取分支使用git pull，如果有冲突，要先处理冲突。
   ###标签使用

   1.命令***git tag <tagname>***用于新建一个标签，默认为HEAD，也可以指定一个commit id；

   2.命令***git tag -a <tagname> -m "blablabla...***"可以指定标签信息；

   3.命令***git tag***可以查看所有标签。

   4.命令***git push origin <tagname***>可以推送一个本地标签；

   5.命令***git push origin --tags***可以推送全部未推送过的本地标签；

   6.命令***git tag -d <tagname***>可以删除一个本地标签；

   7.命令***git push origin :refs/tags/<tagname***>可以删除一个远程标签。
