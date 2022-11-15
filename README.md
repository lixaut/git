# git 命令



### 1. 基本配置



##### 1.1 用户信息配置

```bash
# 配置用户名
git config --global user.name <user_name>
# 配置用户邮箱
git config --global user.email <user_email>
```

##### 1.2 初始化仓库

```bash
git init
```

##### 1.3 配置 git 命令变量（别名）

```bash
# 本地用户（~）根目录下创建 .bashrc 文件
touch ~/.bashrc
# 文件输入内容
alias git-log='git log --pretty=oneline --abbrev-commit --all --graph'
# 添加环境变量
source ~/.bashrc
```

##### 1.4 解决 git bash 乱码问题

```bash
# 执行命令
git config --global core.quotepath false
# ${git_home}/etc/bash.bashrc 文件最后加入下面两行
export LANG="zh_CN.UTF-8"
export LC_ALL="zh_CN.UTF-8"
```



### 2. 常用命令



##### 2.1 提交至暂存区

```bash
# 提交工作区全部变动
git add .
# 提交指定文件
git add <file_name> <file_name>
```

##### 2.2 提交至本地仓库

```bash
# 暂存区提交到本次仓库
git commit -m 'commit message'
# 工作区直接提交到本地仓库
git commit -am 'commit message'
```

##### 2.3 查看当前分支状态

```bash
# 查看文件修改状态（完整）
git status
# （简化）
git status -s
```

##### 2.4 查看本地仓库提交记录

```bash
# 完整
git log
# 信息一行显示
git log --pretty=oneline
# 缩写提交hash值（7位）
git log --pretty=oneline --abbrev-commit
# 显示所有分支
git log --pretty=oneline --abbrev-commit --all
# 图形化显示所有分支
git log --pretty=oneline --abbrev-commit --all --graph
# 查看所有相关记录
git reflog
```

##### 2.5 版本回退

soft 使用场景：撤销提交记录，修改提交信息，重新提交

hard 使用场景：清空当前版本所有东西，重新开始，推翻重来

reflog 上帝视角，可以回到任何一个操作节点

还未被跟踪的新文件，不适合用 git 命令操作回退

```bash
# 清空当前版本的所有内容（工作区、暂存区、本地仓库提交记录）
git reset --hard <hash(7)>
# 仅重置当前版本的本地仓库提交记录
git reset --soft <hash(7)>
# 只保留当前版本的工作区（重置暂存区、本地仓库提交记录）
git reset <hase(7)>
```



### 3. 分支



##### 3.1 查看本地分支

```bash
git branch
```

##### 3.2 创建本地分支

```bash
git branch <branch_name>
```

##### 3.3 切换分支

```bash
git checkout <branch_name>
git switch <branch_name>
```

##### 3.4 创建并切换分支

```bash
git checkout -b <branch_name>
```

##### 3.5 合并分支

```bash
git merge <branch_name>
```

合并分支时解决冲突：

1. 处理文件中冲突的地方
2. 将解决完冲突的地方加入暂存区（add）
3. 提交到仓库（commit）

##### 3.6 删除分支

```bash
git branch -d <branch_name>
# 强制删除
git branch -D <branch_name>
```

##### 3.7 开发中分支使用原则与流程

在开发中，一般有如下分支使用原则与流程：

* master 分支（生产）
* develop 分支（开发）
* feature/xxx 分支
* hotfix/xxx 分支
* 其他分支 test 分支 / pre 分支



### 4. Git 远程仓库



##### 4.1 生成密钥

```bash
ssh-keygen -t rsa -C "QinBerg@gmail.com"
# -t 指定加密算法
# -C 注释，一般填写用户名
```

##### 4.2 添加远程仓库

```bash
git remote add <仓库别名> <仓库路径>
git remote add origin git@github.com:.../...git
```

##### 4.3 查看远程仓库

```bash
git remote
```

##### 4.4 推送到远程仓库

```bash
git push origin master
```

第一次推送建立分支关联关系，后面就不需要再次指定远程分支，`--set-upstream 简写 -u`

```bash
# 第一次
git push -u origin master
# 第二次
git push
# 查看远程仓库分支与本地分支关联关系
git branch -vv
```

##### 4.5 拉取和抓取

```bash
# 抓取：将仓库里的更新都抓取到本地，不会合并
git fetch <remoteName> <branchName>
# 拉取：将仓库里的修改拉到本地并自动进行合并
git pull <remoteName> <branchName>
```

