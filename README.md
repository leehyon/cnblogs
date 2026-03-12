# 中文博客聚合器

[rss.kohsruhe.com](https://rss.kohsruhe.com/) 将来自数百个中文博客的文章聚合到单个页面，覆盖最近 7 天的内容，站点每天自动构建。

无需账号、无需算法 —— 只有一个链接列表，并提供快速过滤器以便检索文章。

> 提示：你也可以直接下载 OPML 文件并在你自己的订阅阅读器中使用！

## 提交订阅

知道有好博客缺失吗？请通过 [在 GitHub 上打开 issue](https://github.com/leehyon/cnblogs/issues/new?template=add-feed.yml) 提供博客名称和 RSS 订阅地址，或直接编辑 `cngblogs.opml` 并提交 PR。合并后几分钟内新订阅会出现在站点上。

## 工作原理

一个 Go 脚本会读取 `cngblogs.opml`，并行抓取每个订阅（使用条件 GET 以尽量减少请求），收集最近 7 天的文章并渲染为静态 HTML 页面。GitHub Actions 会定期运行并将结果部署到 GitHub Pages。

此项目不使用数据库。订阅条目是短期的，超出 7 天窗口的文章将不再展示。

## 本地运行

需要 Go 1.22+ 和 Python 3。

```shell
make build    # fetch all feeds and generate public/index.html
make render   # rebuild HTML from cache (no fetching, fast)
make dev      # render and serve at http://localhost:8080
make clean    # remove public/ and cache.json
```

## 许可

订阅列表（`cngblogs.opml`）由社区维护，其余代码采用 MIT 许可。
