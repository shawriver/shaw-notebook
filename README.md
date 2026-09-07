# 我的笔记本

基于 [Fuwari](https://github.com/saicaca/fuwari) 主题的个人笔记站，Astro 构建，部署在 Cloudflare Pages。

## 日常操作

```bash
pnpm dev          # 本地预览，改文件自动刷新
pnpm new-post 目录/文件名   # 新建一篇笔记
pnpm build        # 生产构建（会顺带生成搜索索引）
```

写笔记的具体格式看站内文章《怎么用这个笔记本》。

## 部署到 Cloudflare Pages

1. 把这个仓库推到 GitHub
2. Cloudflare Dashboard → Workers & Pages → Create → Pages → 连接 GitHub 仓库
3. 构建设置填：

   | 项目 | 值 |
   |---|---|
   | 框架预设 | Astro |
   | 构建命令 | `pnpm build` |
   | 输出目录 | `dist` |
   | Node 版本 | 环境变量加 `NODE_VERSION` = `22` |

4. 首次部署完成后，把 `astro.config.mjs` 里的 `site` 改成 Cloudflare 给的实际域名，再推一次

之后每次 `git push`，Cloudflare 会自动重新构建。

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
