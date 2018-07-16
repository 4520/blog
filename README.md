# 博客源码



## 部署博客

需要安装依赖
```node

npm install hexo-deployer-git --save 

```

配置仓库
deploy:
  type: git
  repo: git@github.com:4520/blog.git
  branch: master
