---
title: "第一篇文章：博客搭建完成"
date: 2026-11-24T10:00:00+08:00
draft: false
tags: ["Hugo", "博客"]
categories: ["随笔"]
summary: "用 Hugo + GitHub Pages 搭了个博客，顺便演示一下常用的 Markdown 写法。"
---

博客搭好了！这篇文章顺便演示一下写技术博客时常用的格式，写新文章时可以直接参考。

## 代码块

代码块右上角有复制按钮，会根据语言自动高亮：

```python
def fib(n: int) -> int:
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

print(fib(10))  # 55
```

```bash
hugo new content posts/my-new-post.md
hugo server -D
```

行内代码这样写：`git push origin main`。

## 表格

| 命令 | 作用 |
|------|------|
| `hugo server -D` | 本地预览（包括草稿） |
| `hugo new content posts/xxx.md` | 新建文章 |
| `git push` | 发布到线上 |

## 引用和列表

> 好记性不如烂笔头。

- 写下踩过的坑
- 记录读过的源码
- 整理项目经验

## 图片

把图片放到 `static/images/` 目录下，然后这样引用：

```markdown
![图片说明](/images/example.png)
```
