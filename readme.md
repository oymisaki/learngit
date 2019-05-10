# learn git

## config
```sh
git config --global user.name "xxx"
git config --global email.name "email"
# 还可以使用--local选项
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
```
git log --graph --pretty=oneline --abbrev-commit
# 查看分支情况
git branch -d feature1
# 删除分支
```

### 分支策略
```sh
git merge --no-ff -m "merge with no-ff" dev
# 加上 --no-ff 参数，就不是 fast forward 模式，能够保存分支信息，并且会变成commit，所以要加后面的参数
```

>首先，`master` 分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
>
>那在哪干活呢？干活都在  `dev`  分支上，也就是说， `dev` 分支是不稳定的，到某个时候，比如1.0版本发布时，再把 `dev`分支合并
>
>到 `master`上，在 `master` 分支发布1.0版本；
你和你的小伙伴们每个人都在 `dev` 分支上干活，每个人都有自己的分支，时不时地往 `dev` 分支上合并就可以了。

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

git stash list
# 看工作现场列表
git stash pop
# 恢复工作现场
```

恢复工作现场也可以用，**如果恢复现场时出现冲突时，解决冲突后，需要提交并将stash中储存的工作区手动drop掉**
```sh
git stash apply id
# 恢复，但是不删除
git stash drop id
# 需要手动给删除
```

### 多人协作

```sh
git remote # 看远程库信息
git remove -v # 更详细的信息

git checkout -b dev origin/dev
# 默认clone下来的是master分支，如果要在dev分支上开发，要将远程的dev分支克隆到本地
```

多人协作，`push` 到一个分支时可能会出现冲突，这时需要把分支的新提交 `pull` 到本地后，手动合并冲突

```sh
git checkout -b dev origin/dev
# 现在本地创建同名分支
git branch --set-upstream-to=origin/dev dev
git pull
# 指定本地与远程的分支链接后，拉到本地，解决冲突
git commit -m "fix env conflict"
# 提交到dev分支
git push origin dev
# 推送鬼刀远程库的dev分支
```
如果多人提交，在历史上会产生分支，使用 `rebase` 命令，将所有的历史分支变成历史一条线，更干净好看

```sh
git rebase
```
