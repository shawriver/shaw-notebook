---
title: 怎么用这个笔记本
published: 2026-09-06
description: 记录一下我自己怎么往这个网站里加笔记，忘了就回来看这篇。
tags: ["使用说明"]
category: 随手记
draft: false
---

## 加一篇新笔记

在项目目录里执行，`xxx` 换成文件名（用英文，别带空格）：

```bash
pnpm new-post 数据结构/二叉树
```

它会在 `src/content/posts/` 下生成一个 `.md` 文件，开头那一段是文章信息，下面直接写正文。

## 开头那一段怎么填

```yaml
---
title: 完全二叉树          # 标题，写中文没问题
published: 2026-09-06     # 日期
description: 一句话说明   # 列表页会显示这句
tags: ["数据结构"]        # 标签，可以多个
category: 数据结构        # 分类，只能一个
draft: false              # 改成 true 就是草稿，网站上看不见
---
```

## 正文只要记住这几个

```md
## 二级标题
### 三级标题

**加粗**

- 列表项
- 列表项

1. 有序列表
2. 有序列表

`行内代码`

[链接文字](https://example.com)
```

代码块用三个反引号包住，后面写语言名：

```c
int main(void) {
    return 0;
}
```

## 本地看效果

```bash
pnpm dev
```

然后浏览器打开终端里给出的地址，改完文件保存，页面会自动刷新。

## 发布出去

```bash
git add .
git commit -m "新增笔记"
git push
```

推上去之后 Cloudflare Pages 会自动重新构建，一两分钟后网站就更新了。
