# Lavino 官网 · 发布仓库

青岛朗维诺国际贸易有限公司官网（https://www.lavinoequipment.com）的**发布仓库**。

## 这个仓库是什么

它只放**已经构建好、可以直接上线的网站文件**——页面、样式、脚本、图片。
Vercel 直接把这些文件发布到全球边缘网络，**不需要在这里做任何构建**。

```
index.html  about.html  products.html  news.html  contact.html  privacy.html  404.html
css/  js/  assets/  news/            ← 网站本体
robots.txt  sitemap.xml  llms.txt    ← 搜索引擎与 AI 助手用的说明文件
vercel.json                          ← 缓存策略与安全响应头
```

## 内容从哪里来（重要）

**不要直接在这个目录里改文件。** 每次同步都会把这里的内容覆盖成最新的。

真正的源文件在隔壁的开发目录：

```
D:\外贸SOHO工作台\05_独立站开发与运营\lavino-website\
```

日常改内容**走管理台**（双击桌面「独立站发新闻」，或在浏览器打开
`http://127.0.0.1:8787/admin`）——新闻、产品、公司介绍、页面文案、
图片都能在里面改，保存后自动重建。

改完之后，把最新内容同步到这里并推送上线：

```
cd D:\外贸SOHO工作台\05_独立站开发与运营\lavino-website
python scripts/sync_deploy.py     # 重建 dist/ 并同步到本目录
cd ..\lavino-deploy
git add -A
git commit -m "更新网站内容"
git push                          # Vercel 会自动收到并发布
```

推送后大约 1 分钟，线上就是最新版本。

## 为什么单独一个仓库

开发目录里还放着**管理台密码、登录会话凭证、第三方接口密钥**。
那些文件绝不能进 Git 仓库（进了就等于公开到互联网上）。
所以发布走这个独立目录，同步时按白名单逐项复制，开发目录里的东西一律不会被带过来。

同步脚本结束前会做一次体检：如果这里出现了任何凭证、源码或内部文档，会立刻报错。

## 域名与加速

- 网站托管：**Vercel**（全球边缘网络，自动 HTTPS）
- DNS 与 CDN：**Cloudflare**（域名解析 + 缓存 + 防护）
- 域名：`lavinoequipment.com` / `www.lavinoequipment.com`

解析记录与上线步骤见开发目录里的
`docs/deploy-guide.html`（图文版：怎么配置、怎么验证、出问题怎么回滚）。

## 回滚

任何一次历史版本都能在 Vercel 控制台的 Deployments 里一键回滚，
不需要改代码，也不会丢数据。
