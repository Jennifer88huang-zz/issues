## 贡献流程

如果仓库禁用了 `Fork` 功能，你不能 fork。

### 第 1 步：克隆仓库

1. 访问 https://github.com/repo
2. 克隆仓库

    ```bash
    mkdir -p $working_dir
    cd $working_dir
    git clone https://github.com/repo.git
    ```

### 第 2 步：同步分支内容

同步本地 master 分支内容。

```bash
cd $working_dir/doc-platform
git fetch origin
git rebase origin/master
```

### 第 3 步：创建分支

基于 master 分支创建新分支。以下代码创建了 `my-branch` 这一分支。

```bash
git checkout -b my-branch
```

### 第 4 步：编辑分支

基于 `my-branch` 分支，对本地文档进行编辑。

### 第 5 步：提交修改

通过以下代码提交修改到新创建的分支。

```bash
git add <filename> 
git commit -m "$add a comment"
```

你可以进行多次提交。

提交修改时，你可能会用到以下命令：
```bash
git add <filename> (add one file)
git add -A (add all changes, including new/delete/modified files)
git add -a -m "$add a comment" (add and commit modified and deleted files)
git add -u (add modified and deleted files, not include new files)
git add . (add new and modified files, not including deleted files)
```

### 第 6 步：推送分支

提交修改到分支后，你可以通过以下代码将此分支推送到原仓库。

```bash
git push origin my-branch
```

### 第 7 步：创建 Pull Request

1. 访问 https://github.com/repo
2. 点击 `my-branch` 分支旁边的 **Compare & pull request** 按钮创建 Pull Request。
