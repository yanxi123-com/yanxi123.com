---
title: 使用 Hugo 搭建个人小站
slug: hugo-wowchemy
summary: 虽然从小不喜欢写东西，但从接触互联网开始，就希望在互联网上留下自己的痕迹。上大学时就做个人网站，毕业后偶尔写写博客，微信兴起后注册了公众号。通过开源的静态网站生成项目 Hugo，以及 WowChemy 主题，用无代码的方式快速搭建个人小站。
date: '2023-10-29T00:00:00Z'
draft: false
authors:
  - admin
tags:
  - Hugo
  - Wowchemy
categories:
  - 技术
---
## 为什么搭个人小站

虽然从小不喜欢写东西，但从接触互联网开始，就希望在互联网上留下自己的痕迹。上大学时就做个人网站，毕业后偶尔写写博客，微信兴起后注册了公众号。独立域名的博客先有 **yanxi.com**，有人看上这个域名，于是卖掉了。然后注册了新的 **yanxi.me**，又因为不小心到期未续费被别人抢注。

从此总感觉少了点什么，前几天忍不住又注册了新域名 **yanxi123.com**，准备重新把个人小站搭起来。

个人博客类网站技术上不复杂，本质上是一个内容管理系统：

* 功能上包含文章发布、分类、Tag、搜索
* 用户体验上需要美观，并适配PC和移动端

为了只花短时间就把网站搭起来，我希望使用一个现成系统，来快速把网站搭起来，并且具有较强的定制型和扩展性强。

## 技术选型

### Git vs 数据库

传统的 CMS 将文章存放在数据库中，随着 Git、Github 的流行近年来越来越多的人将内容存放在 git 仓库中。对比两种存储模式：

- 基于 Git 存储的优点
	- 原生支持版本控制
	- 可以在本地离线状态下写作，速度更快
	- 托管服务免费的选择较多，基本没有免费的且可长期使用的数据库

- 基于数据库存储的优点
	- 适用于内容非常多的大型网站
	- 适用于对 Git, Markdown 等不熟悉的非技术人员

由于平时开发和写文档习惯了 Git 和 Markdown，加上版本控制和成本的优势，所以选择使用 Git 来存储文章内容。
### 选择渲染类型

用户能在浏览器中看到网页，是因为浏览器完成了页面内容的渲染。从页面内容的生成方式区分，可以将网页渲染分为下面几类：

1. **SSR** **服务端渲染** - Server Side Render
2. **CSR** **客户端渲染** - Client Side Render
3. **SSG** **静态站点生成** - Static Side Generation
4. **ISR** **增量静态生成** - Incremental Static Regeneration

服务端渲染（SSR）是历史最悠久的渲染方式，服务端动态读取数据库获取内容，将其生成完整的 HTML 返回给浏览器，从而完成渲染。优点是打开速度快，对搜索引擎友好（有利于SEO）；缺点是需要额外的服务器和数据库资源。

客户端渲染（CSR）起源于前后端分离，是单页面应用所使用的渲染方式。通过在客户端使用 JavaScript 调用接口获取数据，并完成内容的渲染。优点是前后端开发者分离，缺点是打开速度较慢，对搜索引擎不友好。

静态站点生成（SSG）是指在站点发布前，在构建过程中已生成了所有的页面。优点是打开速度快，对搜索引擎友好，无需动态服务器；缺点是当内容较多时，构建过程相对较慢。

增量静态生成（ISR）是 SSG 的增强版，适用于网页内容更改频繁的场景，会动态更新页面内容，无需每次修改都重新构建站点再发布。它具有 SSG 的优点，缺点是需要额外的服务器和数据库资源。

对比以上四种渲染方式的优缺点：
* SSR 和 ISR 需要额外的服务器资源，从维护成本的角度上排除掉
* CSR 打开速度慢，且对搜索引擎不友好，也可以排除掉
* SSG 虽然有构建慢的缺点，但由于个人站点内容较少，更新不频繁，影响不大

下一步就是选择 **SSG（静态站点生成）** 的具体方案了。

### 选择 SSG 开源方案

[支持 SSG 的开源软件](https://jamstack.org/generators/)很多，按照目前（2023年10月底）的 Github 星级排序 Top 10 如下：

|项目|GitHub星|语言|特点|
|---|---|---|---|
|[Next.js](https://nextjs.org/)|[114k](https://github.com/vercel/next.js)|JS|全能|
|[Hugo](https://gohugo.io/)|[69.5k](https://github.com/gohugoio/hugo)|Go|静态站|
|[Gatsby](http://gatsbyjs.org/)|[54.8k](https://github.com/gatsbyjs/gatsby)|JS|静态站|
|[Docusaurus](https://docusaurus.io/)|[48.8k](https://github.com/facebook/docusaurus)|JS|文档类|
|[Nuxt](https://nuxt.com/)|[48.1k](https://github.com/nuxt/nuxt)|JS|全能|
|[Jekyll](https://jekyllrb.com/)|[47.4k](https://github.com/jekyll/jekyll)|Ruby|博客类|
|[Hexo](https://hexo.io/)|[37.6k](https://github.com/hexojs/hexo)|JS|博客类|
|[Astro](https://astro.build/)|[36.2k](https://github.com/withastro/astro)|JS|全能型|
|[Slate](https://slatedocs.github.io/slate/)|[35.5k](https://github.com/slatedocs/slate)|Ruby|文档类|
|[Gitbook](https://www.gitbook.com/)|[25.9k](https://github.com/GitbookIO/gitbook)|JS|文档类

* 其中 Next.js、Nuxt、Astro，支持服务端逻辑和服务端渲染，需要动态服务器的支持
* 其他都是以 SSG 为主：
	* Hugo、Gatsby，是专业的静态网站生成器
	* Jekyll、Hexo，比较适用于博客类
	* Docusaurus、Slate、Gitbook 主要用于文档类静态站

综合以上，先排除需要服务端支持的。其他的都有很高的人气，且使用广泛。对于我的个人小站来说，其实选择哪个都没问题。

最终从 Github 星标数量和构建速度考虑，选择了使用 Go 语言编写的 Hugo 项目。
### 选择主题

下一步就是找网站主题了，直接在 Hugo 官方[推荐的主题](https://themes.gohugo.io/)里选择。从功能性、美观度、Github星级几个方面对比，最终选择了 [Wowchemy主题](https://themes.gohugo.io/themes/wowchemy/)，接下来就是根据它的文档来搭建和定制自己的小站了。

### 环境搭建

需要安装 go 语言环境、Hugo extended 版本，并根据 [Wowchemy 模板](https://github.com/wowchemy/hugo-blog-theme)创建自己的网站。

通过 `hugo serve` 即可在一秒内本地把站点跑起来，通过 `hugo` 即可完成在一秒内生成完整的静态站点。对于习惯了以 npm、nodejs、webpack 为核心来做前端构建的我来说，绝对是神速。

### 定制化 Wowchemy 模板

把配置过程的主要内容记录如下，如果你也以此模板开始，可以作参考：

#### 1. 基本信息定制

（1）修改 `/config/_default/config.yaml`，可配置`title`，`baseURL`。并配置默认使用中文，如果想修改帖子的 URL 格式，可以在`premalinks` 定义。通过`cascade`来配置在文章页显示相关文章，上一篇和下一篇，以及不显示面包屑导航 。关键配置如下：

  ```yaml
  defaultContentLanguage: zh
  hasCJKLanguage: true

  permalinks:
    post: '/post/:year/:month/:slug/'

  cascade:
    show_related: true
    pager: true
    show_breadcrumb: false
  ```

（2）修改 `/config/_default/languages.yaml`，将默认语言改成中文
  ```yaml
  # Default language
  zh:
    languageCode: zh
  ```

（3）修改 `/config/_default/menus.yaml`，来自定义菜单

（4）修改 `/config/_default/params.yaml`，可配置 SEO 相关信息，底部版权信息，以及日期格式方式，示例如下：
  ```yaml
  locale:
    date_format: '2006-01-02'
  ```

（5）修改 `/content/authors/admin/_index.md` 和 `/content/authors/admin/avatar.jpg` 来更新作者信息。
#### 2. 首页定制

通过修改`/content/_index.md`来定制首页，其中 `sections` 由多个 `block`组成，不需要的 block 直接删除即可，需要的可以自行修改参数。Wowchemy 还支持创建自定义的 block，这部分我没有尝试，需要的可以参考[官网](https://university.wowchemy.com/getting-started/page-builder/)。

#### 3. 发布文章
只要在 `/content/post`目录类的`.md`格式文件，都会自动生成对应的博客文章。目录里的结构没有要求，可以自行决定。由于在第一步中设置了统一的帖子URL规则`/post/:year/:month/:slug/`，所以文章的目录结构和最终的URL没有关系。Markdown 文件头部是前言（Front Matter）部分，首位以`---`分隔，后面是正文。下面是帖子的示例：

```markdown
---
title: 使用 Hugo 搭建个人小站
slug: hugo-build-yanxi123-com
summary: 这里是文章的摘要，会在列表页显示。
date: '2023-10-29T00:00:00Z'
draft: false
authors:
  - admin
tags:
  - Hugo
  - Wowchemy
categories:
  - 技术
---
文章的正文从这里开始...
```
#### 4. 对主题做扩展

（1）使用自定义文件覆盖默认文件：比如我希望用自定的站点 footer，这时候可以复制 [site_footer.html](https://github.com/wowchemy/wowchemy-hugo-themes/tree/41d716f8ed23d85e02a66a3cb057138a9f1c75f3/modules/wowchemy/layouts/partials/site_footer.html) 的原始内容到本地的 `/layouts/partials/site_footer.html`路径，然后修改此文件即可。

（2）使用钩子来添加自定义内容：比如我想在站点底部加上自定义的 JS，可以创建`layouts/partials/hooks/body-end/custom.html`文件，这里的内容会放在所有页面的 `</body>`前面。
#### 5. 样式、图标和 Logo 定制

（1）创建 `/assets/scss/custom.scss` 文件，在这里写自定义的样式即可，可以覆盖主题的默认样式。

（2）图标是为浏览器或者操作系统提供的，比如浏览器标题栏左侧的小图标，不会直接显示在网页上，替换 `/assets/media/icon.png` 图标即可。推荐放一个 512x512尺寸的图标，hugo 会自动为你裁剪成多个尺寸，来满足不同场景的需要。

（3）Logo 则用于显示在网页左上角，默认网页不显示图标，如果希望显示图标，将其放到 `/assets/media/logo.png` 位置即可。
## 网站上线

定制完程序，随手将之前博客网站里的的几篇文章迁移了过来。因为之前也是 markdown 格式，基本复制过来就搞定，更前面的就懒得去找了。

由于 Hugo 生成的网站是纯静态的，因此可以放到任何支持静态内容的地方，可以自己搭建静态服务器，或者使用免费 Github Pages 空间。

为了在国内访问更加快捷，我使用了腾讯云[对象存储COS](https://cloud.tencent.com/product/cos)来保存静态站点，再使用其CDN产品来做加速。

至此，新的个人网站终于和大家见面了，欢迎访问 [https://yanxi123.com/](https://yanxi123.com/)

