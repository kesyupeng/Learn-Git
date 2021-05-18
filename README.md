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
$ git config --global user.email "your_email@example.com" 等同于  git config --global --add user.email "your_email@example.com"
$ git config --global user.name "Firstname Lastname"
```

这两个命令会把邮箱和用户名设置在 `C:\Users\$USER` 目录下的 ` .gitconfig` 文件 中。

若没有 `.gitconfig` 文件，执行 `git config --global` 命令的时候则可生成 ~/.gitconfig 文件，`~` 代表当前用户目录，如 `C:\Users\kesyupeng`

仓库名 主干分支之类的属性存在仓库（项目） .git 文件夹下的 config 文件中。

对比一下三个参数的区别：

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
$ git config --list --show-origin 或者 cat ~/.gitconfig
```

#### 创建 SSH Key

```bash
$ ssh-keygen -t rsa -C "you_email@example.com"
然后按一次回车键，输入密码
代码参数含义：

-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。

cmd 下没有 ssh-keygen.exe
git 的安装目录下才有
生成的 id_rsa.pub 和 id_rsa 在 C:\Users\{$username}\.ssh 目录下

跳过不输入密码时，以后也不需要密码了（该密码是你 push 文件的时候要输入的密码，而不是登录 github 的密码）
要改会设置的话 可能就需要 ssh-keygen 命令了
```

查看公开秘钥

```bash
$ cat ~/.ssh/id_rsa.pub
```



用私人秘钥和 GitHub 进行认证和通信

```bash
$ ssh -T git@github.com
```



#### clone 已有仓库

```bash
$ git clone git@github.com:keyupeng/hello-world.git
```



克隆时会在当前目录下生成一个 hello-world 目录，这个目录就是 hello-world 项目，里面存放着项目源码



进入克隆好的项目

```bash
$ cd Hello-World
```



touch+文件名，直接新建一个文件

```bash
$ touch hello_world.php
```

新建一个文件并编辑，若文件存在直接编辑

```bash
$ vi hello_world.php
完成后按 esc，然后再输入 :wq 保存并退出
```

查看仓库状态

```bash
$ git status
```



将 hello_world.php 提交至仓库

```bash
$ git add hello_world.php
$ git commit -m "Add hello world script "
```

查看提交日志

```bash
$ git log
```

把新增的更改推送到远程服务器上

```bash
$ git push
```

















