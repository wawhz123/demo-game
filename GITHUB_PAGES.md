# GitHub Pages 部署和更新指南

## 🚀 首次部署到 GitHub Pages

### 步骤 1：创建 GitHub 仓库

1. 登录 GitHub，点击右上角 `+` → `New repository`
2. 填写仓库信息：
   - **Repository name**: `demo-game`（或你喜欢的名字）
   - **Description**: 游戏大厅 - H5游戏集合
   - **Visibility**: Public（GitHub Pages 免费版需要公开仓库）
   - **不要**勾选 "Initialize this repository with a README"
3. 点击 `Create repository`

### 步骤 2：初始化本地 Git 仓库并推送代码

在项目目录下执行以下命令：

```bash
# 初始化 Git 仓库
git init

# 添加所有文件
git add .

# 提交代码
git commit -m "Initial commit: 游戏大厅"

# 添加远程仓库（替换为你的用户名和仓库名）
git remote add origin https://github.com/你的用户名/demo-game.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

### 步骤 3：启用 GitHub Pages

1. 进入你的 GitHub 仓库页面
2. 点击顶部菜单栏的 **Settings**（设置）
3. 在左侧菜单中找到 **Pages**（页面）
4. 在 **Source**（源）部分：
   - 选择 **Branch**: `main`
   - 选择 **Folder**: `/ (root)`
5. 点击 **Save**（保存）
6. 等待几分钟，GitHub 会显示你的网站地址：
   ```
   https://你的用户名.github.io/demo-game/
   ```

## 🔄 代码变更后如何生效

### 方法一：使用 Git 命令（推荐）

每次修改代码后，执行以下命令：

```bash
# 1. 查看修改的文件
git status

# 2. 添加修改的文件
git add .

# 或者只添加特定文件
git add game-tetris.html

# 3. 提交更改
git commit -m "更新: 适配智能手机触摸控制"

# 4. 推送到 GitHub
git push origin main
```

**生效时间**：
- GitHub Pages 会在推送后 **1-5 分钟**内自动更新
- 如果超过 5 分钟还没更新，可以：
  1. 在仓库 Settings → Pages 中点击 "Save" 强制刷新
  2. 清除浏览器缓存（Ctrl+F5 或 Cmd+Shift+R）

### 方法二：使用 GitHub 网页界面

1. 进入你的 GitHub 仓库
2. 点击要修改的文件（如 `game-tetris.html`）
3. 点击右上角的 **✏️ Edit**（编辑）按钮
4. 修改代码
5. 滚动到底部，填写提交信息：
   - **Commit message**: `更新: 适配智能手机触摸控制`
6. 选择 **Commit directly to the main branch**
7. 点击 **Commit changes**

**生效时间**：同样需要 1-5 分钟

## 📝 常用 Git 命令速查

```bash
# 查看当前状态
git status

# 查看修改内容
git diff

# 添加所有修改
git add .

# 添加特定文件
git add 文件名.html

# 提交更改
git commit -m "提交说明"

# 推送到 GitHub
git push origin main

# 查看提交历史
git log --oneline

# 撤销未提交的修改（危险操作）
git checkout -- 文件名.html

# 撤销已添加但未提交的文件
git reset HEAD 文件名.html
```

## 🔍 验证更新是否生效

### 方法 1：检查 GitHub Actions（如果有）

1. 进入仓库页面
2. 点击 **Actions** 标签
3. 查看最新的部署状态（绿色 ✓ 表示成功）

### 方法 2：清除浏览器缓存后访问

- **Windows**: `Ctrl + F5` 或 `Ctrl + Shift + R`
- **Mac**: `Cmd + Shift + R`
- **移动端**: 清除浏览器缓存或使用无痕模式

### 方法 3：添加版本号验证

在 HTML 文件中添加版本号注释，更新后检查：

```html
<!-- Version: 1.0.1 - 2024-01-15 -->
```

## ⚡ 加速更新生效的技巧

### 1. 强制刷新 GitHub Pages

在仓库 Settings → Pages 中：
- 点击 **Save** 按钮（即使没有修改设置）
- 这会触发一次新的部署

### 2. 使用 GitHub Actions 自动部署（高级）

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
```

### 3. 添加缓存破坏参数

在 HTML 文件的引用中添加版本号：

```html
<link rel="stylesheet" href="style.css?v=1.0.1">
<script src="script.js?v=1.0.1"></script>
```

## 🐛 常见问题

### 问题 1：推送后网站没有更新

**解决方案**：
1. 等待 5-10 分钟（GitHub Pages 有缓存）
2. 清除浏览器缓存
3. 在 Settings → Pages 中点击 Save 强制刷新
4. 检查仓库的 Actions 标签，查看部署状态

### 问题 2：Git 推送失败

**错误信息**：`error: failed to push some refs`

**解决方案**：
```bash
# 先拉取远程更改
git pull origin main --rebase

# 解决冲突后再次推送
git push origin main
```

### 问题 3：文件路径错误导致 404

**检查**：
- 确保所有文件都在仓库根目录
- 检查文件路径大小写（GitHub 区分大小写）
- 确保 HTML 中的链接使用相对路径

### 问题 4：GitHub Pages 显示 404

**解决方案**：
1. 确认仓库是 Public（公开）
2. 确认在 Settings → Pages 中已启用
3. 确认选择了正确的分支（main）和目录（/）
4. 等待几分钟后重试

## 📱 移动端访问

GitHub Pages 自动支持 HTTPS，可以直接在手机上访问：
```
https://你的用户名.github.io/demo-game/
```

## 🔐 使用自定义域名（可选）

1. 在仓库 Settings → Pages → Custom domain 中输入你的域名
2. 在域名 DNS 中添加 CNAME 记录：
   ```
   类型: CNAME
   名称: @ 或 www
   值: 你的用户名.github.io
   ```
3. 等待 DNS 生效（通常几分钟到几小时）

## 📊 监控部署状态

### 查看部署历史

1. 进入仓库 Settings → Pages
2. 查看 **Deployments**（部署）部分
3. 可以看到每次部署的时间和状态

### 查看网站访问统计（需要 GitHub Pro）

GitHub Pages 不提供访问统计，可以：
- 使用 Google Analytics
- 使用其他第三方统计服务

## ✅ 更新检查清单

每次更新代码后：

- [ ] 代码已提交到本地仓库
- [ ] 代码已推送到 GitHub
- [ ] 等待 1-5 分钟
- [ ] 清除浏览器缓存后访问网站
- [ ] 验证功能是否正常
- [ ] 测试移动端访问

## 🎯 快速更新流程总结

```bash
# 1. 修改代码
# 2. 提交更改
git add .
git commit -m "更新说明"
git push origin main

# 3. 等待 1-5 分钟
# 4. 清除缓存后访问网站验证
```

---

**提示**：GitHub Pages 是免费的，但更新有延迟。如果需要即时更新，可以考虑使用 Vercel 或 Netlify（它们支持自动部署且更新更快）。

