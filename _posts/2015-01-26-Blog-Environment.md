---
layout: default
title: 关于写作环境
---
在电脑上我是选择了 GitHub 的 Windows 客户端 + Sublime Text 3 来编辑和提交修改，不但可以很方便地编辑和预览 Markdown 文件，还可以对其它格式的文件很方便地操作。为了保持热情和更方便地更新文档，我还在手机上安装了 Pocket Git + JotterX 来执行相同的事情。这也有助于我对 Git 的版本管理和分支管理有更直观的理解。

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


