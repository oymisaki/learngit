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