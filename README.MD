# hexo

## 工具

- git
- node.js

## 命令

- 安装hexo
`npm install -g hexo`
- 安装其他依赖
`npm install`
- 创建文件夹
`hexo init 文件名`
- 生成静态文件:
`$ hexo generate`

## 本地服务
- `hexo server`默认4000，可能跑不起来
- `hexo server -p 4001`，更换端口

## 发布git

- 配置git路径:
```
deploy:
  repository: https://github.com/Firsmant/Firsmant.github.io.git
  type: git
  branch: master

```

- 安装git支持
`npm install hexo-deployer-git`

- `hexo deployer`
将文件上传到GitHub，会放到`Firsmant.github.io`仓库中


## 常用命令

- 新建博文
`hexo new "博文的标题"`

- 文章基本设置
```
---
title: 简单排序
date: 2018-07-11 22:37:24
comments: true #是否可评论
toc: true #是否显示文章目录
categories: "数据结构/排序" #分类
tags:   "数据结构" #标签
---
```
- 新建标签
`hexo new page tags`
配置tags目录下的index

```
---
title: tags
date: 2018-07-11 22:37:24
type: "tags"
---
```

- 新建分类
`hexo new page categories`
配置categories目录下的index

```
---
title: categories
date: 2018-07-11 22:37:37
type: "categories"
---

```


- 修改无变化
`hexo clean`


### 其他

- 添加README.md,站点配置文件中 
```
skip_render: README.md
```
- 头像，修改主题配置
```
avatar: 
  url:  /images/avatar.jpg
```
- 点击心形
`themes\next\source\js\src`下新建`love.js`
js代码：http://7u2ss1.com1.z0.glb.clouddn.com/love.js
添加引用：`themes\next\layout\_layout.swig`末尾添加：
```  
<!-- 页面点击小红心 -->
  <script type="text/javascript" src="/js/src/love.js"></script>
```
- 头像圆形并旋转
`themes\next\source\css\_common\components\sidebar\sidebar-author.styl`代码部分修改
- 文章显示一部分
```
auto_excerpt:
  enable: true
  length: 150
```