# hexo 

### 工具
- git
- node.js

### 命令

- 创建文件夹
`hexo init 文件名`

- 生成静态文件:
`$ hexo generate`

### 本地服务
- `hexo server`默认4000，可能跑不起来
- `hexo server -p 4001`，更换端口

### 发布git

- 配置git路径:
```
deploy:
  repository: https://github.com/Firsmant/Firsmant.github.io.git
  type: git
  branch: master

```

- 安装git支持
`npm install hexo-deployer-git`

- 将文件上传到GitHub，会放到`Firsmant.github.io`仓库中
`hexo deployer`

### 常用命令

- 新建博文
`hexo new "博文的标题"`

- 修改无变化
`hexo clean`


### 其他

- 在source目录下添加README.md,站点配置文件中 
```
skip_render: README.md
```