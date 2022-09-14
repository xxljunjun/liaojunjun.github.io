### hexo_github搭建个人博客

### 新建xxljunjun.github.io

### npm install -g hexo-cli

### hexo init

### hexo g

### hexo s

### 启动项目
+ npm run server
```
http://localhost:4000/
```

### 将Hexo部署到GitHub
+ 更改_config.yml
```
deploy:
  type: git
  repository: https://github.com/fengye97/fengye97.github.io.git  #你的仓库地址
  branch: master
```
+ npm install hexo-deployer-git --save
```js
// 上传到xxljunjun.github.io项目
hexo clean   #清除缓存文件 db.json 和已生成的静态文件 public
hexo g       #生成网站静态文件到默认设置的 public 文件夹(hexo generate 的缩写)
hexo d       #自动生成网站静态文件，并部署到设定的仓库(hexo deploy 的缩写)
```

### 可以通过github访问
```
http://xxljunjun.github.io
```

### 更换主题
+ hexo s 
```

```

### 新写文章
+ hexo new "我的第一篇博客"



