---
title: 使用Hexo写博客
date: 2021-01-20 14:50:41
tags:
---
尽管 Hexo 支持 MarkDown，但是我们却不能像写单独的 MarkDown 文档时那样肆无忌惮。由于我们所写的文档是需要被解析为静态网页文件的，所以我们必须严格遵从 Hexo 的规范，这样才能解析出条理清晰的静态网页文件。

### 新建文档
假设我们的文章名为 “hello hexo markdwon”，在命令行键入以下命令即可：
```
$ hexo new "hello hexo markdown"
```
上述命令的结果是在 ./hexo/source/_posts 路径下新建了一个 hello-hexo-markdown.md 文件。

然后，我们就可以打开编辑器尽情地写作了。

### 文章分类
`categories` 是用来给文章分类的，它跟 `tags` 不同的是其具有顺序性和层次性。

例如，我们写一篇关于 CSS3 动画的文章，我们可能会为其打标签 ”CSS3“、”动画“等，但是我们却会将其分在 CSS/CSS3 类别下，这个是有一定的相关性、顺序性和层次性。简单来说，`categories` 有点儿像新建文件夹对文档进行分门别类的归置。

`categories` 的用法同 `tags` 一样，只不过斗个 `categories` 值是分先后顺序的。

### 生成文件
### 清除缓存文件
为了避免不必要的错误，在生成静态文件前，强烈建议先运行以下命令：
`
$ hexo clean
`
上述命令会清除本地站点文件夹下的缓存文件（`db.json`）和已有的静态文件（`public`）。

### 生成静态文件
写好 MarkDown 文档之后，我们就可使用以下命令生成静态文件：
```
$ hexo generate
$ hexo server
```
然后我们就可以启动 Hexo 服务器，使用浏览器打开 http://localhost:4000 查看效果了。