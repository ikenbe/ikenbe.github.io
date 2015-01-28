---
layout: default
title: 关于写作环境
---
在电脑上我是选择了 GitHub 的 Windows 客户端 + Sublime Text 3 来编辑和提交修改，不但可以很方便地编辑和预览 Markdown 文件，还可以对其它格式的文件很方便地操作。为了保持热情和更方便地更新文档，我还在手机上安装了 Pocket Git + JotterX 来执行相同的事情。这也有助于我对 Git 的版本管理和分支管理有更直观的理解。

我之前也有在用 Sublime Text， 不过还是又看了这篇 [Sublime Text 全程指南](http://zh.lucida.me/blog/sublime-text-complete-guide/)， GUI 环境下我也同意这是目前综合考虑最好的编辑器了。

## Jekyll 的主要作用：

从 GitHub 的 [dependency versions](https://pages.github.com/versions/) 可以得到默认支持的插件

> + jekyll
> + jekyll-coffeescript
> + jekyll-sass-converter
> + kramdown
> + maruku
> + rdiscount
> + redcarpet
> + RedCloth
> + liquid
> + pygments.rb
> + jemoji
> + jekyll-mentions
> + jekyll-redirect-from
> + jekyll-sitemap
> + github-pages
> + ruby

1. 把 Markdown 等标记语言的文件生成为静态文件。(支持数种转换引擎，在 _confi.yml 进行设置，我设为了 GFM 默认的 redcarpet)
2. 使用 [Liquid](http://liquidmarkup.org/) 把一些动态数据转化为静态页面。
3. 转换 SASS 为标准 CSS
4. 生成站点结构

##如果直接使用 HTML+JS+CSS?

肉身管理静态站点的问题有很多，例如有的东西一旦修改就要一个一个文件全部改一遍。人又不可能把所有东西都做到最好保证以后就永远不需要修改，所以必然很痛苦。更何况世上本来就没有最好这一说。

JS 和 CSS 本来就是要人手写的， CoffeeScript 和 LESS SCSS 之类的据我目前的了解知识能一定程度地把这些东西简化而已。

所以思考了一番我还是坚持现在的选择，以后如果想改动或者迁移，这里的架构也很方便导入到别的地方去。

##Liquid 的研究

Jekyll 的最大优点之一就是对 Liquid 的支持，通过模板的指令在生成的静态页面里加入动态的内容。 比如 [rsms](rsms.github.com) 在他的首页 html 加入了一些循环、判断、和限制：

{% raw %}
```html
{% for post in site.posts limit:25 %}<a
    href="{{ post.url }}" class="post-excerpt{% if post.photo_url %} photo{% endif %}">
      <div class="padded-content">
        <div class="title">{{ post.title }}</div>
      {% if post.photo_url %}
        <div class="image" style="background-image:url('{{ post.photo_url }}')"></div>
      {% else %}
        <!-- <div class="title">{{ post.title }}</div> -->
        <info datetime="{{ page.date | date: "%Y-%m-%d" }}">
          {{ post.date | date: "%b %Y" }}
        </info>
        {% if post.description %}
        <span class="body">{{ post.description | strip_html }}</span>
        {% else %}
        <span class="body">{{ post.excerpt | strip_html }}</span>
        {% endif %}
      {% endif %}<!-- post.photo_url -->
      </div>
    </a>{% endfor %}
```
{% endraw %}

在首页显示日志，限制在25篇以内，判断是否显示为图片日志，判断是否显示摘要，都是很智能的规则。不过我还没找到 Liquid 的这些定义文档，或者应该是 GitHub 预设的这些定义？

Update:   
找到了 [Liquid for Designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers) 因为我从来没考虑过自己是不是 designer 所以完全忽略了。   
还有 [Havanna](http://havee.me) 翻译的[中文版](http://havee.me/internet/2013-11/jekyll-liquid-designers.html)，虽然我不一定要中文，不过这位的文章配色看起来蛮舒服。
