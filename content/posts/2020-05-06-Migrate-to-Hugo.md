---
title: "从 Jeykll 迁移到 Hugo"
date: 2020-05-06
Lastmod: 2020-05-08
categories: 折腾
---

终于从 Jekyll 迁移到 Hugo 了。

碰到了不少头疼的小问题，还好有 Google，但即使有 Google，还是走了很多弯路，回头看，还是得仔细读官方文档原文。以下是我碰到的麻烦以及帮我解决问题的链接：



## 1. MD 文件 front matter 的批量转换

参考：[Migrate to Hugo](https://gohugo.io/tools/migrations/#jekyll)

虽然不需要从头造轮子，但是用到的Python脚本也没有那么容易顺利跑，硬着头皮看各种莫名其妙错误代码。

## 2. Markdown 中的 javascript 被忽略

与Jekyll使用的 kramdwon 不同，Hugo 使用的 Markdown 解释器默认会对 HTML、javascript 会直接忽略。这导致我的 instafeed 页面以及文章里的 Google 地图无法显示。

Hugo 目前（0.69.2） 默认的 Markdown 解释器是[Goldmark](https://gohugo.io/getting-started/configuration-markup#goldmark)，之前版本（0.60之前？）默认使用的是 Blackfriday。

Hugo 提出 shortcodes 来解决，文档中有这样的描述：

>Hugo loves Markdown because of its simple content format, but there are times when Markdown falls short. Often, content authors are forced to add raw HTML (e.g., video `<iframes>`) to Markdown content. We think this contradicts the beautiful simplicity of Markdown’s syntax.
>
>Hugo created **shortcodes** to circumvent these limitations.

读了这段话之后的我就开始阅读关于 shortcodes 的文档以及博客。说实话，对于几乎算是零基础的我来说，很多地方读得很费劲。我只是想显示一个特定页面而已，却读了很多如何去搞一个通用的 shortcodes 的说明。

除了官方文档以外，这三篇是对我最有帮助的：

1. [笔记：Hugo 中 Shortcode 的基本使用](https://moxo.io/blog/2018/02/10/shortcode-in-hugo/)
2. [在 Hugo 博客上实践 Shortcodes 短代码, 太强大了](https://matnoble.me/tech/hugo/shortcodes-practice-tutorial-for-hugo/)
3. [在 Hugo 的 Markdown 里直接使用 HTML](https://lvv.me/posts/2019/12/06_raw_html_with_hugo/)

尤其是第二、三篇，完美解决我的痛点。

但是，总有但是。使用第三篇的中方法解决问题之后我又一次读了[Goldmark 相关的段落](https://gohugo.io/getting-started/configuration-markup#goldmark)。

注意到 Goldmark 有一个 unsafe 项：

>**unsafe**
>
>By default, Goldmark does not render raw HTMLs and potentially dangerous links. If you have lots of inline HTML and/or JavaScript, you may need to turn this on.

所以实际上还有一个简单粗暴地解决我需求的方法：在`config.toml`中令`unsafe = true`，即：

```toml
[markup]
    [markup.goldmark.renderer]
      unsafe = true
```
实测有效。

## 3. 作为 Github Pages 发布

[Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

[使用 Hugo + GitHub Pages 搭建个人博客](https://mogeko.me/posts/zh-cn/018/)

## 4. 页面显示不正确

正确push到github仓库之后，打开username.github.io，却发现网页显示不正确。原因是配置文件里的baseURL我是按insideout.top设置的，所以在根目录下还需要一个CNAME文件，里面填上baseURL域名。问题解决。

## 5. disqus 的配置

Diary theme 默认的评论系统是gitalk。但事实上Hugo已经内置支持disqus：

1. 把正确的disqusShortname放在正确的位置。（不应放在`[params]`之下）
2. [给Hugo添加disqus评论服务](https://zh4ui.net/post/2017-04-20-hugo-with-disqus/)
3. [Hugo Doc - Comments](https://gohugo.io/content-management/comments/)

## 6. 与之前 Jekyll 的 Permalinks 格式保持一致

文章迁移过来了，评论也得迁移过来。永久链接的格式保持一致是最便捷的办法。这篇博客非常有帮助：

[jekyll-hexo-hugo 互相迁移时关于永久链接的问题](https://leay.net/2019/09/23/jekyll-hexo-hugo/)
