---
date: 2026-01-24
tags:
  - 工具软件
  - GitHub
---
# Step 1
- 先在GitHub上面创建好仓库，得到如下界面
![[Pasted image 20260124162030.png]]
# Step 2
- 在本地文件夹位置打开终端，初始化一个git仓库
```
git init
```

- 推送至现有仓库
```
git remote add origin git@github.com:你的用户名/obsidian-notes.git
```

- 改名主分支为main
```
git branch -M main
```

- 添加文件
```
git add . // 添加所有文件
```

- commit
```
git commit -m "description"
```

- 上传远程仓库
```
git push -u origin main
```

# Step 3 初始化完成后的上传
```
git add .
git commit -m "descreption"
git push
```

- 如果在github上面进行更改过要先同步到本地
```
git pull origin main
```
# 遇到问题

## 验证链接
```
# 先删除原来的HTTPS远程地址
git remote remove origin

# 添加SSH远程地址（粘贴你刚复制的地址）
git remote add origin git@github.com:WhiteYan2006/First-Github-Test.git

# 验证远程地址是否正确
git remote -v
```

在更新 Obsidian 笔记并推送至 `First-Github-Test` 仓库时，遇到了 `non-fast-forward` 类型的推送失败错误，核心原因是**你的本地 `main` 分支提交记录落后于远程仓库的 `main` 分支**（比如你可能在 GitHub 网页上直接编辑过仓库文件、或之前推送过其他内容），Git 为了避免覆盖远程的最新内容，拒绝了这次 “非快进式” 推送。另外你看到的 `LF will be replaced by CRLF` 是换行符提示（非错误），我会先解决核心的推送报错，再解释这个警告。

## 一、核心问题：解决 non-fast-forward 推送失败

### 步骤 1：拉取远程最新内容并合并到本地（推荐，安全）

这是最规范的解决方案，先同步远程的最新内容到本地，再推送：

bash

运行

```
# 拉取远程main分支的最新内容，并自动合并到本地main分支
git pull origin main
```

- 如果拉取后提示**合并冲突**（比如你本地和远程都改了同一个文件）：
    
    打开冲突的文件（会看到 `<<<<<<< HEAD` `=======` `>>>>>>> xxx` 标记），手动保留需要的内容后保存；
    
    再执行 `git add .` 和 `git commit -m "解决合并冲突，同步远程内容"`。
- 如果没有冲突，Git 会自动完成合并，终端会提示类似「Merge made by the 'ort' strategy」。

### 步骤 2：重新推送本地更新


```
git push
```

### （可选，不推荐新手）强制推送（会覆盖远程内容）

如果你确定远程仓库的最新内容是无用的，想要强制用本地内容覆盖远程（**谨慎使用，可能丢失远程数据**）：

```
git push -f origin main
```

> 仅建议在自己的私有仓库、且确认远程内容无需保留时使用。

## 二、关于 LF/CRLF 警告的解释（非错误，可忽略 / 优化）

你看到的 `warning: LF will be replaced by CRLF` 是 Git 的换行符自动转换提示：

- LF：Linux/Mac 系统的换行符；
- CRLF：Windows 系统的换行符；
- Git 默认会在 Windows 下把文件中的 LF 转换成 CRLF（提交时再转回 LF），仅为适配不同系统的换行符规范，**不影响文件内容和推送**。

如果想关闭这个警告（可选），执行以下命令：

```
# 配置Git不自动转换换行符，仅在Windows下建议
git config --global core.autocrlf false
```

## 三、验证是否解决

推送成功后，终端会显示类似以下内容，且 GitHub 仓库页面能看到你更新的笔记，说明问题解决：

```
Enumerating objects: x, done.
Counting objects: 100% (x/x), done.
Writing objects: 100% (x/x), x bytes | x KiB/s, done.
Total x (delta x), reused 0 (delta 0)
To https://github.com/WhiteYan2006/First-Github-Test.git
   xxxxxxx..xxxxxxx  main -> main
```

### 总结

1. 核心原因：本地分支提交记录落后于远程，导致「non-fast-forward」推送失败，优先用 `git pull origin main` 同步远程内容后再推送；
2. 关键提醒：避免使用强制推送（`-f`），除非确认远程内容无需保留；
3. 换行符警告：`LF/CRLF` 是系统适配提示，不影响功能，可忽略或用 `core.autocrlf false` 关闭。