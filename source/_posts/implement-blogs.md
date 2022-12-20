---
title: implement blogs
date: 2022-12-17 01:07:45
categories: 技术杂谈
tags:
  - github page
  - hexo
  - next

---
**部署blog步骤**

## Preparation

1. 在着手搭建博客之前，需要准备以下环境&技术。

2. 一台电脑，PC/Mac 均可。

3. 不算太差的网络环境。

4. Markdown 基本语法，为了后面的博客写作使用。

5. 一个 GitHub 账号。

## 安装和配置 Git
```
brew install git
```
### 配置 Git

在首次安装 Git 后，需要对其进行配置，添加用户的名称与邮箱。
```

$ git config --global user.name "githubname"

$ git config --global user.email "name@mail.com"
```

另外为了让本地安装的 Git 能够顺利提交代码到 GitHub 上，还需要生成密钥。
```

$ ssh-keygen -t rsa -C "name@mail.com"
```

### 配置 GitHub

访问 GitHub 网站，并登录你的账号，如果没有账号可以注册一个。

依次点击右上角【头像】-【Settings】-【SSH and GPG keys】-【SSH keys】-【New SSH key】。

在 Title 中填上任意名字，并在 Key 中将上一步的公钥文件中的内容复制粘贴进去，然后点击【Add SSH key】。此时本地安装的 Git 应该已经可以顺利提交代码到你的 GitHub 账号了。

## 安装 Node.js

Windows 环境下安装 Node.js

推荐使用 nvs 来安装 Node.js 。

首先下载并安装 nvs 。打开 PowerShell ，执行以下命令来使用淘宝源安装LTS版本的 Node.js ：
```
> nvs remote add taobao https://npm.taobao.org/mirrors/node/
nvs add taobao/lts
nvs use taobao/lts
nvs link taobao/lts
```
MacOS 环境下安装 Node.js

推荐使用 Homebrew 来安装 Node.js 。
```
$ brew install node
```
## 安装和配置 Hexo

### 安装 Hexo

在命令行工具中，执行以下命令来安装 Hexo ：

初始化 Hexo 项目打开命令行工具并进入想要作为博客目录的父目录中，执行以下命令，初始化 Hexo 项目目录。
```
$ npx hexo init <folder_name>

$ cd <folder_name>

$ npm install
```
对 Hexo 项目进行基本配置Hexo 项目目录下的_config.yml文件是 Hexo 的站点配置文件，一些常规配置项都在此文件中进行配置。编辑该文件，我们来进行一些基础配置。修改站点名称修改站点配置文件的title配置项，例如修改为：title: Just Another Blog此时网站名称将修改为Just Another Blog。修改作者名称修改站点配置文件的author配置项，例如修改为：author: Ruka Kayamori此时网站作者将修改为Ruka Kayamori。启动本地 Hexo Server执行以下命令可以启动本地服务。
```
$ hexo clean

$ hexo g

$ hexo s
```
默认的本地访问地址是http://localhost:4000。

上面是最初始的博客页面，里面会有一篇自带的 Hello World 博文。

## 编写博文

创建新的博文文件在 Hexo 项目目录中，执行以下命令可以创建一篇新的博文文件。

其中，layout代表新建的文件的布局名称，默认为post，即博文；也可以选择draft，即草稿，草稿默认不会显示在 Hexo 页面中，在执行过hexo publish命令后会将草稿发布为博文。title为博文的标题。

将 Hexo 项目部署到 GitHub Pages

安装 hexo-deployer-git 插件

在 Hexo 项目目录中，执行以下命令来安装必要的插件。

### 编辑 Hexo 站点配置

打开 Hexo 项目的站点配置文件，并修改url配置项。然后再编辑deploy配置项及其子项。
```
$ npm install hexo-deployer-git --save
```
## 创建 GitHub Repo

在 GitHub 首页登录你的账号，然后点击右上方的+，再点击New repository。在Repository name中输入<你的GitHub用户名>.github.io，其他保持不变即可，再点击Create repository即可完成 Repo 的创建。
```
vim /Users/allen/Project/blog/hexo/_config.yml

url: https://githubname.github.io

deploy:
  type: 'git'
  repo: https://githubname/githubname.github.io
```
注意点：
1. Github后续更新了默认主分支的名称，已经不叫master了，改为了main，如果还是写master，并不会报错，但是会在main分支之外新建一个master分支 
2. repository一栏必须填ssh的地址，因为GitHub的密码验证于2021年8月13日不再支持，也就是不能再用密码方式去提交代码。要使用personal access token替代，当然这里我建议用SSH免密登陆，具体GitHub如何配置SSH免密登陆的步骤参考上面

## 部署项目
```
hexo -d
```
在 Hexo 项目目录中，执行以下命令来将项目部署到 GitHub Pages。
```
$ hexo clean

$ hexo deploy
```
后续有新的博文更新或者是配置变更，都通过重复本步骤来部署到 GitHub Pages 中。

## 启用 GitHub Pages 服务在 
GitHub 上打开<你的GitHub用户名>.github.io项目，点击Settings，再点击Pages，选择master分支后点击Save。

启用配置后，可能需要稍等一段时间（半小时左右），GitHub 才会刷新CDN缓存。
## 访问页面
访问https://<你的GitHub用户名>.github.io/即可在公网上查看我们的博客页面。

至此基础部署完成，但默认主题看起来比较单调，可进行配置

## 安装 NexT 主题

在 Hexo 目录中执行以下命令来安装 NexT 主题。
```
$ npm install hexo-theme-next
```
### 启用 NexT 主题

打开 Hexo 项目的站点配置文件，并修改theme配置项。
```
theme: next
```
### 创建主题配置文件

在 Hexo 项目根目录，创建一个名为_config.<theme_name>.yml的空文件。

例如我们是 NexT 主题，那么就创建_config.next.yml文件。

然后我们将 Hexo 项目根目录下的node_modules/hexo-theme-next/_config.yml文件中的全部内容拷贝到_config.next.yml文件中。

后续我们将_config.next.yml文件称为主题配置文件，以区别站点配置文件。

### 更改 NexT 主题显示方案

NexT 主题拥有4种显示方案，分别是Muse、Mist、Pisces和Gemini，默认配置为Muse。如果要修改显示方案，打开主题配置文件，修改scheme配置项即可，例如修改为Pisces方案。
```
# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```
刷新到github page较慢，可通过```hexo d``` 启动本地服务调试查看，本地地址查看：

http://localhost:4000/

至此部署环境基本完成，如果与更深更个性化的部署需求，比如主题更改等，可详细参考官网，接下来是主要的博文编写发布

## 发布博文

### 新建页面
```
hexo new page "页面名称"
```
--建在 hexo/source下
### 新建博文
```
hexo new "页面名称" "文章题目"
```
"页面名称"如果不填默认在post 下

### 编辑博文

文本编辑器打开博文，markdown格式，比如typora

### 发布到github
```
hexo clean hexo deploy
```

如果暂时不想发布，写草稿，并进行本地预览：
```
hexo new draft test
hexo server --draft
```
如果准备发布草稿：
```
hexo publish test
```

## 自定义页面
### 新建相关文件夹
```
mkdir source/html
```
在 blog 的源文件夹下找到 source 文件夹，在该文件夹下新建一个文件夹用来储存后继需要部署的 html 文件。该文件夹下可以新建子文件夹，方便存放 css、js文件。
### 关闭渲染
自定义的 html 文件需要跳过渲染，否则会像文章页、标签页一样，无法自己编辑格式：
在 config.yml 文件里（注意是Hexo本身自带的config.yml，不是主题带的config.yml）找到
```
skip_render:                #跳过指定渲染，可用glob来匹配路径
```
在后面添加文件或文件夹路径即可：
```
- "html/**"               #跳过html文件夹下所有子文件夹和文件的渲染
```
记得加’-‘；具体可参考 [Chak Aciano的文章](https://blog.csdn.net/weixin_58068682/article/details/116611715)

### 添加链接至首页
在 _config.next.yml 文件下（即自己安装的主题的config文件）找到 menu ：

```
menu:
   首页: / || fas fa-home
   归档: /archives/ || fas fa-archive
   标签: /tags/ || fas fa-tags
   分类: /categories/ || fas fa-folder-open
   #清单||fas fa-list:
     #音乐: /music/ || fas fa-music
     #电影: /movies/ || fas fa-video
   友链: /link/ || fas fa-link
   #关于: /about/ || fas fa-heart
   简历: /html/resume/resume.htm || fas fa-file-user
```

创建页面
```
hexo new page tags
hexo new page categories
hexo new page link
hexo new page about

```

## 其他设置
### 统计阅读时间
文章添加阅读时间，npm安装：
```
npm install hexo-symbols-count-time
```

在 Hexo 的配置文件中加入下面的配置（这里的字长已经评价时间是按照中文配置的，英文 / 中英混合需要修改 awl 以及 wpm 参数）：
```
symbols_count_time:
  symbols: true
  time: true
  total_symbols: true
  total_time: true
  exclude_codeblock: false
  awl: 3
  wpm: 200
  suffix: "mins."
```
确认 NexT 的配置（默认就是这个不必添加修改，确认一下存在无误即可）：
```
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: false
```

### 盘古插件
方便显示，在中英文已经数字符合等合适位置加入一下空格间隔以美化 UI。
```
pangu: true
```

### 搜索功能
NexT 主题自带了一个搜索功能 Local Search，即在编译文件时本地生成一个数据库，放在网站根目录下，用户借助此数据库进行搜索查询。 安装：
```
npm install hexo-generator-searchdb
```
在 NexT 的配置文件中打开：
```
local_search:
  enable: true
```


### 文末添加今日诗词
给个人博客添加一些人文气息，文末调用今日诗词的 API 根据访问的时间地点等智能推荐一句诗词，参考官方提供的接口文档，使用高级安装代码以显示更多信息。

### 创建文件夹
```
mkdir source/_data
```

首先通过主题配置将自定义页尾项取消注释：
```
custom_file_path:
  postBodyEnd: source/_data/post-body-end.njk
```
然后新建文件 source/_data/post-body-end.njk，并在其中加入下面内容即可


```
vim source/_data/post-body-end.njk
<script src="//sdk.jinrishici.com/v2/browser/jinrishici.js"></script>
<script>
  jinrishici.load((result) => {
    let jrsc = document.getElementById('jrsc');
    const data = result.data;
    let author = data.origin.author;
    let title = '《' + data.origin.title + '》';
    let content = data.content.substr(0, data.content.length - 1);
    let dynasty = data.origin.dynasty.substr(0, data.origin.dynasty.length - 1);
    jrsc.innerText = content + ' @ ' + dynasty + '·' + author + title;
  });
</script>
<div style="text-align: center"><span id="jrsc" >正在加载今日诗词....</span></div>

```


### 同步生成文件夹
将每篇博客对应生成一个文件夹目录（方便插入图片等附件）：
```
post_asset_folder: true
```


### 博文添加更新时间
更新模板：*scaffolds/post.md*
```
---
title: {{ title }}
date: {{ date }}
update: {{ date }}
tags:
---

```

### 添加分类

生成分类目录
```
hexo new page categories
```

在categories目录中有一个index.md文件，在文件中添加type: categories
在categories目录中有一个index.md文件，多个分类可以复制多份

```
vim source/categories/index.md

---
title: 分类一
date: 2022-12-18 00:19:23
type: categories
---

title: 分类二
date: 2022-12-18 00:19:23
type: categories
---
```

给文章添加"分类"属性
```
---
title: 文章标题
date: 2022-12-18 00:19:23
categories: 分类一
---
```

### 添加标签
生成标签目录
```
hexo new page tags
```

在tags目录中有一个index.md文件，在文件中添加type: tags

```
vim source/tags/index.md

---
title: 标签一
date: 2022-12-18 00:19:23
type: tags
---

---
title: 标签二
date: 2022-12-18 00:19:23
type: tags
---

```

给文章添加"标签"属性
```
---
title: 文章标题
date: 2022-12-18 00:19:23
categories: 分类
tags:
  - 标签一
  - 标签二
---
```


### 打开网页版编辑
1. 
[网页vscode打开](https://github1s.com/hophiya/hophiya.github.io)

但是这种方式打开的 VS Code 只能用于阅读源码不支持编辑功能，并且不能添加扩展

2. github.dev方式
Opening the github.dev editor
You can open any GitHub repository in github.dev in either of the following ways:

- To open the repository in the same browser tab, press . while browsing any repository or pull request on GitHub.

- To open the repository in a new browser tab, press >.

- Change the URL from "github.com" to "github.dev".

- When viewing a file, use the dropdown menu next to  and select Open in github.dev.


### 添加评论


### 添加浏览量

参考：
[Hexo博客：二、添加分类及标签](https://www.jianshu.com/p/98ce38df7f87)

### 源码单独保存
1. 单独建立分支，参考：[使用git分支保存hexo博客源码到github](https://zhuanlan.zhihu.com/p/71544809)

将本地hexo目录与远程仓库关联
进入到本地hexo工程目录，也就是我们通常执行hexo new post等命令的目录，执行如下操作：

```
git remote add origin https://github.com/hophiya/hophiya.github.io.git
git add .
git commit -m 'hexo source post'
git push origin source
```

因为我们只需要保留博客源码，其他无关的文件并不希望推送，需要确保配好了.gitignore文件
```
cat .gitignore
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
_multiconfig.yml%
```

删除public等文件（可选）
因为source分支是从master分支新建的，初始代码实际就是master的拷贝，因而master中已有的public等deploy生成的文件也会一起带过来，这些都不算是博客源文件，如果你也觉着source分支还存着这些有些别扭，就可以先在本地把它删掉，然后执行：

git add .
git commit -m 'DEL: public things which only for deploy'
git push origin source


2. Hexo 项目编译生成静态页面，部署到 gh-pages


### 常用命令汇总
至此基本完成部署，后续主要写博客及代码部署，常用命令如下：

新建博文:
```
hexo new "文章题目"
```

给文章添加分类和标签:
```
---
title: 文章标题
date: 2022-12-18 00:19:23
categories: 分类
tags:
  - 标签一
  - 标签二
---
```

部署博客：
```
$ hexo clean

$ hexo deploy
```

合并原文件：
```
git branch -a
* source(显示为当前分支)
git fetch origin source
```

合并到远程仓库：
```
git push origin source
```

*end*


本文部署过程参考： 

[hexo官方手册](https://hexo.io/zh-cn/docs/ )

[如何搭建个人独立博客？](https://www.zhihu.com/question/20463581/answer/2492289487 )

[Github Pages搭建个人博客(最新版)](https://www.jianshu.com/p/745eacc56227)

[Hexo 博客 NexT 主题的安装使用](http://home.ustc.edu.cn/~liujunyan/blog/hexo-next-theme-config/#hexo-%E5%AE%89%E8%A3%85)

[Hexo创建自定义页面](https://zhuanlan.zhihu.com/p/525469921)

[博客字数以及阅读时间估计插件](https://github.com/theme-next/hexo-symbols-count-time)

[Hexo博客：二、添加分类及标签](https://www.jianshu.com/p/98ce38df7f87)

[github+hexo搭建博客怎么增加评论和浏览量功能？](https://www.zhihu.com/question/47405173/answer/2348712269?utm_id=0)

[valine](https://valine.js.org/quickstart.html)

[在网页端使用 VS Code 编辑 GitHub 项目——github.dev](https://sspai.com/post/68891)

[The github.dev web-based editor](https://docs.github.com/en/codespaces/the-githubdev-web-based-editor)

[使用git分支保存hexo博客源码到github](https://zhuanlan.zhihu.com/p/71544809)

[Hexo+GitHub搭建个人博客，实现云端编辑、一键发文](https://www.jianshu.com/p/cafbaec21a2a)

一并感谢
