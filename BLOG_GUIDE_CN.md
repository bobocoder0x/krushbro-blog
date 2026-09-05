# Krushbro 博客维护指南

## 地址

- 正式地址：https://krushbro.xyz/（需域名接入和证书签发完成）
- Pages 地址：https://krushbro-blog.pages.dev/
- 仓库：https://github.com/bobocoder0x/krushbro-blog

## 只用浏览器发布文章

1. 在 GitHub 打开 `src/content/blog/`。
2. 点击 **Add file → Create new file**，输入英文文件名，例如 `my-first-note.md`。
3. 写入下面的文章模板，修改标题、日期、简介和正文。
4. 点击 **Commit changes**，提交到 `main`。
5. Cloudflare Pages 会自动构建并部署。等待项目部署页显示成功，再刷新博客。

```markdown
---
title: "文章标题"
pubDatetime: 2026-09-05T12:00:00Z
description: "一句话介绍这篇文章。"
featured: false
draft: false
tags:
  - 学习笔记
---

正文从这里开始。

## 小标题

支持 Markdown 格式。
```

`draft: true` 不会展示在网站上；这个仓库是公开的，草稿仍可在 GitHub 被他人看到。请勿提交密码、密钥或私人资料。`featured: true` 会展示在首页精选。日期使用实际发布时间；未来日期的文章还需要在到期后重新构建才能上线。

## 常用修改位置

- 站名、作者、域名、社交链接：`astro-paper.config.ts`
- 首页介绍：`src/pages/index.astro`
- 关于页面：`src/content/pages/about.md`
- 正式文章：`src/content/blog/`
- 上游模板示例：`src/content/posts/`，已与正式文章集合分离，不在网站发布。

## 部署配置

- Cloudflare Pages 项目：`krushbro-blog`
- 生产分支：`main`
- 构建命令：`pnpm build`
- 输出目录：`dist`
- 构建变量：`NODE_VERSION=24`、`PNPM_VERSION=11.3.0`
- Cloudflare 免费套餐；未开通付费计算、数据库或高级证书服务。域名续费仍由 Dynadot 单独计费。
- Dynadot 名称服务器：`justin.ns.cloudflare.com`、`zelda.ns.cloudflare.com`
- 根域 DNS：`CNAME @ → krushbro-blog.pages.dev`，开启代理。根域还必须在 Pages 自定义域中完成绑定。

## 更新失败时

在 Cloudflare 的 **Workers 和 Pages → krushbro-blog → 部署 → Details** 查看日志。检查 Markdown 的开头是否有两组 `---`、日期格式是否正确、字段是否齐全。构建失败时，之前成功的生产部署继续提供服务。可在 GitHub 修正后重新提交；需要恢复旧版本时，在 Pages 部署历史中选择对应成功部署进行回滚。

## 主题来源

基于 [AstroPaper](https://github.com/satnaing/astro-paper)，保留仓库中的 MIT LICENSE。本站为静态博客，不包含 Halo 后台。
