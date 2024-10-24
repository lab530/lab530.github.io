+++
slug = "Blogging Guidelines Collaborative Development"
title = '博客须知(协同开发)'
date = 2024-09-16T19:23:49+08:00
weight=1
draft = false

+++

###  !!! 写博客前先看此文




## 1. 切换到主分支
在开始新功能的开发前，首先需确保你的主分支是最新的。您可以通过以下命令切换到 `main` 分支并拉取最新的代码：

```bash
git checkout main
git pull
```

## 2. 创建新功能分支

拉取完最新的代码后，可以基于 `main` 分支切换到新功能分支。这里以模块名为例创建一个功能分支：

```bash
git checkout -b backend/feature/模块名
```



## 3. 完成功能开发后切回开发分支

在功能开发结束后，需要将工作目录切换回开发分支，以便进行后续的合并操作。这里假设您的开发分支为 `backend/develop`(第一次执行时git checkout -b backend/develop)：

```bash
git checkout backend/develop
```



## 4. 合并功能分支

现在，您可以将新创建的功能分支合并到开发分支中。执行以下命令进行合并：

```bash
git merge backend/feature/模块名
```



确保没有冲突后，您就成功将功能合并到开发分支了。

## 5. 合并到主分支

在 `backend/develop` 分支的版本稳定之后，您可以将这些更改合并到 `main` 分支。请按照以下步骤操作：

首先，确保在 `backend/develop` 分支上合并 `main` 分支的最新更新：

```bash
git merge main
```



接着，切换到 `main` 分支并合并开发分支：

```bash
git checkout main
git merge backend/develop
```



## 6. 提交更改

最后，将所有改动提交到远程仓库。请按照以下命令逐步进行：

```bash
git add .
git commit -m "描述您的更改内容"
git push
```

