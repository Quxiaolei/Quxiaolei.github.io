# Git 常用命令总结

[⬅️ Back](./)

<!-- TOC -->
- [Git 常用命令总结](#git-常用命令总结)
    - [Git 理论基础](#git-理论基础)
      - [工作区](#工作区)
      - [Git config](#git-config)
    - [Git 基础](#git-基础)
      - [仓库初始](#仓库初始)
      - [仓库状态](#仓库状态)
      - [修改管理](#修改管理)
      - [远程仓库](#远程仓库)
    - [参考资料](#参考资料)

<!-- /TOC -->

## Git 理论基础

### 工作区

Git 的三个工作区概念：

- 工作目录：展示工程某个版本的内容
- 暂存区（索引）：保存了下次将提交的文件列表信息
- Git 仓库：保存项目的元数据和对象数据库

![工作目录、暂存区域以及 Git 仓库](./imgs/git_areas.png)

一般的工作流程就是：

从 `Git 仓库` 中拉取项目工程到本地；在 `工作目录` 中修改文件后暂存文件，可将待提交的文件提交至 `暂存区` ，commit 后即将文件从暂存区提交至 `Git 仓库`。

### Git config

在设备中有三个等级的 config 文件：

1. `/etc/gitconfig` 文件

   包含系统的所有每个用户及仓库的通用配置，可以使用 `--system`  配置。

2. `~/.gitconfig` 或 `~/.config/git/config` 文件
   只针对当前用户，可以使用 `--global` 配置。

3. `.git/config`

   只针对当前仓库。

常见的配置命令：

```shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
# 设置默认文本编辑器
git config --global core.editor emacs
# 查看 Git 配置
git config --list
# 检查某项配置
git config user.name
# 删除全局设置
git config --global --unset <entry-name>
```

## Git 基础

### 仓库初始

| 命令                                                      | 释义                                                         |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| `git init`                                                | 创建仓库                                                     |
| `git add`<br />`git add .`<br />git add -f                | 把文件添加到 `暂存区`<br />将工作区所有文件添加到 `暂存区`<br />强制添加文件 |
| `git commit`<br />`-m`<br />`-v`<br />`-a`<br />`--amend` | 将 `暂存区` 文件提交到 Git<br />将提交信息和命令放在一行<br />将 diff 信息作为提交信息<br />跳过提交到 `暂存区` 的步骤，直接提交<br />尝试重新提交（如果未做变动时，只会覆盖提交信息） |

`.gitignore` 忽略文件配置：

```shell
cat .gitignore
```

[github_gitignore_ A collection of useful .gitignore templates](https://github.com/github/gitignore)

### 仓库状态

| 命令                                                         | 释义                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `git status`<br />`git status --short`<br/>`git status -s`   | 查看仓库的当前状态（含未提交变动）<br />查看简版仓库修改     |
| `git diff`<br />`git diff --cached`<br />`git diff HEAD`<br />`git diff --stat`<br />`git diff <commit-id> <commit-id>` | 比较 `工作目录` 与 `暂存区` 文件（即上次 `git add` 的内容）的区别<br />比较 `暂存区` 文件与仓库文件（即上次 `git commit` 后的内容）的区别<br />比较 `工作目录` 与仓库当前版本文件的区别<br />显示变动的摘要信息<br />展示任意两个 commit 之间的文件变动 |
| `git log`<br />`git log -p`<br />`git log --stat`<br />`git log --pretty=oneline`<br />`git log --pretty=format:"%h %s" --graph` | 查看 Git 操作历史记录<br />显示每次提交的内容差异<br />显示每次提交的简略统计信息<br />格式化历史记录信息为一行<br />格式化历史记录信息显示分支和合并历史 |
| `git reflog`                                                 | 查看命令历史                                                 |

### 修改管理

| 命令                                                         | 释义                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `git checkout -- <file>`<br />`git checkout .`               | 丢弃 `工作区` 某文件的变动<br />丢弃所有文件的变动           |
| `git reset`<br />`git reset --hard HEAD^`<br/>`git reset --hard <commit_id>`<br />`git reset HEAD` <file> | 回退到某个版本<br />回到上一版本<br />回到某次提交<br />撤销 `暂存区` 已修改的内容 |
| `git rm <file>`<br />`git rm -f <file>`<br />`git rm --cached <file>`<br />`git rm -r *` | 从 `暂存区` 中移除某个文件<br />强制删除文件<br />把文件从暂存区删除<br />递归删除该目录下的所有文件和子目录 |
| `git mv`                                                     | 用于移动或重命名一个文件、目录、软连接                       |
| `git stash`<br />`git stash list`<br />`git stash apply <name>`<br />`git stash drop <name>`<br />`git stash pop <name>` | 贮藏代码<br />查看贮藏代码<br />应用贮藏<br />移除贮藏<br />应用贮藏并移除 |
| `git cherry-pick <commit id>`                                | 从某个分支上选择某次提交应用到当前分支                       |

在 Git中用 `HEAD` 表示当前版本，上一个版本就是 `HEAD^`，上上个版本是 `HEAD^^` 或 `HEAD^2`。

### 远程仓库

| 命令                                                         | 释义                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `git remote add <shortname> <repo>`<br />`git remote`<br />`git remote -v`<br />`git remote show <remote-name>`<br />`git remote rename <remote-name> <remote-name>`<br />`git remote rm <remote-name>`<br />`git remote set-url origin <URL>` | 添加一个新的远端 Git 仓库<br />查看远程仓库服务器<br />显示需要读写远程仓库分支和对应 URL<br />查看某一个远程仓库的更多信息<br />修改一个远程仓库的简写名<br />远程仓库的移除<br />修改远程仓库的 url |
| `git clone <repo> <directory>`<br />`--depth=1`<br />`--recursive` | 克隆仓库到指定的目录<br />只会 clone 最近一次提交<br />自动初始化并更新仓库中的每一个子模块 |
| `git fetch <remote-name>`                                    | 抓取克隆（或上一次抓取）后新推送的所有工作                   |
| `git merge`                                                  | 合并指定分支到当前分支                                       |
| `git pull`<br />`git pull --rebase origin <branch-name>`     | 自动抓取并合并远程分支到当前分支<br />强制把远程库的代码跟新到当前分支上面 |
| `git push <remote-name> <branch-name>`<br />`git push -u`<br />`git push <remote-name> --delete <branch-name>`<br />`git push origin <tagname>`<br />`git push origin --tags` | 推送分支到远端<br />推送代码到远端，并将本地分支与远端分支关联<br />删除远端分支<br />将标签推送到远端<br />一次推送多个标签到远端 |
| `git checkout <name>`<br />`git checkout <tagname>`<br />`git checkout -b <name> <branch-name>`<br />`git checkout --track <branch-name>` | 切换分支<br />检出标签<br />创建并切换分支<br />快速创建并切换分支 |
| `git branch`<br />`git branch <name>`<br />`git branch -d/-D <name>`<br />`git branch -v/-vv`<br />`git branch --merged/--no-merged`<br />`git branch -u <name>`<br />`git branch --set-upstream-to=<remote-branch> <branch>` | 查看当前分支<br />创建分支<br />删除（强制删除）分支<br />查看所有分支的最后一次提交<br />查看合并（未合并）到当前分支的分支<br />设置当前分支追踪的远程分支<br />指定本地分支与远程分支的链接 |
| `git rebase <branch>`                                        | 将提交到某一分支上的所有修改都移至另一分支上                 |
| `git tag`<br />`git tag -a <tag>` <commit id><br />`git tag -a <tag> -m '<description>'`<br />`git tag -d <tag>` | 查看 tag<br />添加 tag<br />创建一个附注 tag<br />删除标签   |
| `git show <tag>`                                             | 查看标签信息与对应的提交信息                                 |
| `git submodule init`<br /><br />`git submodule update`<br />`git submodule add <URL>`<br />`git submodule foreach <command>` | 初始化子模块本地配置文件<br />从项目中抓取所有数据并检出父项目中的提交<br />为仓库添加子模块<br />遍历 submodule 做某操作 |

## 参考资料

- [GIT CHEAT SHEET](./resources/git-cheatsheet.pdf)
- [Git教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)
- [Git的奇技淫巧](https://github.com/521xueweihan/git-tips)
- [git - the simple guide - no deep shit!](http://rogerdudler.github.io/git-guide/index.zh.html)

---

[⬅️ Back](./)

[⬆️ 回到顶部 ⬆️](#git-常用命令总结)