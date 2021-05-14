Git 教程





工作区(工作树) -- 暂存区（Stage 或者 Index）-- HEAD（本地仓库） --远程仓库


一个命令速查表：awesome-cheatsheets


设置用户名邮箱
安装完 Git 之后，要做的第一件事就是设置你的用户名和邮件地址。 这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改：
git config --global user.email "1373998182@qq.com" 等同于  git config --global --add user.email "1373998182@qq.com"
git config --global user.name "kesyupeng"

这两个命令会把邮箱和用户名设置在 C:\Users\用户名 目录下的 .gitconfig 文件中，linux 下是 ~/.gitconfig 或者 ~/.config/git/config
 C:\Program Files\Git\etc 目录下也有一个 gitconfig 文件，是系统的，在 linxu 下是 /etc/gitconfig
git config --global --unset user.name  删除 user.name 配置
执行 git config --global 命令的时候生成 ~/.gitconfig 文件
仓库名 主干分支之类的属性 存在 项目 .git 文件夹下的 config 中

Git 会按照你需要自动为大部分的输出加上颜色，你能明确地规定哪些需要着色以及怎样着色，设置 color.ui 为 true 来打开所有的默认终端着色。auto 则是自动选择
git config --global color.ui auto



查看设置
git config --list --show-origin 或者 cat ~/.gitconfig

创建 SSH Key
$ ssh-keygen -t rsa -C you_email@example.com
然后按一次回车键，输入密码
代码参数含义：

-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。

cmd 下没有 ssh-keygen.exe
git 的安装目录下才有
生成的 id_rsa.pub 和 id_rsa 在 C:\Users\{$username}\.ssh 目录下

跳过不输入密码时，以后也不需要密码了
要改会设置的话 可能就需要 ssh-keygen 命令了

查看公开秘钥
$ cat ~/.ssh/id_rsa.pub

~ 指当前用户目录
如：/c/Users/admin

known_hosts 是什么东西？
ssh 会把你每个你访问过计算机的公钥 (public key) 都记录在 known_hosts。当下次访问相同计算机时，OpenSSH 会核对公钥。如果公钥不同，OpenSSH 会发出警告， 避免你受到 DNS Hijack 之类的攻击。
known_hosts格式：Ip或域名 主机名 host-key
使用 known_hosts 的作用是防止 DNS 攻击。

linux 下公钥存放的位置
~/.ssh/authorized_keys

用私人秘钥和 GitHub 进行认证和通信
$ ssh -T git@github.com

clone 已有仓库
git clone git@github.com:keyupeng/hello-world.git

克隆时会在当前目录下生成一个 hello-world 目录，这个目录就是 hello-world 项目，里面存放着项目源码

$ git branch -a
* master
  remotes/origin/HEAD -> origin/master  # 这个的意思是指默认分支
  remotes/origin/feature-A
  remotes/origin/master

git clone 克隆后我们会处于默认分支下，且只会克隆 master 项目，特性分支项目需要手动克隆检出

git checkout -b feature-A origin/feature-A 

再次运行 git branch -a 发现有 feature-A 项目了

进入克隆好的项目
$cd Hello-World

touch+文件名，直接新建一个文件
$ touch hello_world.php

新建一个文件并编辑，若文件存在直接编辑
vi + 文件名
$ vi hello_world.php
完成后按 esc，然后再输入 :wq 保存并退出

查看仓库状态
$ git status

出现 fatal: not a git repository (or any of the parent directories): .git 问题
原因：没有初始化

将 hello_world.php 提交至仓库
$ git add hello_world.php
$ git commit -m "Add hello world script by php"


查看提交日志
$ git log

进行 push
$ git push


第 2 部分

创建一个目录并初始化仓库
$ mkdir git-tutorial
$ cd gti-tutorial
$ git init
初始化后会生成一个 .git 目录，这个目录存储着管理当前目录内容所需的仓库数据

我们一般将该目录（不是.git 目录）的内容称为”附属于该仓库的工作树“ ？（未确认


git status  查看仓库的状态
$ git status
一般使用该命令后可能会出现这个词，untracked files 表示未跟踪文件
意思是说该文件还没加入到暂存区
只是在当前工作目录创建了文件，那么该文件并不会被记入 Git 仓库的版本管理对象当中。因此我们用 git status 命令查看 REAME.md 文件时，它会显示在 Untracked files 里。


git add 向暂存区添加文件
$ git add 文件名.后缀
使用该命令后再 git status 可能出现的词：changes to be committed 表示 已暂存/已暂存可以被提交的文件/等待提交/要提交的更改
add 表示将文件加入暂存区。暂存区是提交之前的一个暂存的区域


git commit 保存仓库的历史记录
$ git commit -m  "备注提交信息"
-m 后面的消息 称为提交信息，对这个提交的概述。
git commit -am "备注信息"  # 可以提交被跟踪的文件，未被系统跟踪的文件不能提交 
该命令相当于 git commit -a-m "提交信息"
该命令可以将当前暂存区中的文件实际保存到仓库的历史记录中（.git 文件中？）
提交（commit）：是指”记录工作树中所有文件的当前状态“ 重点--》所有文件

想要记录更详细的提交信息，请不加 -m，直接执行 git commit，会跳出 vim 编辑器
再运行 git status 出现：
nothing to commit, working tree clean 现在是 2021年 # 工作树
14年出版的 GitHub 入门与实践 的结果则是：nothing to commit, working directory clean # 工作目录




git log 查看提交日志，该命令只能查看以当前状态为终点的历史日志
$ git log
该命令可以查看以往仓库中提交的日志。git log 可加 目录或者文件名
显示文件前后的差别
$ git log  [文件名.后缀]  # 只显示该文件信息
$ git log -p [文件名.后缀]  # 只显示该文件前后对比信息

$ git log --pretty=short  # 只显示 哈希值 和 作者 和 提交信息
git log --pretty=oneline 只显示 哈希值 和 提交信息
git log master..origin/master # 对比本地和远程 master 的区别显示远程有而本地没有的 commit 信息


git diff 查看更改前后的区别，可以查看 工作树、暂存区、最新提交之间的区别
git diff  对比 工作树 和 暂存区的区别，如果暂存区无文件，则比较工作树和最新提交之间的区别，如果暂存区有文件，且和 工作树 里的一样，则不会有任何显示
git diff HEAD 查看 工作树 和 最新提交 的差别
git diff --cached 查看 暂存区 和 最新提交HEAD 的查别

在刚刚提交的 README.md 文件里面添加一句”Git 教程“
执行 git diff 命令，查看 当前工作树 与暂存区 的区别。由于我们没用 git add 命令 向暂存区添加任何东西，所以程序只会显示 工作树 与 最新提交 状态之间的差别
养成一个好习惯：在执行 git commit 之前 先执行 git diff HEAD ，查看本次提交和上次提交有什么差别。
HEAD 是指向 当前分支中最新一次的提交。


分支操作

显示分支一览表
git branch 
git branch -a 显示所有分支

创建、切换分支
git checkout -b <分支名>  # 创建分支并切换到分支
相当于：
git branch <分支名>
git checkout <分支名>

git checkout - 切换回上一个分支

git merge 合并分支
先切回到主分支，再执行
$ git merge --no-ff <分支名>  # 这个会保存你的特性分支历史，合并也是一个提交
git merge 则不会显示 feature，只保留单条分支记录，直接用 HEAD 指向新特性？ （即只有主干，删除分支后没有提交信息了

以图表形式查看分支
git log --graph


更改提交的操作

1.回溯历史版本
git reset 
让仓库的 HEAD、暂存区、当前工作树 回溯到指定状态，需要用 git reset --hard 命令

回溯到还没创建 feature-A 的 master 主干
git reset --hard 751bb6

创建 fix-B 版本
git checkout -b fix-B

推进历史 
git reflog 查看当前仓库的操作日志，在日志中找出回溯历史之前的哈希值，并通过 git reset --hard 命令恢复到回溯历史前的状态。

git reset --hard 9e96abb # 回到 合并 feature-A 的那一刻

合并 fix-B 到 master
git merge --no-ff fix-B 

合并冲突，需要修改 README.md 文件
然后再 add 和提交




修改提交信息
git commit --amend 修改上一条提交信息



2.压缩历史
git rebase -i
在合并特性分支之前，如果发现已提交的内容出现拼写错误之类的问题，不妨提交一个参数，然后将这个修改包含到前一个提交之中，压缩成一个历史记录。

先创建一个特性分支 feature-C
git checkout -b feature-C


增加 README.md 内容


把两条提交合并成一条
git rebase -i HEAD~2
这条命令可以选定当前分支中包含 HEAD（最新提交）在内的两个最新实力记录为对象，并在编辑器中打开

合并至 master 分支
git checkout master
git merge --no-ff feature-C



upstream 意为上游，即本地分支所对应的远程分支

master和origin/master 都是本地分支，不同的是origin/master指向远程仓库且无“实体”，相当于远程仓库orign的master分支在本地的一个代理人，orign master则很清晰，其中origin表示远程仓库名字，master远程仓库中的分支名字。

当使用git fetch origin master时，本地的origin/master仓库会更新至最新，但是master分支无变化，此时再用git merge origin/master即可将最新代码合并至master，master也就是最新代码了，也可使用git pull origin master直接代替git fetch+git merge
pull request 这个功能很重要
推送至远程仓库 
添加远程仓库
git remote add origin git@gitHub.com:kesyupeng/learn_git  # origin 是这个远程仓库的简称，你可以改成自己喜欢的简写如lg

如果更换远程地址，或者远程地址改名了，则
git remote remove <name> # 删除配置文件 config 里面的节点 等同于 git remote rm <name>  
git remote add origin git@github.com:<username>/<projectname>

git remote # 查看远程仓库
git remote -v # 查看所有远程仓库
git remote show <仓库名> # 查看某个远程仓库更多信息
执行上述命令后，Git 会自动将 git@github.com:kesyupeng/learn_git 远程仓库的名称设置为 origin（标识符）

推送至远程仓库
git push <远程主机名> <本地分支名>:<远程分支名>
git push -u origin master 或者 git push --set-upstream origin master
执行该命令，当前分支内容就会被推送到远程仓库 origin 的 master 分支。
-u 参数表示在推送的同时，将 origin 仓库的 master 分支设置为本地仓库当前分支的 upstream（上游）。

拉取远程仓库

git fetch <仓库名>
git fetch origin 会抓取克隆（或上一次抓取）后新推送的所有工作。 必须注意 git fetch 命令只会将数据下载到你的本地仓库 —— 它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。

如果你的当前分支设置了跟踪远程分支（阅读下一节和 Git 分支 了解更多信息）， 那么可以用 git pull 命令来自动抓取后合并该远程分支到当前分支。
默认情况下，git clone 命令会自动设置本地 master 分支跟踪克隆的远程仓库的 master 分支（或其它名字的默认分支）。 运行 git pull 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

git pull = git fetch + git merge
























