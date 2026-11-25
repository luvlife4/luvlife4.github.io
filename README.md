# 我的技术博客（Hugo + PaperMod + GitHub Pages）

整个博客完全免费，不需要服务器。写好文章后 `git push`，GitHub 会自动构建并发布。

---

## 一、第一次上线（大约 10 分钟）

### 1. 在 GitHub 新建仓库

- 仓库名填 **`你的用户名.github.io`**（比如用户名是 `zhangsan`，就填 `zhangsan.github.io`）
- 选 **Public**，其余选项都不用勾

> 用这个名字，博客地址就是 `https://你的用户名.github.io/`。
> 用别的仓库名也可以，那样地址会是 `https://你的用户名.github.io/仓库名/`。

### 2. 推送代码（把 PaperMod 主题也加进来）

解压后，在本目录里打开终端，依次执行：

```bash
git init -b main
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git add .
git commit -m "初始化博客"
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
git push -u origin main
```

### 3. 打开 GitHub Pages

仓库页面 → **Settings** → 左侧 **Pages** → **Source** 选 **GitHub Actions**。

### 4. 等待部署

点仓库顶部的 **Actions**，能看到「部署博客到 GitHub Pages」正在运行，一两分钟后变成绿色对勾 ✅ 就上线了。

> 如果第 2 步推送时还没打开 Pages，第一次运行可能会失败。没关系：在 Actions 页面点左侧的这个工作流，再点右边的 **Run workflow** 重新跑一次就好。

打开 `https://你的用户名.github.io/` 就能看到博客了。

### 5. 改成你自己的信息

打开 `hugo.toml`，把标了「改这里」的几项改掉（博客名、简介、名字、GitHub 链接）；再改一下 `content/about.md`。改完 `git push` 即可。

---

## 二、日常写文章

```bash
hugo new content posts/redis-cache-notes.md
```

会生成 `content/posts/redis-cache-notes.md`，打开后：

1. 改 `title`（可以写中文）
2. 把 `draft: true` 改成 `draft: false`（`true` 是草稿，不会发布）
3. 在下面用 Markdown 写正文

写完：

```bash
git add .
git commit -m "新文章：Redis 缓存笔记"
git push
```

一两分钟后线上就更新了。

> 不想装 Hugo 的话，直接复制一份 `content/posts/hello-world.md` 改内容也完全可以，甚至可以在 GitHub 网页上直接新建文件。

### 插入图片

把图片放进 `static/images/`，文章里写：`![说明](/images/xxx.png)`

---

## 三、在本地预览（可选，推荐）

安装 Hugo（装 extended 版本）：

- **Windows**：`winget install Hugo.Hugo.Extended`
- **macOS**：`brew install hugo`
- **Linux**：参考 https://gohugo.io/installation/linux/

然后在博客目录运行：

```bash
hugo server -D
```

浏览器打开 http://localhost:1313 ，改文件后页面会自动刷新。`-D` 表示草稿也显示。

> 如果你是用 `git clone` 把仓库拉到另一台电脑上，记得加 `--recurse-submodules`，否则主题文件夹是空的：
> `git clone --recurse-submodules https://github.com/你的用户名/你的用户名.github.io.git`

---

## 四、绑定自己的域名（可选）

1. 仓库 **Settings → Pages → Custom domain**，填你的域名（如 `blog.example.com`），保存
2. 到域名服务商添加一条 DNS 记录：类型 **CNAME**，主机记录 `blog`，值 `你的用户名.github.io`
3. 等 DNS 生效后，在同一页面勾上 **Enforce HTTPS**

---

## 五、目录说明

```
hugo.toml                  博客配置（标题、菜单、主题参数）
content/posts/             文章都放这里
content/about.md           「关于」页面
content/archives.md        「归档」页面（不用改）
content/search.md          「搜索」页面（不用改）
static/                    图片等静态文件
archetypes/default.md      新建文章时使用的模板
themes/PaperMod/           主题（git submodule，不要直接改）
.github/workflows/hugo.yml 自动部署流程
```

## 常见问题

- **页面样式全乱了 / 没有样式**：通常是主题没加进来，检查 `themes/PaperMod` 里有没有文件，没有就重新执行第 2 步里的 `git submodule add` 命令。
- **新文章没显示**：检查是不是还是 `draft: true`，或者 `date` 写成了未来的时间（Hugo 默认不发布未来日期的文章）。
- **国内访问慢**：可以把同一个仓库导入 Cloudflare Pages（免费，构建命令填 `hugo --gc --minify`，输出目录填 `public`，环境变量 `HUGO_VERSION` 设为 `0.163.2`）。
- **更新主题**：`git submodule update --remote --merge`，然后提交并推送。
