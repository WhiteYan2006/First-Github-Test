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

