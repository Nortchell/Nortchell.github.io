title: Hexo-admin插件
author: Nortchell
tags: []
categories:
  - 日常杂谈
date: 2021-04-24 21:20:00
---
## 原始方法
在我们放置博客文件的文件夹 Hexo 中，source/_posts/ 目录下存放着所有博文的 Markdown 文件，初始化只有一个 hello-world.md 文件。
我们可以在 Git Bash 中创建新博文：

hexo new
在_posts 目录下会生成相应的.md 文件，接下来我们可以编辑该文件，直接写博文，使用 Markdown 语法。

写完博文后，执行即可在博客中更新。
```
hexo g
hexo d
```
## Hexo Admin 插件管理
用原生的方法来管理博文十分的不便，便有了 Hexo Admin 这一插件来方便我们的操作。

首先安装插件。

npm install --save hexo-admin
启动服务器。
即可在 localhost:4000/admin/ 中编辑博文了。

## Hexo Admin 错误信息解决方法

当你第一次点击 Deploy 按钮时，可能会遇到上面的问题
解决方法:

在项目中创建 hexo-deploy.sh 文件并设置权限
```
$ touch hexo-deploy.sh; chmod a+x hexo-deploy.sh
```
在文件内写入一下内容
```
hexo clean && hexo g && hexo d
```
编辑配置文件
在根目录_config.yml 配置文件中，在之前配置的 admin 配置信息下加入 deployCommand: ‘./hexo-deploy.sh’ 信息

在解决完上述错误信息后，将会报出 deploy Error: spawn UNKNOWN 错误信息
解决方法:

打开 node_modules 目录下 hexo-admin 目录下 deploy.js
将
```
var proc = spawn(command, [message], {detached: true});
```
改为
```
var proc = spawn((process.platform === "win32" ? "hexo.cmd" : "hexo"), ['d']);
```
改完之后便解决了问题

参考博客：
https://chiwai.tang99.club/posts/2672848395.html

## Hexo Admin 图片
Hexo Admin 可以直接复制图片粘贴，然后自动下载到 source/images 目录并重命名。但在 Windows 中粘贴后会出现裂图。这时就需要手动把括号中的前后两个斜杠去掉，就能正常显示。