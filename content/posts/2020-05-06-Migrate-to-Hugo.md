---
title: "从 Jeykll 迁移到 Hugo"
date: 2020-05-06T20:45:39+08:00
categories: 折腾
---

终于从 Jekyll 迁移到 Hugo 了。

碰到了不少头疼的小问题，还好有 Google，但即使有 Google，还是走了很多弯路，回头看，还是得仔细读官方文档原文。以下是我碰到的麻烦以及帮我解决问题的链接：



## 1. MD文件头部的批量转换
参考：[Migrate to Hugo](https://gohugo.io/tools/migrations/#jekyll)

用到的Python脚本没有那么容易顺利跑，硬着头皮看错误代码。

## 2. Markdown 中的 javascript 被忽略

与Jekyll使用的 kramdwon 不同，Hugo 使用的 Markdown 解释器默认会对 HTML、javascript 会直接忽略。这导致我的 instafeed 页面以及文章里的 Google 地图无法显示。

Hugo 目前（0.69.2） 默认的 Markdown 解释器是[Goldmark](https://gohugo.io/getting-started/configuration-markup#goldmark)，之前版本（0.60之前？）默认使用的是 Blackfriday。

Hugo官方文档中也有这样的描述：
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

[使用 Hugo + GitHub Pages 搭建个人博客](https://mogeko.me/2018/018/)

## 4. 页面显示不正确

正确push之后，打开username.github.io，却发现，网页显示不正确，CSS完全没有加载。原因是配置文件里的baseURL我是按insideout.top设置的，所以在根目录下还需要一个CNAME文件，里面填上baseURL域名。问题解决。
