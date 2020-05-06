---
categories: 折腾
comments: true
date: "2015-11-02T00:00:00Z"
tags:
- Google
- iOS
- 备忘
- 折腾
title: 开启 Google Photos 的人脸识别分组功能
---

*吐槽：* Google 的人脸识别技术我最开始是在 [Picasa][3] 上面领教到的。简直太强大了，爱死这个功能。虽然现在感觉 Picasa 基本被 Google 战略性抛弃了，大版本号停留在 3.9 已经快 4 年了，连它的[官方博客][1]自 2011 年 12 月 8 日发布 3.9 版本后都没有更新过了= =，就只剩[屈指可数的几个人][2]还在维护着，但是我依然觉得它是 PC 上最强大的照片管理软件。（Google 收购一个很赞的项目然后继续把它做到更好，比同类都好，然后再抛弃不再开发。好像这种例子真不少，Google，这种行为难道不是变相的作恶吗？？！！！说好的不作恶呢）

---

Google Photos 只在美国提供人脸分组的功能。使用其他地区的 IP 地址打开 Google Photos 则根本看不到关于面部识别分组的选项。

那么人不在美国但是还是想用这个功能呢？还是有办法。

网络上的搜索结果很多，大部分都雷同，而且大部分都是只提到了 Andriod 上的操作方法。那 iOS 呢？

实践起来还是折磨了我很久。最终，还是搞定了。但是我没有花时间测试需要的最少条件。

---

## 原理

使用 VPN 让 Google Photos 以为你在美国，你就可以看到开启人脸识别的选项。这一次开启之后，即使之后你的 IP 不在美国，这个设置依然生效。

---

## 简要的步骤

1. 登出手机上所有 Google 出品的 App 里的 Google 帐户。（比如我先登出了 Google Photos，手机上还有 Google Maps 也要登出。）
2. 删除 Google Photos 应用。
3. 重新安装 Google Photos。（中国区的完全可以）
4. 开启 VPN。（这一步是最关键的地方，我主要是被坑在这一步，并不是所有的 VPN 都能成功，后面详说）
5. 打开 Google Photos，登陆，设置，就可以看到“将相似的面孔归为一组”了。如下图：

![](/assets/images/2015/11/02/setting.png)

过一会儿就会看到：

![](/assets/images/2015/11/02/people.png)

---

## 我走的那些弯路

- **VPN**: 这个是最最关键的！使用 **TunnelBear**可以保证成功，App Store 里直接搜就有。连接到美国。我自己搭的 VPN、Shadowsocks 都没成功，明明是洛杉矶的 VPS，搞不懂。还试过 iqlink 也没用。其他的 VPN 没试过。
- **飞行模式**：最后证明完全没必要。（还以为跟 Apple News 一样封地区呢~我想多了）
- 更改**语言**、**国家和地区**：最后也证明不需要。说白了，Google Photos 只认 IP。
- 美区的 Google Photos：**没必要**。最开始在中区下的 Google Photos， 用自己的 VPN，人脸识别出不来。还以为中区是阉割版，最后发现想多了，其实就是 VPN 的问题。

---

## References
1. [StackExchange: Google Photos Faces filter does not appear](http://webapps.stackexchange.com/questions/78621/google-photos-faces-filter-does-not-appear)
2. [HowTo: Enable face recognition in the new Google Photos][4]
3. 上文的**评论**也提供了非常有用的信息：

>**VentraIP Australia:**
>From my understanding with iOS you need to physically log out of all your Google accounts BEFORE deleting Photos, reinstall, activation VPN (eg: Tunnelbear) and then reinitialise Photos and login again.
>Apparently it doesn't work unless you log out of all your Google accounts first (since Google does the shared logins on all iOS apps).

4. [不认识的网友 Macadamianuts][5]在我的[吐槽微博][6]下的热心回复：

> 卸载app， 挂梯子， 手机设置里地区和语言都调成美国，安装app，在设置中开启人脸识别，再把语言和地区调回来。

（实际上语言和地区没有影响）

[1]: http://googlephotos.blogspot.com/
[2]: https://sites.google.com/site/picasaresources/top-contributors
[3]: http://picasa.google.com/
[4]: http://ausdroid.net/howto/howto-enable-face-recognition-in-the-new-google-photos/
[5]: http://weibo.com/u/5631999767
[6]: http://weibo.com/1772939994/D14JLbtuC?from=page_1005051772939994_profile&wvr=6&mod=weibotime&type=comment
