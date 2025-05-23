# Git  常用操作及技巧

[GIT 命令大全](http://www.cnblogs.com/Small-music/p/9075681.html)

## Git 分支命令

- 创建name的分支，并切换过去
```sh
      git checkout -b name
```
- 拉取远程分支，创建并切换到这个分支
```sh
      git checkout -b name origin/remote-branch
      git checkout -b 本地分支名 origin/远程分支名
```
- 查看所有分支
```sh
      git branch -v
```
- 删除分支
```sh
      git branch -d name
      git branch -D name
```
- 合并到master
```sh
      git checkout master
      git merge name
```
- 暂存所有更改到本地分支
```sh
      git stash
```
- 恢复
```sh
      git stash pop
```

## Git 撤销本地提交
```
git reset --mixed HEAD~2
```

## Git 中设置代理

### 设置 http 代理
```sh
git config --global https.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080

git config --global --unset http.proxy
git config --global --unset https.proxy
```

### 设置 socks5 代理

```sh
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

### 查看环境关于代理的环境变量
```sh
env|grep -i proxy
```

### Linux设置/删除环境变量方法

#### bash

- 设置：export 变量名=变量值
- 删除：unset 变量名

#### csh

- 设置：setenv 变量名 变量值
- 删除：unsetenv 变量名

## Git 推本地 master 到远端非 master 分支
```sh
git push origin master:fix_branch
```

## 添加 submodule

为当前工程添加submodule，命令如下：

```
git submodule add repo_url path
```

其中，repo_url 是指子模块仓库地址，path 指将子模块放置在当前工程下的路径。 
注意：路径不能以 / 结尾（会造成修改不生效）、不能是现有工程已有的目录（不能顺利 Clone）。

命令执行完成，会在当前工程根路径下生成一个名为“.gitmodules”的文件，其中记录了子模块的信息。添加完成以后，再将子模块所在的文件夹添加到工程中即可。

强制添加可以使用  --force 参数。

## 更新 submodule

更新当前仓库中的 submodule，命令如下：

```sh
git submodule update --init --recursive
```

参数 `--recursive` 的意思是递归更新子模块，也就是会更新子模块的子模块，如果不加这个参数，则只会更新第一级的子模块。

## 删除 submodule

删除当前仓库中的 submodule，方法如下：

- 删除 .gitsubmodule  文件中对应的 submodule。

- 删除 .git/config 中对应的 submodule 项（这一步我测试的时候如果不做也可以，后面再次添加子模块的时候加上 --force 参数也可以再次添加）。

- 执行命令 `git rm --cached <submodule_path>`，执行命令前，请确保该 Git 仓库没有未提交的内容，否则会执行失败，示例如下：

```sh
git rm --cached hello
```

## GIT 与远程 REPOSITORY 同步 TAG 和BRANCH

参考如下地址：http://smilejay.com/2013/04/git-sync-tag-and-branch-with-remote/

## 输入输出均不转换换行符

```sh
git config --global core.autocrlf false
```
## 克隆时指定日志层数

这种方法可以减少下载文件的数量，大大提高下载速度。

```sh
git clone --depth=1 Git_URL
```

## Enter passphrase for key problem

git 配置完 SSH 以后，push 或者 pull 的时候每次都提示 Enter passphrase for key '/Users/m/.ssh/id_rsa': ，可以这样解决:

1. 终端输入
```
eval `ssh-agent`
ssh-add
```
但是关闭终端窗口，或者重新就必须重新输入，治标不治本。

2. 终端输入
```
ssh-add -k /Users/m/.ssh/id_rsa
ssh-add -K privateKey 中privateKey 为/Users/m/.ssh/id_rsa
```

## 多个 commit 合并

下面是把 4 个 commit 合并成一个：

```shell
git reset --mixed HEAD~4
```

## 回退某个文件版本

要在 Git 中将某个文件回退到指定版本，你可以使用 git checkout 命令，后面跟上想要回退到的提交的哈希值和文件路径。这里是具体的步骤：

1. 首先，找到你想要回退到的版本的提交哈希值。你可以使用 git log 命令查看提交历史，找到对应的提交哈希值。

```
  git log -- path/to/your/file
```

这会显示该文件的提交历史，你可以从中找到你想要回退到的那个版本的哈希值。

2. 使用 git checkout 命令回退文件：

```
  git checkout <commit-hash> -- path/to/your/file
```

将 <commit-hash> 替换为你在第一步中找到的哈希值，path/to/your/file 替换为你想要回退的文件的路径。

这样，指定的文件就会被回退到你选择的版本。如果你想要保留这个更改，可以直接提交这个回退的文件。

