---
title: 使用hexo+github搭建个人博客
date: 2019-06-30 20:33:23
categories: 博客 #分类
tags: [hexo,github,AppVeyor] 
description: hexo+github
---

   GitHub Pages是非常方便的帮助我们去建立一个静态网站。

   Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

   [Appveyor](https://www.appveyor.com/) 适用于Windows和Linux的持续集成解决方案。该服务免费提供给开源项目，可以在平台上构建，测试，部署应用程序

<!--more-->

> Github pages存放的都是静态文件，博客存放的不只是文章内容，还有文章列表、分类、标签、翻页等动态内容

### 环境

- Windows 10

- [node.js 12.6.0](https://nodejs.org/dist/v12.6.0/node-v12.6.0-x64.msi)

- [GIt 2.22.0](https://github-production-release-asset-2e65be.s3.amazonaws.com/23216272/88a18380-89d0-11e9-8cd3-ee4334db7683?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20190707%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20190707T055134Z&X-Amz-Expires=300&X-Amz-Signature=a44aecc4f4ebab8d019a910d48b8e008dfaecabd11a2584020a946795b7fb44e&X-Amz-SignedHeaders=host&actor_id=38916495&response-content-disposition=attachment%3B%20filename%3DGit-2.22.0-64-bit.exe&response-content-type=application%2Foctet-stream)

- Hexo 3.9.0

  > 安装 Hexo 依赖Node.js(Should be at least nodejs 6.9)和Git

### 搭建GitHub并配置SSH key

- 新建一个名为`你的用户名.github.io`的仓库，一个你存放博客源码的仓库

  > 1. 注册的邮箱一定要验证，否则不会成功；
  > 2. 仓库名字必须是：`username.github.io`，其中`username`是你的用户名
  > 3. 博客源码也可以直接放在 你的用户名.github.io的仓库下，在构建的时候只更新博客所在的目录

- [配置SSH key](https://junqiangni.github.io/2019/07/07/git-使用SSH连接GitHub/)

### 使用Hexo

- [Hexo 安装](https://hexo.io/zh-cn/docs/)(使用 npm 安装 Hexo)

  ``` shell
  $ npm install -g hexo-cli
  ```

- [建站](https://hexo.io/zh-cn/docs/setup)

  ``` shell
  $ hexo init <folder>  
  $ cd <folder> #可以直接到对应的目录下执行 hexo init
  $ npm install
  ```

- [配置](https://hexo.io/zh-cn/docs/configuration)

  您可以在 `_config.yml` 中修改大部分的配置。

- [命令](https://hexo.io/zh-cn/docs/commands)

   常用命令

  -  init

    ```shell
    $ hexo init [folder]
    ```

    新建一个网站。如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。
  
  - new

     ```shell
     $ hexo new [layout] <title>
     ```
  
     新建一篇文章。如果没有设置 `layout` 的话，默认使用 [_config.yml](https://hexo.io/zh-cn/docs/configuration) 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。
  
     ```shell
     $ hexo new "post title with whitespace"
     ```
  
     > 1.生成指定名称的文章至*hexo\source\_posts\postName.md*。或直接在source\_posts中写文档（注意格式）
     >
     > ```markdown
     > ---
     > title: postName #文章页面上的显示名称，可以任意修改，不会出现在URL中
     > date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改categories: #文章分类目录，可以为空，注意:后面有个空格
     > tags: #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
     > ---
     > 这里开始使用markdown格式输入你的正文。
     > ```
     >
     > 2.写博客工具 [Typora网站](https://www.typora.io/)  [下载](https://www.typora.io/windows/typora-setup-x64.exe?)
     >
     > 3.博文列表不显示全部内容
     >
     > ```markdown
     > 在合适的位置加上<!--more--> 即可
     > ```
     >
     > 
  
  - generate
  
    ```shell
    $ hexo generate
    ```
  
    生成静态文件。
  
    | 选项             | 描述                   |
    | :--------------- | :--------------------- |
    | `-d`, `--deploy` | 文件生成后立即部署网站 |
    | `-w`, `--watch`  | 监视文件变动           |
  
  该命令可以简写为
  
    ```shell
    $ hexo g
  ```
  
 - server
  
  	```shell
  	$ hexo server
	```
  
	启动服务器。默认情况下，访问网址为： `http://localhost:4000/`。
  
     | 选项             | 描述                           |
     | :--------------- | :----------------------------- |
     | `-p`, `--port`   | 重设端口                       |
     | `-s`, `--static` | 只使用静态文件                 |
     | `-l`, `--log`    | 启动日记记录，使用覆盖记录格式 |
  
  - [deploy](https://hexo.io/zh-cn/docs/deployment)
  
      ```shell
      $ hexo deploy
      ```
  
      Hexo 提供了快速方便的一键部署功能，让您只需一条命令就能将网站部署到服务器上。
  
      | 参数               | 描述                     |
      | :----------------- | :----------------------- |
      | `-g`, `--generate` | 部署之前预先生成静态文件 |
  
      该命令可以简写为：
  
      ```shell
      $ hexo d
      ```
      
      > 在开始之前，您必须先在 `_config.yml` 中修改参数，一个正确的部署配置中至少要有 `type` 参数，例如
      >
      > ```yaml
      > deploy:
      >   type: git
      >   repository: git@github.com:yourusername/yourusername.github.io.git
      >   branch: master
      > ```
  

   - [主题](https://hexo.io/zh-cn/docs/themes)

     创建 Hexo 主题非常容易，您只要在 `themes` 文件夹内，新增一个任意名称的文件夹，并修改 `_config.yml`内的 `theme` 设定，即可切换主题。

     > [next主题](https://github.com/theme-next/hexo-theme-next)

     

### 参考

1[https://www.cnblogs.com/zhcncn/p/4097881.html](https://www.cnblogs.com/zhcncn/p/4097881.html)

2.[http://ibruce.info/2013/11/22/hexo-your-blog/](http://ibruce.info/2013/11/22/hexo-your-blog/)

3.[https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)

4.https://formulahendry.github.io/2016/12/04/hexo-ci/#more

5.https://segmentfault.com/a/1190000015648687?utm_source=tag-newest

