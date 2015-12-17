title: 利用github-pages搭建静态博客
date: 2015-10-20
tags: Github
---

*什么是GitHub Pages？*
GitHub Pages本用于介绍托管在GitHub的项目， 不过，由于他的空间免费稳定，用来做搭建一个博客再好不过了。
<!--more-->
## 新建Repository
格式如下，username是GitHub的用户名，可以在GitHub的账户相关信息中看到
![](http://7xlxb6.com1.z0.glb.clouddn.com/imagesGitHub%20Pages%2001.png)

新建完成后，通过[username].github.io这种形式的地址可以访问。

## 安装Hexo

系统环境：
> win7 64bit
node v0.10.5
npm 1.2.19

Hexo安装，要用全局安装，加-g参数。打开命令行windows(cmd)/linux(Terminal)
```shell 
npm install -g hexo-cli
```

### 建站

```shell 
$ hexo init <folder>
$ cd <folder>
$ npm install
```
<folder>是站点存放目录，如果不指定<folder>默认为当前目录。hexo init执行完成后会在站点目录下生成
```
├── _config.yml
├── package.json
├── scaffolds
├── scripts
├── source
|   |
|   └── _posts
└── themes
    |
    └── landscape
```
.config.yml：站点的配置文件；
source:      博客文章存放目录；
themes:		 站点主题存放位置；

切记，执行完hexo后，不要忘记在站点目录下执行`npm install`

### 添加文章
```shell
hexo new post "article-title"
```
这条命令会在你的博客目录的 source/_posts 下生成一个 article-title.md 的文件，用编辑器打开article-title.md就可以编辑文章了。
博客文章遵循markdown语法。关于markdown，请找度娘or谷姐。

### 发布文章
```shell
hexo g
```
命令执行完后，会生成一个public目录，这就是站点文件，我们只需要把这里面的文件上传至github。
### 预览
```shell
hexo s
```
hexo 默认启动 `http://localhost:4000/`，
如下图所示
 ![](http://7xlxb6.com1.z0.glb.clouddn.com/hubidankanhexo-s.png) 

### 添加自定义页面
执行new page命令
`hexo new page "about"`
在hexo\source\下会生成about目录，里面有个index.md，直接编辑就可以了，然后在主题的_config.yml中将其配置显示出来。
上述步骤，也可以手工生成，在hexo\source\下手工新建about和index.md也是完全等价的。


## 上传至GitHub Pages
git上传命令就不在这详细讲了。

## 如何绑定新的域名
可能觉得[username].github.com这个域名不太好，可以自定义一个自己域名。那么首先需要有一个自己的域名。
然后需要将域名解析到`192.30.252.154`和`192.30.252.153`到，至于如何解析，可以域名提供商的管理控制台设置。界面类似于下图：
 ![](http://7xlxb6.com1.z0.glb.clouddn.com/hubidankandns.png) 
然后在第一步新建的Repository根目录下新建`CNAME`(注意大小写)文件，这个文件内容就是你自己的域名，不需要其他任何东西。
可以参考[github官方配置文档](https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/) 
 接下来等待十分钟左右，就可以通过自己的域名访问站点了。


 ## 补充说明
 其实hexo本身具有直接部署到github的功能，可以研究下。