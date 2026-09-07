# 我的笔记本

基于 [Fuwari](https://github.com/saicaca/fuwari) 主题的个人笔记站，Astro 构建，部署在自己的 VPS 上。

## 日常操作

```bash
pnpm dev          # 本地预览，改文件自动刷新
pnpm new-post 目录/文件名   # 新建一篇笔记
pnpm build        # 生产构建（会顺带生成搜索索引）
```

写笔记的具体格式看站内文章《怎么用这个笔记本》。

## 部署到 VPS

线上站点由 VPS 上的 Caddy 提供服务，GitHub 只作为公开源码仓库和备份，不参与页面托管。

服务器上的发布流程由 `/usr/local/bin/knowledge-publish` 完成：

```bash
cd /srv/knowledge/repo
git pull --ff-only
knowledge-publish
```

上述命令用途：拉取已审核的源码并重新构建静态站点，然后原子替换线上文件。风险：会修改服务器上的站点文件并重新加载发布内容，不会修改防火墙或 DNS。

如果需要在本地预览，使用：

```bash
pnpm install
pnpm build
```

线上地址：<https://me.622168.xyz/>

## 目录

```
src/
├── config.ts               # 站点名称、头像、导航、主题色
├── content/
│   ├── posts/              # 所有笔记放这里
│   │   ├── data-structure/
│   │   ├── embedded/
│   │   └── notes/
│   └── spec/about.md       # 关于页
└── ...
```
