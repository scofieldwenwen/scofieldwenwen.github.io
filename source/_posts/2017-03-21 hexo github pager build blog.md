---
date: 2017/7/15 20:46:25
upate: 2017/7/17 15:17:00
language: zh-Hans
tags:
  - Hexo
title: Hexo + Github 搭建个人博客
---
欢迎来到 [scofieldwenwen 的个人博客](http://scofieldwenwen.com)，受到[ stormzhang ](http://stormzhang.com)的影响，决定开始搭建自己的博客.该文是我自己搭建博客的过程，采用的是 Hexo 博客框架管理，使用 Github 托管，将自己的域名关联到 Github Pages 上。

## 安装 git
* 在 Windows 平台下载安装 Git， [点击下载Git](https://git-for-windows.github.io/)
* 安装教程: [在 Windows 上安装 Git](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)
* Git 的命令就是 Linux 的 shell 命令行: [Git 基本操作命令](http://www.jianshu.com/p/76f15b958d0c)
* 查看 Git 安装是否完成，在 win+r 中输入 cmd 命令窗口弹出后，输入 git –version 查看 git 版本
* 设置 Git 的用户名和邮箱：
    $ git config --global user.name "scofieldwenwen"
    $ git config --global user.email "scofieldwenwen@163.com"


## 安装 Node.js
* Node.js [官网下载](https://nodejs.org/en/download/)， 下载后基本都是点击下一步完成安装.
* 查看 Node.js 是否安装完成，在 win+r 中输入 cmd 命令窗口弹出后，输入 node -v 查看 Node 版本

## 安装 Hexo
 * 在创建目标文件夹 (如 D:\hexo)，在 hexo 文件夹里，单机右键选择 **Git Bash Here**，输入以下命令安装 Hexo :
     $ npm install -g hexo-cli

* Hexo 初始化配置
    $ npm hexo init 
    $ npm install 

* 初始化之后， hexo 的结构目录如下:![](http://p049pdhen.bkt.clouddn.com/blog_build_hexo%20files.png)

* Hexo 常用的命令行：
    hexo help #查看帮助
    hexo init #初始化一个目录
    hexo new "postName" #新建文章
    hexo new page "pageName" #新建页面
    hexo generate #生成生成静态网页，可以在 public 目录查看整个网站的文件
    hexo server #本地预览，'Ctrl+C'关闭
    hexo deploy #部署.deploy目录
    hexo clean #清除缓存，强烈建议每次执行命令前先清理缓存，每次部署前先删除 .deploy 文件夹

    简写：
    hexo n == hexo new
    hexo g == hexo generate
    hexo s == hexo server
    hexo d == hexo deploy

* Hexo 安装 server，生成静态文件后，用 server 启动服务器，从而预览。
    $ npm install hexo-server --save 

* 可以就可以查看第一个 hexo 默认生成的 blog ，输入命令：
     $ hexo generate
      $ hexo server 
     在浏览器查看本地静态网页：[http://localhost:4000/](http://localhost:4000/)
     ![](http://p049pdhen.bkt.clouddn.com/blog_build_hexo%20local%20preview.png)
      看到这个页面有点小激动，本地博客搭建起来了，不过只是个本地的网页而已，接下来就要把网页部署上去。

## 将博客部署到 Github Pages 上
* 准备一个 Github 账号，没有的就去[官网](https://github.com/)注册一个账号。
* 创建一个仓库 repository，用来托管博客。仓库名必须为 [github用户名].github.io 
  ![](http://p049pdhen.bkt.clouddn.com/blog_build_github%20create%20repository.png)

* 配置 SSH 密钥教程：[github 设置添加 SSH](http://www.cnblogs.com/ayseeing/p/3572582.html)
* 将本地的 Hexo 文件同步到 Github 的仓库中：
  复制刚才创建仓库的 HTTPS 链接
  ![](http://p049pdhen.bkt.clouddn.com/blog_build_github%20clone%20repository.png)
  将链接粘贴到 Hexo 文件目录的 _config.yml 配置文件上保存：
      deploy:
    type: git
      repo: https://github.com/scofieldwenwen/scofieldwenwen.github.io.git
      branch: master
  **注意**：配置文件键值之间必须有个空格
  将博客部署上去：
     $ hexo g
   $ hexo d
  或者直接输入
   $ hexo g -d
  在浏览器查看 Github Pages，在浏览器输入 username.github.io (我的是scofieldwenwen.github.io) 就可以看到自己的博客了!到这里一个免费的博客就创建好了。

## 配置博客以及主题
* 配置博客： [Hexo 官网教程](https://hexo.io/zh-cn/docs/configuration.html)
* 在 [Hexo 官网](https://hexo.io/themes/) 选取主题
* 将主题在 Github 上打开，复制 Clone HTTPS ，然后在在 hexo\theme 目录下 clone 该主题，如我使用是Next主题
    git clone https://github.com/iissnan/hexo-theme-next.git
* clone 成功后，修改 Hexo 目录中的配置文件 _config.yml 的主题 ，主题名字为 clone 下来的主题文件夹名称
    theme: hexo-theme-next
* 生成静态网页，查看本地效果
      $ hexo g
    $ hexo s
* 效果可以的话，就部署到 Github 上
     $ hexo clean
     $ hexo g -d

## 将自己的域名关联上 Github Pages 上
* 购买一个域名，我的是在[ 阿里云 ](https://wanwang.aliyun.com/domain/)上购买的。
* 配置 CNAME 文件
  在 \hexo\source 文件夹下创建文件 CNAME （没有后缀名），编辑内容，填写申请的域名。
* 修改 DNS
  ![](http://p049pdhen.bkt.clouddn.com/blog_build_ali%20cloud%20dns.png)
* **注意:** 不能有不能有相同的主机记录,比如我的邮箱也有 @ 的主机记录,我就不需要邮箱就把它删了。


## 大功告成
* 最后网页部署，浏览器输入域名（scofieldwenwen.com）或者自己 Github Pages 的地址
  ![](http://p049pdhen.bkt.clouddn.com/blog_build_my_blog.png)

## 总结

  *  搭建 hexo 中还会用到一些插件，这个因人而异，当然这些插件都是有说明文档的，照着来就行。
  *  万事开头难，但是一旦开始就要把它做好！
  *  接下来就是要坚持写自己的博客了，记录总结，留下自己成长的过程！


