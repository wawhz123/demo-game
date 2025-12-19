# 🎮 游戏大厅

一个纯前端的 H5 游戏集合，包含多种经典小游戏。

## 🎯 包含的游戏

- 🔗 **连线不相交** - 将相同颜色的圆点连起来，保证所有线段互不相交
- 🎮 **俄罗斯方块** - 经典消除游戏，支持触摸控制
- 🔢 **2048** - 数字合并益智游戏
- 🃏 **斗地主** - 经典卡牌游戏
- 🂡 **21点** - 挑战庄家的卡牌游戏

## 🚀 快速开始

### 本地运行

直接双击 `index.html` 文件，在浏览器中打开即可。

### 部署到 GitHub Pages

1. **首次部署**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/你的用户名/demo-game.git
   git push -u origin main
   ```
   然后在 GitHub 仓库 Settings → Pages 中启用 Pages。

2. **代码更新后**
   ```bash
   git add .
   git commit -m "更新说明"
   git push origin main
   ```
   ⏱️ **生效时间**：推送后 1-5 分钟内自动更新

## 📱 移动端支持

所有游戏都已适配移动设备，支持触摸操作：
- 触摸滑动控制
- 虚拟操作按钮
- 响应式布局

## 📚 详细文档

- [部署指南](./DEPLOY.md) - 完整的部署说明
- [GitHub Pages 部署和更新指南](./GITHUB_PAGES.md) - GitHub Pages 详细教程
- [部署检查清单](./DEPLOY_CHECKLIST.md) - 部署前检查项

## 🔄 更新流程

### 快速更新（GitHub Pages）

```bash
# 1. 修改代码
# 2. 提交更改
git add .
git commit -m "更新说明"
git push origin main

# 3. 等待 1-5 分钟，网站自动更新
# 4. 清除浏览器缓存后访问验证（Ctrl+F5）
```

### 加速更新

如果更新后网站没有变化：
1. 在 GitHub 仓库 Settings → Pages 中点击 **Save** 强制刷新
2. 清除浏览器缓存（Ctrl+F5 或 Cmd+Shift+R）
3. 等待几分钟后重试

## 🌐 访问地址

部署到 GitHub Pages 后，访问地址为：
```
https://你的用户名.github.io/demo-game/
```

## 📋 技术栈

- 纯 HTML/CSS/JavaScript
- 无依赖，无需构建工具
- 支持所有现代浏览器

## 📝 许可证

MIT License

---

**提示**：代码更新后，GitHub Pages 会在 1-5 分钟内自动更新。如果超过 5 分钟还没更新，可以在 Settings → Pages 中点击 Save 强制刷新。

