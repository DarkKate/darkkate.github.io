---
categories: 折腾
comments: true
date: "2015-05-13T00:00:00Z"
tags:
- 折腾
title: 我的豆瓣秀
---

### 我最近看过的

<script type="text/javascript" src="http://www.douban.com/service/badge/DarkKate/?selection=latest&amp;picsize=medium&amp;hideself=on&amp;show=collection&amp;n=8&amp;hidelogo=on&amp;cat=drama%7Cmovie%7Cbook%7Cmusic&amp;columns=4"></script>

### 历史随机列表

<script type="text/javascript" src="http://www.douban.com/service/badge/DarkKate/?selection=random&amp;picsize=medium&amp;hideself=on&amp;show=collection&amp;n=8&amp;hidelogo=on&amp;cat=drama%7Cmovie%7Cbook%7Cmusic&amp;columns=4"></script>

*其实只是突然想起来[豆瓣提供了这么一个功能](https://www.douban.com/service/badgemaker)，想在自己的博客里测试一下，以后挂在 About 页面应该比较好。*

实际上就是在页面里放了一段 JavaScript 代码：

#### 我最近看过的

{{< highlight javascript >}}
<script type="text/javascript" src="http://www.douban.com/service/badge/DarkKate/?selection=latest&amp;picsize=medium&amp;hideself=on&amp;show=collection&amp;n=8&amp;hidelogo=on&amp;cat=drama%7Cmovie%7Cbook%7Cmusic&amp;columns=4"></script>
{{< / highlight >}}

#### 历史随机列表

{{< highlight javascript >}}
<script type="text/javascript" src="http://www.douban.com/service/badge/DarkKate/?selection=random&amp;picsize=medium&amp;hideself=on&amp;show=collection&amp;n=8&amp;hidelogo=on&amp;cat=drama%7Cmovie%7Cbook%7Cmusic&amp;columns=4"></script>
{{< / highlight >}}

-----

目前发现了一个很要命的问题：**图片显示不全！**

审查元素后发现一下症状：


1. 文件名以 s 开头的图片（书籍、剧集、专辑）每次都能显示，而以 p 开头的图片（电影）则出现 403 (forbidden) 状态码。

2. 我把这个 js 代码写了一个 html 文件，在本地可以**完美显示**，上传到 GitHub上去之后，就出现了上述问题。

这个文件代码如下：

{{< highlight html >}}
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="zh" lang="zh-cn">

<h2>Random List</h2>

<script type="text/javascript" src="http://www.douban.com/service/badge/DarkKate/?selection=random&amp;picsize=medium&amp;hideself=on&amp;show=collection&amp;n=8&amp;hidelogo=on&amp;cat=drama%7Cmovie%7Cbook%7Cmusic&amp;columns=4"></script>
</html>
{{< / highlight >}}

---

2015-7-5, update:

不知道从什么时候开始，豆瓣秀的图片又都能正常显示了。

难道是我发给豆瓣的邮件的效果？可是他们并没有回复我呀。

2015-9-12, update:

今天发现豆瓣在其网站删去了有关豆瓣收藏秀的页面。另一方面，我上面的js代码依然是能够工作的。
