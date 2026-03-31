# Everland Technology Limited 网站部署指南

## 📁 网站文件结构

```
everland-website/
├── index.html          # 主页（公司简介 + 服务列表）
├── terms.html          # Terms & Conditions（服务条款）
├── privacy.html        # Privacy Policy（隐私政策）
├── refund.html         # Refund Policy（退款政策）
├── contact.html        # Contact Us（联系我们）
└── DEPLOYMENT.md       # 本部署指南
```

## 🚀 部署选项

### 选项 1: Vercel（推荐 - 免费且简单）

#### 步骤 1: 创建 Vercel 账户
1. 访问 https://vercel.com
2. 使用 GitHub/Google 账户登录

#### 步骤 2: 部署网站
```bash
# 安装 Vercel CLI
npm install -g vercel

# 进入网站目录
cd /Users/liwencao/.openclaw/workspace/everland-website

# 部署
vercel
```

#### 步骤 3: 连接自定义域名
1. 在 Vercel Dashboard 中选择你的项目
2. 点击 "Settings" → "Domains"
3. 添加域名：`everlandapps.com`
4. Vercel 会显示需要配置的 DNS 记录

---

### 选项 2: Netlify（免费且简单）

#### 步骤 1: 创建 Netlify 账户
1. 访问 https://netlify.com
2. 使用 GitHub/Google 账户登录

#### 步骤 2: 部署网站
```bash
# 安装 Netlify CLI
npm install -g netlify-cli

# 进入网站目录
cd /Users/liwencao/.openclaw/workspace/everland-website

# 部署
netlify deploy --prod
```

#### 步骤 3: 连接自定义域名
1. 在 Netlify Dashboard 中选择你的站点
2. 点击 "Domain settings"
3. 添加自定义域名：`everlandapps.com`

---

### 选项 3: GitHub Pages（完全免费）

#### 步骤 1: 创建 GitHub 仓库
```bash
cd /Users/liwencao/.openclaw/workspace/everland-website
git init
git add .
git commit -m "Initial commit"
```

#### 步骤 2: 推送到 GitHub
1. 在 GitHub 创建新仓库：`everland-website`
2. 推送代码：
```bash
git remote add origin https://github.com/YOUR_USERNAME/everland-website.git
git branch -M main
git push -u origin main
```

#### 步骤 3: 启用 GitHub Pages
1. 进入仓库 Settings → Pages
2. Source 选择 "main branch"
3. 保存后会获得一个 `yourusername.github.io/everland-website` 的 URL

---

## ☁️ Cloudflare DNS 配置

### 登录 Cloudflare
1. 访问 https://dash.cloudflare.com
2. 选择你的域名：`everlandapps.com`
3. 进入 "DNS" 页面

### 添加 DNS 记录

#### 如果使用 Vercel:
| 类型 | 名称 | 内容 | Proxy |
|------|------|------|-------|
| CNAME | www | cname.vercel-dns.com | DNS Only |
| ALIAS | @ | 76.76.21.21 | DNS Only |

或者使用 Vercel 提供的 Nameservers:
1. 在 Vercel Domain 设置页面获取 Nameservers
2. 在 Cloudflare 的 "Nameservers" 页面更新

#### 如果使用 Netlify:
| 类型 | 名称 | 内容 | Proxy |
|------|------|------|-------|
| CNAME | www | your-site-name.netlify.app | DNS Only |
| ALIAS | @ | 75.2.60.5 | DNS Only |

#### 如果使用 GitHub Pages:
| 类型 | 名称 | 内容 | Proxy |
|------|------|------|-------|
| CNAME | www | yourusername.github.io | DNS Only |
| ALIAS | @ | 185.199.108.153 | DNS Only |
| ALIAS | @ | 185.199.109.153 | DNS Only |
| ALIAS | @ | 185.199.110.153 | DNS Only |
| ALIAS | @ | 185.199.111.153 | DNS Only |

### DNS 配置步骤
1. 在 Cloudflare DNS 页面，点击 "Add record"
2. 选择记录类型（CNAME 或 ALIAS）
3. 输入 Name 和 Content
4. Proxy status 选择 "DNS Only"（灰色云朵）
5. 点击 "Save"

### 等待 DNS 生效
- DNS 变更通常需要 5-30 分钟生效
- 最长可能需要 48 小时全球传播
- 使用 `nslookup everlandapps.com` 检查是否生效

---

## ✅ 验证部署

### 检查网站是否可访问
1. 访问 `https://everlandapps.com`
2. 访问 `https://www.everlandapps.com`
3. 检查所有页面链接是否正常：
   - Terms & Conditions
   - Privacy Policy
   - Refund Policy
   - Contact Us

### 检查 SSL 证书
- Vercel/Netlify/GitHub Pages 都自动提供 HTTPS
- 确保访问时显示安全锁图标

---

## 📧 网站内容确认

网站包含以下必需页面和链接：

### 主页 (index.html)
- ✅ 公司简介
- ✅ 服务列表（App 开发、信息咨询）
- ✅ 页脚链接到所有法律页面

### 法律页面
- ✅ Terms & Conditions (terms.html)
- ✅ Privacy Policy (privacy.html)
- ✅ Refund/Return Policy (refund.html)
- ✅ Contact Us (contact.html)

### 联系信息
- ✅ Email: admin@everlandapps.com
- ✅ Address: UNIT 1022A, BEVERLEY COMM CENTRE, 87-105 CHATHAM RD SOUTH, TSIM SHA TSUI, HONG KONG

---

## 🔧 故障排除

### 网站无法访问
1. 检查 DNS 是否生效：`nslookup everlandapps.com`
2. 清除浏览器缓存
3. 尝试使用 `https://` 访问

### SSL 证书问题
1. 等待 DNS 完全生效
2. 在部署平台重新触发证书颁发
3. 清除浏览器 SSL 缓存

### 页面显示不正确
1. 检查 HTML 文件是否完整上传
2. 清除 CDN 缓存
3. 重新部署网站

---

## 📞 需要帮助？

如果在部署过程中遇到问题：
- Vercel 支持：https://vercel.com/support
- Netlify 支持：https://answers.netlify.com/
- GitHub Pages 文档：https://pages.github.com/
- Cloudflare 支持：https://support.cloudflare.com/

---

**最后更新：** 2026 年 3 月 31 日
**公司名称：** Everland Technology Limited
