---
title: "使用 Ruby + DevKit 搭建 Chirpy 博客"
description: "本文记录在 Windows 环境下，通过 RubyInstaller-DevKit + Chirpy 主题搭建 GitHub Pages 博客的完整流程"
date: 2026-06-15 20:00:00 +0800
categories: [博客搭建]
tags: [jekyll, chirpy]
---

## 一、创建博客仓库

1. 打开 Chirpy Starter 模板  
   https://github.com/cotes2020/chirpy-starter
2. 点击 **Use this template → Create a new repository**
3. 仓库名必须为：`username.github.io`
4. Clone 到本地：
```powershell
git clone https://github.com/username/username.github.io.git
cd username.github.io
```

---

## 二、安装 Ruby + DevKit（必须）

Chirpy 依赖部分需要编译的 Ruby 扩展，**Windows 必须使用 DevKit 版本**。

### 1️⃣ 下载
https://rubyinstaller.org/downloads/

选择 **Ruby+DevKit x64**，例如：
```
rubyinstaller-devkit-3.2.x-x64.exe
```

### 2️⃣ 安装
- ✅ 勾选 **Add Ruby to PATH**
- 一路 Next 直至完成
- 安装结束会弹出 **MSYS2 安装窗口**
  - 输入 `1` 或 `3` 回车
  - 等待安装完成
- **关闭并重新打开终端**

### 3️⃣ 验证
```powershell
ruby -v
gem -v
```

---

## 三、配置国内镜像（推荐）

国内访问 RubyGems 较慢，建议更换镜像：

```powershell
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
gem sources -l
```

确认输出中包含 `https://gems.ruby-china.com/`。

---

## 四、安装 Chirpy 依赖

Chirpy Starter 已通过 `Gemfile` 锁定依赖版本，**无需手动安装 Jekyll**。

```powershell
bundle install
```

若提示缺少 `bundler`，可执行：
```powershell
gem install bundler
bundle install
```

---

## 五、基础配置

编辑 `_config.yml`：

```yaml
title: 你的博客名称
tagline: 一句话简介
description: 技术博客与学习记录
url: "https://用户名.github.io"
lang: zh-CN
timezone: Asia/Shanghai

avatar: /assets/img/avatar.png

social:
  name: 你的名字
  email: you@example.com
  links:
    - https://github.com/用户名
```

---

## 六、本地预览

```powershell
bundle exec jekyll serve
```

浏览器访问：
```
http://127.0.0.1:4000
```

---

## 七、第一篇文章

📄 `_posts/2026-06-15-hello-chirpy.md`

```markdown
---
title: "Hello Chirpy"
date: 2026-06-15 20:00:00 +0800
categories: [Blog]
tags: [起步, chirpy]
---

这是使用 **Chirpy 主题** 搭建的第一篇博客 ✅

- 支持目录（TOC）
- 支持标签与分类
- 支持深色模式
- 支持本地预览与 GitHub Pages 自动部署
```

提交并发布：
```powershell
git add .
git commit -m "first post"
git push
```
稍等片刻，访问：
```
https://用户名.github.io
```
---

## 八、常见问题

- **MSYS2 未安装？**  
  手动执行：`ridk install`
- **bundle install 失败？**  
  确认 DevKit 安装成功，并重开终端
- **GitHub Pages 未生效？**  
  仓库 Settings → Pages → Source 选择 **GitHub Actions**