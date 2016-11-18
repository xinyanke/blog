---
title: Hexo
date: 2016-11-15 17:13:02
tags:
- hexo
comments: true
categories: 
- 工具箱
---

>## 什么是Hexo?

Hexo 是一个快速、简洁且高效的博客框架。
* 超快速度
* 支持Markdown
* 一键部署
* 丰富的插件

>## 安装Hexo

1. 必备程序（安装步骤略）
	* Node.js
	* Git
2. 安装Hexo
`npm install -g hexo-cli`

>## 建站

下列命令 将会在指定文件夹中新建所需要的文件。

```
hexo init <folder>
cd <folder>
npm install
```
新建完成后，指定文件夹的目录如下：

```
|—— _config.yml	   // 网站的配置信息
|—— package.json   // 应用程序的信息
|—— scaffolds	   // 模板文件夹
|—— source	   // 存放用户资源的地方
|	|—— _drafts
|	|—— _posts // markdown和html文件会被解析并放到此文件夹
|__ themes	   // 主题文件夹，根据此主题生成静态页面

```

>## 配置

* _config.yml 配置参数

| 参数 | 描述 |
| --- | --- |
| title | 网站标题 |
| subtitle | 网站副标题 |
| description | 网站描述 |
| author | 您的名字 |
| language | 网站使用的语言 |
| timezone | 网站时区 |

* 网址

| 参数 | 描述 | 默认值 |
| --- | --- | --- |
| url | 网址 |   |
| root | 网站根目录 |  |
| permalink | 文章的永久链接格式 | :year/:mouth/:day/:title/ |
| permalink_default | 永久链接中各部分的默认值 |

> 网站存放在子目录
如果存放在子目录中，例如`http://yoursite.com/blog`,则请将`url`设为`http://yoursite.com/blog`，并把`root` 设为`/blog/`

* 目录

| 参数 | 描述 | 默认值 |
| --- | --- | --- |
| source_dir | 资源文件夹，这个文件夹用来存放内容。 | source |
| public_dir | 公共文件夹，这个文件夹用于存放生成的站点文件。 | public |
| tag_dir | 标签文件夹 | tags |
| archive_dir | 归档文件夹 | archives |
| category_dir | 分类文件夹 | categories |
| code_dir | Include code 文件夹 | downloads/code |
| i18n_dir | 国际化（i18n）文件夹 | :lang |
| skip_render | 跳过指定文件的渲染，您可使用 glob 表达式来匹配路径。 |   |

* 文章

| 参数 | 描述 | 默认值 |
| --- | --- | --- |
| new_post_name | 新文章的文件名称 | :title.md |
| default_layout | 预设布局 | post |
| auto_spacing | 在中文和英文之间加入空格 | false |
| titlecase | 把标题转换为 | title case |
| false | external_link | 在新标签中打开链接 | true |
| filename_case | 把文件名称转换为 (1) 小写或 (2) 大写 | 0 |
| render_drafts | 显示草稿 | false |
| post_asset_folder | 启动 Asset 文件夹 | false |
| relative_link | 把链接改为与根目录的相对位址 | false |
| future | 显示未来的文章 | true |
| highlight | 代码块的设置 |  |

>## 指令

* init
`hexo init [folder]` 新建，如果没有设置folder，默认在目前的文件夹建立

* new
`hexo new [layout] <title>`
新建一篇文章，如果没有设置`layout`，默认使用`_config.yml`中的`default_layout`参数代替。如果标题包含空格的话，使用括号括起来

* generate
`hexo generate` 生成静态文件。 -d 文件生成后立即部署网站。-w 监视文件变动

* publish
`hexo publish [layout] <filename>` 发表草稿

* server
`hexo server` 启动服务器。默认访问网址:http://localhost:4000
-p 重设端口; -s 只使用静态文件; -l 启动日记记录，使用覆盖记录格式

* deploy
`hexo deploy` 部署网站 -g 部署之前预先生成静态文件

* render
`hexo render <file1> [file2] ...` 渲染文件 -o 设置输出路径

* migrate
`hexo migrate <type>` 从其他博客系统迁移内容

* clean
`hexo clean` 清楚缓存文件db.json 和已生成的静态文件(public)

* list
`hexo list <type>` 列出网站资料

* version
`hexo version` 显示hexo版本

```
hexo --safe 	// 安全模式，不会载入插件和脚本
hexo --debug	// 调试模式，在终端显示调试信息并记录到`debug.log`
hexo --silent	// 简洁模式，隐藏终端信息
hexo --config custom.yml	// 自定义配置文件的路径，将不再使用_config.yml
hexo --draft	//显示草稿
hexo --cwd /path/to/cwd		//自定义当前工作目录的路径

```
>## 写作

`hexo new [layout] <title>` 创建新文章。

* 布局（layout） 

```
post	//source/_posts
page	//source
draft	//source/_drafts
```
> 不要处理我的文章
如果你的文章不想被处理，可以将Front-Matter中的`layout:`设为`false`

* 文件名称
Hexo 默认以标题做为文件名称，可以编辑`new_post_name`参数来改变默认的文件名称，例如:`:year-:month-:day-:title.md` 可以通过日期来管理文章。

| 变量 | 描述 |
| --- | --- |
| :title | 标题（小写，空格将会被替换为短杠） |
| :year | 建立的年份，比如， 2015 |
| :month | 建立的月份（有前导零），比如， 04 |
| :i_month | 建立的月份（无前导零），比如， 4 |
| :day | 建立的日期（有前导零），比如， 07 |
| :i_day | 建立的日期（无前导零），比如， 7 |

* 草稿
`hexo publish [layout] <title>` 将保存到`source/_drafts`文件夹中的草稿移动到`source/_posts`文件夹
草稿默认不会显示在页面中，您可在执行时加上` --draft` 参数，或是把` render_drafts` 参数设为 true 来预览草稿

>## Front-matter
Front-matter 是文件最上方以 --- 分隔的区域，用于指定个别文件的变量。

| 参数 | 描述 | 默认值 |
| --- | --- | --- |
| layout | 布局 |
| title | 标题 |
| date | 建立日期 | 文件建立日期 |
| updated | 更新日期 | 文件更新日期 |
| comments | 开启文章的评论功能 | true |
| tags | 标签（不适用于分页） |
| categories | 分类（不适用于分页） |
| permalink | 覆盖文章网址 |

* 分类和标签
只有文章支持分类和标签，您可以在 Front-matter 中设置。在其他系统中，分类和标签听起来很接近，但是在 Hexo 中两者有着明显的差别：分类具有顺序性和层次性，也就是说 Foo, Bar 不等于 Bar, Foo；而标签没有顺序和层次。

```
categories:
- Diary
tags:
- PS3
- Games
```
>## 标签插件

标签插件和 Front-matter 中的标签不同，它们是用于在文章中快速插入特定内容的插件。

* 引用块
在文章中插入引言，可包含作者、来源和标题。
别号： quote
```
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```
* 代码块
在文章中插入代码。
别名： code
```
{% codeblock [title] [lang:language] [url] [link text] %}
code snippet
{% endcodeblock %}
```
* 在文章中插入 iframe。

```
{% iframe url [width] [height] %}

```
* Image
在文章中插入指定大小的图片。

```
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}

```
* Link
在文章中插入链接，并自动给外部链接添加` target="_blank"` 属性。

```
{% link text url [external] [title] %}

```

* Vimeo
在文章中插入 Vimeo 视频。

```
{% vimeo video_id %}

```

* 引用文章
引用其他文章的链接。

```
{% post_path slug %}
{% post_link slug [title] %}

```
* 引用资源
引用文章的资源。

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}

```
* Raw
如果您想在文章中插入 Swig 标签，可以尝试使用 Raw 标签，以免发生解析异常。

```
{% raw %}
content
{% endraw %}

```

>## 资源文件夹

资源（Asset）代表 source 文件夹中除了文章以外的所有文件，例如图片、CSS、JS 文件等。比方说，如果你的Hexo项目中只有少量图片，那最简单的方法就是将它们放在 source/images 文件夹中。然后通过类似于` ![](/images/image.jpg)` 的方法访问它们。

>## 服务器

`hexo server` 启动服务器，期间，文件变动会自动更新。

`hexo server -p 5000` 修改端口

`hexo server -s` 静态模式,只处理`public`文件夹内的文件，而不会处理文件变动。

`hexo server -i 192.168.1.1` 自定义IP

>## 生成文件

`hexo generate` 生成静态文件
`hexo generate --watch` 监视文件变动并立即重新生成静态文件。
`hexo generate --deploy` 和 `hexo deploy --generate` 两个命令相同，生成完毕后自动部署网站。

>## 部署

`hexo deploy` 一键部署到服务器
开始之前，必须先在`_config.yml` 中修改参数，一个正确的部署配置中至少要有` type` 参数，例如：
```
deploy:
  type: git
```
您可同时使用多个deployer，Hexo 会依照顺序执行每个 deployer。
```
deploy:
- type: git
  repo:
- type: heroku
  repo:
```
>## Git

安装 hexo-deployer-git。
`$ npm install hexo-deployer-git --save`
修改配置:
```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```
| 参数 | 描述 |
| --- | --- |
| repo | 库（Repository）地址 |
| branch | 分支名称。如果您使用的是 GitHub 或 GitCafe 的话，程序会尝试自动检测。 |
| message | 自定义提交信息 |

>## 其他方法

生成的所有文件都在`public`文件夹中，可以将它们复制到任何地方。

（完结）


