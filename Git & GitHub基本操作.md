---
date: 2026-01-24
tags:
  - 工具软件
  - GitHub
---
# SSH配置以及Git常用命令

## SSH：安全认证和便捷连接
- SSH允许在本地仓库和远程仓库之间安全通信，并省去每次推送或拉取代码时输入密码的麻烦

## SSH配置步骤

- 配置个人信息
```
git config --global user.name "Your Name"
git config --global user.email "Your Email" 
```

- 生成SSH密钥
```
ssh-keygen -t rsa -C "Your Email"
```

- `-t rsa`：使用RSA算法生成密钥
- `-C`：添加备注，一般是邮箱地址

- 生成后的密钥保存在`C:\Users\XXX/.ssh/id_rsa`
- `id_rsa`为私钥，`id_rsa.pub`为公钥

- 在GitHub的设置中的SSH与GPG公钥中添加新的SSH密钥，把`id_rsa.pub`中的公钥粘贴进去

- 连接测试
```
ssh -T git@github.com
```
选`yes`保存信息


## Git 常用命令

| 功能        | 命令                                                                                    | 比喻                        |
| --------- | ------------------------------------------------------------------------------------- | ------------------------- |
| 配置用户名和邮箱  | `git config --global user.name "你的名字"`<br><br>`git config --global user.email "你的邮箱"` | 设置 “署名”，每次提交都会标明是谁的贡献。    |
| 初始化仓库     | `git init`                                                                            | 新建一本 “时光机日记本”，准备开始记录代码版本。 |
| 添加文件到暂存区  | `git add 文件名`                                                                         | 把草稿整理好，放到提交的 “草稿区”。       |
| 提交到本地仓库   | `git commit -m "提交说明"`                                                                | 把草稿正式写进日记本，并附上说明。         |
| 推送代码到远程仓库 | `git push origin 分支名`                                                                 | 把本地代码同步上传到远程仓库。           |
| 克隆远程仓库    | `git clone 仓库地址`                                                                      | 下载别人的代码到本地。               |
| 查看状态      | `git status`                                                                          | 检查当前代码的变化情况。              |
| 查看提交历史    | `git log`                                                                             | 查看代码的提交记录，回顾开发的 “时间线”。    |
| 创建分支      | `git branch 分支名`                                                                      | 为不同功能开发创建独立章节，不干扰主线内容。    |
| 切换分支      | `git checkout 分支名`                                                                    | 从一个章节切换到另一个章节。            |
| 合并分支      | `git merge 分支名`                                                                       | 把不同章节的内容合并到主线。            |
| 拉取代码      | `git pull origin 分支名`                                                                 | 从远程仓库拉取最新代码。              |
