# learn git

## config
```sh
git --config global user.name "xxx"
git --config global email.name "email"
```

## git start
```sh
mkdir learngit
cd learngit
git init
git add readme.md
git commit -m "wrote readme file"
git add file1.txt file2.txt
git commit -m "add 2 files"
```

## 时光机
```sh
git status
git diff # 看修改
git add readme.md
git status
git commit -m "add ..."
```

### 版本回退
```sh
git log
git log --pretty=oneline # 省略无关参数
git reset --hard HEAD^
# ^回退一个版本，^^回退两个版本
git reset --hard 1094a
# 回到指定版本
git reflog
# 忘记版本号，可以从这里找回
```

### 工作区与暂存区
1. 工作区 workspace, `git status` 显示 `untracked` 或者 `unstaged`.
2. 暂存区 通过 `git add` 添加到 `stage`， 
3. 版本库 通过 `git commit` 提交到 `repository`

### 管理、撤销修改
+ 每次修改要 `git add` 后才能**commit**到版本库，否则只在工作区
+ 要撤销修改：
  ```sh
  git checkout -- readme.md
  # 撤销文件工作区的修改
  git reset HEAD readme.md
  # 撤销文件暂存区的修改，
  ```

### 删除文件
```sh
rm test.txt
# 在工作区删除了文件
git rm text
git commit -m "remove test.txt"
# 在版本库中删除
git checkout -- test.txt
# 删错了，需要恢复
```

## 远程仓库

### 关联远程库
```sh
git remote add origin https://github.com/oymisaki/learngit.git  # 关联远程库
git push -u origin master
# 推送到远程库上， -u 表示将本地和远程的master分支关联起来
git push origin master
# 推送
```

### 克隆
```sh
git clone https://github.com/oymisaki/learngit.git
```
也可以使用 `git://` 协议，比 `https://` 协议更快

## 分支管理

### 创建与合并分支
> Git 创建分支实际上，创建一个分支指针，并将 `HEAD` 指针指向分支，在分支上修改上，分支的指针移动，合并时，将 `master` 的指针与分支的指针相同就完成合并
```sh
git branch dev # 创建新分支
git checkout dev # 切换分支
git merge dev # 合并分支
git branch -d dev # 删除分支

git branch # 列出分支
git checkout -b dev # 创建并切换分支
```

### 解决冲突
Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，修改好保存，再提交，手动提交冲突。

### bug分支
```sh
git stash
# 储存目前工作状态
git checkout -b issue-101
# 创建bug分支
git add readme.txt 
git commit -m "fix bug 101"
# 提交bug修复
git checkout master
git merge --no-ff -m "merged bug fix 101" issue-101
# 合并分支
```