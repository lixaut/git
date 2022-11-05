# git 学习



### 基本配置

用户信息配置

```bash
# 配置用户名
git config --global user.name <username>

# 配置用户邮箱
git config --global user.email <useremail>
```



### 常用命令

提交暂存区
```bash
# 提交工作区全部变动
git add .

# 提交指定文件
git add <filename> <filename>
```

提交本地仓库
```bash
# 暂存区提交到本次仓库
git commit -m 'commit message'

# 工作区直接提交到本地仓库
git commit -am 'commit message'
```

