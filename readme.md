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
```

*这是用来测试的时光机的行*