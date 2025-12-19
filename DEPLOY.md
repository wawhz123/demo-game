# 游戏大厅部署指南

本项目是一个纯前端的H5游戏集合，可以轻松部署到任何静态文件托管服务。

## 📁 项目文件结构

```
demo-flow/
├── index.html              # 游戏大厅主页
├── game-flow.html          # 连线游戏
├── game-tetris.html        # 俄罗斯方块
├── game-2048.html          # 2048游戏
├── game-doudizhu.html      # 斗地主
├── game-blackjack.html     # 21点
└── DEPLOY.md              # 本部署文档
```

## 🚀 部署方式

### 方式一：GitHub Pages（推荐，免费）

1. **创建GitHub仓库**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/你的用户名/demo-flow.git
   git push -u origin main
   ```

2. **启用GitHub Pages**
   - 进入仓库 Settings
   - 找到 Pages 选项
   - Source 选择 `main` 分支，`/ (root)` 目录
   - 点击 Save
   - 等待几分钟，访问 `https://你的用户名.github.io/demo-flow/`

### 方式二：Vercel（推荐，免费，快速）

1. **安装Vercel CLI**
   ```bash
   npm install -g vercel
   ```

2. **部署**
   ```bash
   cd demo-flow
   vercel
   ```
   按照提示完成部署，会自动获得一个 `xxx.vercel.app` 域名

3. **或通过网页部署**
   - 访问 https://vercel.com
   - 使用GitHub账号登录
   - 点击 New Project
   - 导入你的GitHub仓库
   - 自动部署完成

### 方式三：Netlify（推荐，免费）

1. **通过网页部署**
   - 访问 https://www.netlify.com
   - 注册/登录账号
   - 点击 "Add new site" -> "Deploy manually"
   - 拖拽整个项目文件夹到页面
   - 自动获得 `xxx.netlify.app` 域名

2. **或通过Git部署**
   - 连接GitHub仓库
   - 自动构建和部署

### 方式四：传统服务器（VPS/云服务器）

#### 使用Nginx

1. **安装Nginx**
   ```bash
   # Ubuntu/Debian
   sudo apt update
   sudo apt install nginx

   # CentOS/RHEL
   sudo yum install nginx
   ```

2. **配置Nginx**
   ```bash
   sudo nano /etc/nginx/sites-available/default
   ```

   添加配置：
   ```nginx
   server {
       listen 80;
       server_name 你的域名.com;  # 或服务器IP

       root /var/www/demo-flow;
       index index.html;

       location / {
           try_files $uri $uri/ =404;
       }

       # 支持HTML5路由
       location / {
           try_files $uri $uri/ /index.html;
       }

       # 静态资源缓存
       location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
           expires 1y;
           add_header Cache-Control "public, immutable";
       }
   }
   ```

3. **上传文件**
   ```bash
   sudo mkdir -p /var/www/demo-flow
   sudo chown -R $USER:$USER /var/www/demo-flow
   # 使用scp或FTP上传所有文件到 /var/www/demo-flow
   ```

4. **启动Nginx**
   ```bash
   sudo nginx -t  # 测试配置
   sudo systemctl restart nginx
   sudo systemctl enable nginx
   ```

#### 使用Apache

1. **安装Apache**
   ```bash
   # Ubuntu/Debian
   sudo apt install apache2

   # CentOS/RHEL
   sudo yum install httpd
   ```

2. **配置虚拟主机**
   ```bash
   sudo nano /etc/apache2/sites-available/demo-flow.conf
   ```

   添加配置：
   ```apache
   <VirtualHost *:80>
       ServerName 你的域名.com
       DocumentRoot /var/www/demo-flow

       <Directory /var/www/demo-flow>
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>
   </VirtualHost>
   ```

3. **启用站点**
   ```bash
   sudo a2ensite demo-flow.conf
   sudo systemctl restart apache2
   ```

### 方式五：使用Docker

1. **创建Dockerfile**
   ```dockerfile
   FROM nginx:alpine
   COPY . /usr/share/nginx/html
   EXPOSE 80
   CMD ["nginx", "-g", "daemon off;"]
   ```

2. **构建和运行**
   ```bash
   docker build -t demo-flow .
   docker run -d -p 80:80 demo-flow
   ```

## 🔒 HTTPS配置（推荐）

### 使用Let's Encrypt免费SSL证书

1. **安装Certbot**
   ```bash
   sudo apt install certbot python3-certbot-nginx
   # 或
   sudo apt install certbot python3-certbot-apache
   ```

2. **获取证书**
   ```bash
   # Nginx
   sudo certbot --nginx -d 你的域名.com

   # Apache
   sudo certbot --apache -d 你的域名.com
   ```

3. **自动续期**
   Certbot会自动配置自动续期，证书每90天自动更新

## 📝 部署前检查清单

- [ ] 所有HTML文件都在根目录
- [ ] 检查所有文件路径是否正确（相对路径）
- [ ] 测试所有游戏链接是否正常
- [ ] 检查浏览器控制台是否有错误
- [ ] 测试移动端访问是否正常

## 🌐 域名配置（可选）

1. **购买域名**
   - 阿里云、腾讯云、GoDaddy等

2. **DNS配置**
   - 添加A记录指向服务器IP
   - 或添加CNAME记录指向托管服务域名

3. **等待DNS生效**
   - 通常几分钟到几小时

## 🐛 常见问题

### 1. 页面404错误
- 检查文件路径是否正确
- 确保index.html在根目录
- 检查服务器配置是否正确

### 2. 游戏无法加载
- 检查浏览器控制台错误
- 确认所有HTML文件都已上传
- 检查文件权限（Linux服务器）

### 3. 移动端显示异常
- 检查viewport meta标签
- 测试响应式布局
- 检查CSS媒体查询

### 4. 静态资源加载失败
- 检查文件路径（使用相对路径）
- 确认文件已上传
- 检查服务器MIME类型配置

## 📱 移动端优化建议

项目已包含移动端适配，但可以进一步优化：

1. **添加PWA支持**（可选）
   - 创建manifest.json
   - 添加service worker
   - 支持离线访问

2. **性能优化**
   - 压缩CSS和JavaScript
   - 优化图片大小
   - 启用Gzip压缩

## 🔧 服务器性能优化

### Nginx优化配置示例

```nginx
# Gzip压缩
gzip on;
gzip_vary on;
gzip_min_length 1024;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

# 缓存配置
location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```

## 📊 监控和分析（可选）

1. **Google Analytics**
   - 添加GA跟踪代码到index.html

2. **服务器监控**
   - 使用UptimeRobot监控服务可用性
   - 配置告警通知

## 🎯 快速部署命令总结

### GitHub Pages
```bash
git init
git add .
git commit -m "Deploy"
git remote add origin https://github.com/用户名/仓库名.git
git push -u origin main
# 然后在GitHub设置中启用Pages
```

### Vercel
```bash
npm install -g vercel
vercel
```

### Netlify
- 直接拖拽文件夹到 https://app.netlify.com/drop

## 📞 需要帮助？

如果遇到问题，请检查：
1. 浏览器控制台错误信息
2. 服务器日志
3. 文件权限设置
4. DNS配置是否正确

---

**推荐部署方式：**
- 个人项目：GitHub Pages（免费、简单）
- 商业项目：Vercel/Netlify（免费、CDN加速）
- 企业项目：自建服务器（完全控制）

