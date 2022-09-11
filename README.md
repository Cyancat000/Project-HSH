# Project HSH
使用先进方式存储数据，实现无服务器搭建环境，快速简单实用的应用商店

我们使用了JSON进行存储，并规定了一系列的格式，前端通过解析JSON就生成出内容，无需额外数据库也无需服务器，只要使用Serverless平台搭建一个能下载文件的环境即可（当然如果你愿意也可以用服务器）

每个应用可以建立一个专属的应用页面，用于展示更新日志、历史版本以及博文，开发者可以在里面添加内容

# 格式
为了让JSON更加工整，我们制定了一系列的格式

## 首页
```
---
title: 标题
date: YY-MM-DD HH:MM:SS
---

文章内容
```

## 索引文件
索引文件顾名思义，是用来存储索引的，索引的JSON格式如下

**注意，为了防止截图图片过多，我们规定最多为十个，子key由1开始，最高为9**

**注意，为了防止标签关联过多，我们规定最多为十个，子key由1开始，最高为9**

如截图或标签并没有达到9个可以不写，解析时将会忽略

```json
[{
  "name": "",
  "url": "",
  "logo": "",
  "screenshorts": {
    "screenshorts-0": "url0",
    "screenshorts-1": "url1",
    "screenshorts-2": "url2",
    "screenshorts-3": "url3",
    "screenshorts-4": "url4",
    "screenshorts-5": "url5",
    "screenshorts-6": "url6",
    "screenshorts-7": "url7",
    "screenshorts-8": "url8",
    "screenshorts-9": "url9"
  },
  "desc": "",
  "tags": {
    "tags-0":"标签0",
    "tags-1":"标签1",
    "tags-2":"标签2",
    "tags-3":"标签3",
    "tags-4":"标签4",
    "tags-5":"标签5",
    "tags-6":"标签6",
    "tags-7":"标签7",
    "tags-8":"标签8",
    "tags-9":"标签9"

  },
  "pages": ""
}
]
```

## 索引文件目录
考虑到存储太多数据在一个JSON文件中就会很难处理，所以我们规定一个索引文件只存储 **100条数据** ，通过该目录指向其他的索引文件

**我们的默认客户端规定上限是9999**

```json
[{
    "0001": "index0001.json",
    "0002": "index0002.json",
    "0003": "文件链接，以此类推"
}]
```

## 应用专属页面的格式
应用专属页面作用是用于展示更新日志、历史版本以及博文，开发者可以在里面添加内容

以下是一个应用专属页面的索引JSON文件的格式
```json
[{
    "title": "资源名称",
    "blog-list": "指向 blog-list.json 的链接",
    "changelog": "指向 changelog.md 的链接"
}]
```

### pages/appname/blog (博客)
以下是一个博客目录的格式
```json
[{
    "title": "文章名字",
    "markdown-url": "markdown文件的链接"
}]
```

以下是一个博文Markdown文件的格式
```
---
title: 标题
date: YY-MM-DD HH:MM:SS
---

文章内容
```

### pages/appname/changelog (更新日志及下载历史版本)
考虑到各种因素，我们认为更新日志只需要一个 `changelog.json` 就可以满足，以下是更新日志的格式

```json
[{
    "version": "v0.2",
    "url": "",
    "desc": ""
},
{
    "version": "v0.2",
    "url": "",
    "desc": ""
},
]
```