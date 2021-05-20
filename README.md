# Git 学习教程

> 注：该教程是在 Win10 环境下编写的

安装之前确保已经阅读了以下文章或已安装 Git,并能区别 Git 和 GitHub 的关系.
1. [Git 详细安装教程 (详解 Git 安装过程的每一个步骤)](https://blog.csdn.net/mukes/article/details/115693833)
2. [Git 和 Github 的区别？以及 Git 的起源](https://blog.csdn.net/mukes/article/details/115673337)



一个 Git 项目的构成:

工作区(工作树) -- 暂存区（Stage 或者 Index）-- HEAD（本地仓库） --远程仓库

一个 Git 命令速查表：[awesome-cheatsheets](https://github.com/skywind3000/awesome-cheatsheets/blob/master/tools/git.txt)




### 快速入门

#### 设置用户名邮箱
安装完 Git 之后，要做的第一件事就是设置你的用户名和邮件地址。 这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改：

``` bash
$ git config --global user.email "your_email@example.com" 
等同于  git config --global --add user.email "your_email@example.com"

$ git config --global user.name "Firstname Lastname"
```

这两个命令会把邮箱和用户名设置在 `C:\Users\$USER` 目录下的 ` .gitconfig` 文件 中。

若没有 `.gitconfig` 文件，执行 `git config --global` 命令的时候则可生成 ~/.gitconfig 文件，`~` 代表当前用户目录，如 `C:\Users\kesyupeng`

git config 有三个比较重要的配置参数：

```bash
git config --system 系统配置，表示系统上每一个用户及他们仓库的通用配置，路径在 C:\Program Files\Git\etc\gitconfig(Git 安装目录 etc 文件夹下)
git config --global 当前用户配置，表示 windows 当前用户的仓库配置，路径在 C:\Users\$USER\.gitconfig
git config --local  仓库配置，每个 Git 仓库（项目）都有，路径在仓库（项目） .git 文件夹下的 config 文件中
三个参数，优先级由下往上，同一个属性，下面的会覆盖上面的，如 --local 会覆盖 --global，--global 会覆盖 --system.
```

Git 会按照你的需要自动为大部分的输出内容配制不同颜色，你能明确地规定哪些需要着色以及怎样着色，设置 color.ui 为 true 来打开所有的默认终端着色。下面 auto 则是自动选择。
```bash
$ git config --global color.ui auto
```

你可以通过以下命令查看所有的配置以及它们所在的文件：

```bash
$ git config --list --show-origin 
```

#### 创建 SSH Key

```bash
$ ssh-keygen -t rsa -C "you_email@example.com"
```

代码参数含义：

-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。



运行上面那条命令后会让你输入一个文件名，用于保存刚才生成的 SSH key 代码，如：

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/admin/.ssh/id_rsa): [Press enter]
```

输入文件名再回车则使用输入的文字所为文件名。

直接点击回车则使用默认文件名（推荐），那么就会生成 `id_rsa` 和 `id_rsa.pub` 两个秘钥文件。

接着又会提示你输入两次密码（该密码是你推送（git push）文件到远程仓库的密码，而不是登录 GitHub 的密码）

```bash
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:
```

密码可不输，直接点回车即可。

生成密钥成功结果如下：

```bash
Your identification has been saved in /c/Users/you/.ssh/id_rsa.
Your public key has been saved in /c/Users/you/.ssh/id_rsa.pub.
The key fingerprint is:
......
```

生成的 `id_rsa.pub` 和 `id_rsa` 在 `C:\Users\{$username}\.ssh` 目录下
`id_rsa.pub` 是公钥，`id_rsa` 是私钥。
公钥可以给所有人，私钥留给自己。

查看公开秘钥

```bash
$ cat ~/.ssh/id_rsa.pub
```



#### 添加 SSH Key 到 GitHub

把公钥添加到 GitHub 后，就可以用 私钥 来认证，而不用账号密码（使用账号密码每次推送都要输入一次账号密码），比较方便。

私钥是你本人拥有，其他人都不知道，用公钥验证私钥通过，说明这个就是你本人，和账号密码类似。



用编辑器打开 id_rsa.pub 文件，复制里面的内容

打开 GitHUb，登录账号，点击右上角的头像，再点击 `Settings`，然后点击菜单栏的 `SSH and GPG keys` 进入页面添加 `SSH key`。

点击 `New SSH key` 按钮添加一个 `SSH key` ，把你复制的 SSH key 代码粘贴到 key 所对应的输入框中，记得 SSH key 代码的前后不要留有空格或者回车。当然，上面的 Title 所对应的输入框你也可以输入一个该 SSH key 显示在 GitHub 上的一个别名，默认的会使用你的邮件名称。

最后，打开 git bash。

用私人秘钥和 GitHub 进行认证和通信

```bash
$ ssh -T git@github.com
```

成功则显示

```bash
$  ssh -T git@github.com
Hi kesyupeng! You've successfully authenticated, but GitHub does not provide shell access.

```



#### 仓库操作

克隆远程仓库到本地

随意在文件管理器一个地方进行鼠标右击，比如`E:\Git`目录下，然后点击 `git bash`,然后执行以下操作：

```bash
$ git clone git@github.com:keyupeng/hello-world.git
```

克隆时会在当前目录下生成一个 hello-world 目录，这个目录就是 hello-world 项目，里面存放着项目源码



进入克隆好的项目

```bash
$ cd Hello-World
```



新建一个文件并编辑，若文件存在直接编辑

```bash
$ vim hello_world.py
按 i 进入编辑模式，编辑完成后按 esc，然后再输入 :wq 保存并退出
```

查看仓库状态

```bash
$ git status
```

一般使用该命令后可能会出现这个词 untracked files， 表示未跟踪文件
意思是说该文件还没加入到暂存区，只是在当前工作目录创建了文件，该文件还没被记入 Git 仓库的版本管理对象当中。因此我们用 git status 命令查看 hello_world.py 文件时，它会显示在 Untracked files 里。



向暂存区添加文件

```
$ git add hello_world.py # 将文件提交到 暂存区
```

使用该命令后再 git status 可能出现的词：changes to be committed 表示 `等待提交`
add 表示将文件加入暂存区，暂存区是提交之前的一个暂存的区域



将暂存区内容添加到本地仓库中

```bash
$ git commit -m "备注提交信息"
```

该命令只能提交暂存区的文件到本地仓库，如果你又新建了文件没有 `git add` 的话是不会添加到本地仓库的。

且该命令不是提交一个文件，暂存区有多少个文件就提交多少个文件。

在 Git 中，可以通过相关命令回溯到某个提交点，所以要保证一次提交是完整的。

这样，别人同步你的提交时，能把项目运行起来。

比如说项目要增加某个功能，但是你写到了一半就提交了，这是不完整的提交，你的同事更新到你的最新提交，想运行看看效果，结果却运行不起来。

所以在项目中千万不要写一个文件提交一次（练习除外）



查看提交日志

```bash
$ git log
```

该命令可以查看以往仓库中提交的日志。



把新增的提交推送到远程服务器上

```bash
$ git push
```

















