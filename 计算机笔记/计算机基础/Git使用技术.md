# 工作流程

- 克隆 Git 资源作为工作目录。
- 在克隆的资源上添加或修改文件。
- 如果其他人修改了，你可以更新资源。
- 在提交前查看修改。
- 提交修改。
- 在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。

![img](../../_Repertory/res/Git使用技术.assets/git-process.png)

# 概念辨析

# Git 工作区、暂存区和版本库

- 工作区
- 暂存区：英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- 版本库：工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

# 实战使用
## 用户管理
配置用户名和邮箱


## 创建仓库

#### git init

Git 使用 **`git init`** 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 **`git init`** 是使用 Git 的第一个命令。

#### git add

```shell
git add *.c
git add -A # 追加所有操作
```

#### git commit

```shell
git commit -m '提交说明'
```

**注：** 在 Linux 系统中，commit 信息使用单引号 **'**，Windows 系统，commit 信息使用双引号 **"**。

所以在 git bash 中 **git commit -m '提交说明'** 这样是可以的，在 Windows 命令行中就要使用双引号 **git commit -m "提交说明"**。

#### git clone

```shell
git clone
```

我们使用 **git clone** 从现有 Git 仓库中拷贝项目（类似 **svn checkout**）。

克隆仓库的命令格式为：

```shell
git clone <repo>
```

如果我们需要克隆到指定的目录，可以使用以下命令格式：

```shell
git clone <repo> <directory>
```

## 基本操作

![img](../../_Repertory/res/Git使用技术.assets/git-command.jpg)

#### 常用的六大命令：

1. 克隆文件：git clone/fetch
2. 推送文件：git push
3. 拉取文件：git pull
4. 添加文件：git add
5. 提交说明：git commit
6. 切换分支：git checkout

#### 提交与修改

| 命令         | 说明                                     |
| :----------- | :--------------------------------------- |
| `git add`    | 添加文件到暂存区                         |
| `git status` | 查看仓库当前的状态，显示有变更的文件。   |
| `git diff`   | 比较文件的不同，即暂存区和工作区的差异。 |
| `git commit` | 提交暂存区到本地仓库。                   |
| `git reset`  | 回退版本。                               |
| `git rm`     | 将文件从暂存区和工作区中删除。           |
| `git mv`     | 移动或重命名工作区文件。                 |

#### 远程操作

| 命令         | 说明               |
| :----------- | :----------------- |
| `git remote` | 远程仓库操作       |
| `git fetch`  | 从远程获取代码库   |
| `git pull`   | 下载远程代码并合并 |
| `git push`   | 上传远程代码并合并 |

#### 分支操作

创建分支命令：

```shell
git branch -b (branchname)
```

切换分支命令:

```shell
git checkout (branchname)
```

合并分支命令:

```shell
git merge (branchname)
```

删除分支命令：

```shell
git branch -d (branchname)
```

#### 标签操作

查看标签：

```shell
git tag
```

创建标签：

```shell
git tag -a v1.0
```
