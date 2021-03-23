---
 
title: 'Hexo: 用GitHub搭建自己的博客网站'
date: 2019-10-27 18:04:27
tags: Hexo
categories: Hexo
---

## Hexo：用Github搭建自己的博客网站！

作为一名程序猿，拥有一个自己的博客来记录学习和一闪而过的灵感是一件好处多多的事，既可以帮助自己进步，也可以在别人遇到类似问题的时候帮上忙，~~甚至还可以面试的时候装个*~~。当然，现在网络上的各类博客有很多，诸如大家耳熟能详的CSDN、博客园、简书等等，可以直接发表自己的文章，这些网站用户交互做的很好，并且贴心地支持Markdown。

然而自己购买域名和服务器专门来搭建博客网站，除了购买成本令人望而生畏外，光是花力气搭建网站、定期维护就需要可观的精力和时间。

那么，接下来就要隆重介绍今天的主角——**hexo**！

#### Hexo 简介
------
Hexo是一款基于Node.js的静态博客框架，网页托管在Github上，安装使用非常方便，完全是搭建博客的首选！

文章分为两个部分：

- hexo的初级搭建，github部署，以及个人域名的绑定
- hexo的基本配置，主题更换等

**Let's Go！**

#### 第一部分  hexo的初级搭建
------
### Hexo搭建步骤

1. 安装Git
2. 安装Node.js
3. 安装Hexo
4. Github创建个人仓库
5. 生成SSH添加到GitHub
6. 将hexo部署到Github
7. 设置个人域名
8. 发布文章！

### 1. 安装Git

绝对不能不知道这个工具！不了解它的同学们！出门左转赶紧学起来！

- **Windows**
&emsp;&emsp;到Git官网下载[Git Download](https://gitforwindows.org/) ，安装后就可以用 **Git Bash** 命令行工具来使用Git了。安装好后，在Git Bash中输入`git --version`检验是否安装成功


<img src="Hexo：用GitHub搭建自己的博客网站\git安装成功检验.PNG" width="60%" height="60%">

- **Linux**

&emsp;&emsp;对Linux来说，就是一行代码的事儿

```bash
sudo apt-get install git
```

&emsp;&emsp;同样，安装好后，用`git --version`查看版本

### 2. 安装Node.js

hexo是基于Node.js编写的，所以需要一下Node.js和里面的npm工具。

- **Windows** 

&emsp;&emsp;[Node.js](https://nodejs.org/en/download/)官网下载LTS版本，64位msi安装包，安装后分别在命令行（`win+R`输入`cmd`调用）输入`node -v`和`npm -v`检验PATH环境变量是否配置了Node.js

&emsp;&emsp;<img src="Hexo：用GitHub搭建自己的博客网站\nodejs安装成功检验.PNG" width="60%" height="60%">

- **Linux** 


  ```bash
  sudo apt-get install nodejs
  sudo apt-get install npm
  ```

&emsp;&emsp;检验安装成功方式同Windows

### 3. 安装hexo

Windows环境进入Git Bash，Linux环境进入终端，开始搭博客啦！

首先新建一个文件夹blog来存放自己的博客，然后`cd`进入到这个文件夹下，输入下面的命令安装hexo

```bash
npm install -g hexo-cli
```

同样，安装完毕后需要`hexo -v`查看一下版本

<img src="Hexo：用GitHub搭建自己的博客网站\hexo安装成功检验.PNG" width="60%" height="60%">

至此需要的工具都安装完了。接下来初始化一下hexo

```bash
hexo init blog
```

这里的blog取什么名字都行

<img src="Hexo：用GitHub搭建自己的博客网站\initBlog.PNG" width="60%" height="60%">

这时，在你的blog文件夹下会出现一个新的blog文件夹，进入到这个子文件夹后新建hexo

```bash
npm install
```

新建完成后，指定文件夹目录下应该有以下主要文件：

- **node_modules**：依赖包
- **scaffolds**：生成文章的一些模板
- **source**：用来存放自己的文章
- **themes**：网站主题
- **__config.yml**：博客的配置文件

```bash
hexo g
hexo server
```

输入以上命令来开启hexo服务，在浏览器中输入`localhost:4000`就可以看到博客的初始化界面啦，现在还是有点丑丑的，大概长这样

<img src="Hexo：用GitHub搭建自己的博客网站\server.PNG" width="60%" height="60%">

`ctrl-c`可以把服务关掉

此时再回到文件夹，你会发现多了一个`public`文件夹，这时用来存放生成的页面的。

### 4. GitHub创建个人仓库

上文提到过，hexo的静态网页是托管在GitHub中的，所以需要在GitHub中新建一个 **和你用户名相同的** 仓库，后面加 **.github.io**，也就是**xxxx.github.io**，只有这样将来要部署到GitHub Page的时候才会被识别。

### 5. 生成SSH添加到GitHub

回到Git Bash中，输入命令

```bash
git config --global user.name "yourname"
git config --global user.email "youremail"
```

这里的`yourname`对应你的GitHub用户名，`youremail`对应你的GitHub注册邮箱，这样GitHub才能知道你是不是对应它的用户。不放心的话可以用下面两条命令来检查一下：

```bash
git config user.name
git config user.email
```

然后创建SSH，你可以选择密钥的保存位置，然后一路回车

```bash
ssh-keygen -t rsa -C "youremail"
```

<img src="Hexo：用GitHub搭建自己的博客网站\rsa.png" width="60%" height="60%">

创建成功后，文件夹下会有两个文件，其中`id_rsa`是你这台电脑的私人密钥，`id_rsa.pub`是公共密钥。把公钥放在GitHub上，这样当你链接GitHub自己的账户时，她就会根据公钥匹配你的私钥，匹配成功才能通过git上传自己的文件到GitHub上。

在GitHub的setting（右上角头像下拉）中找到`SSH and GPG keys`的设置选项，点击`New SSH key`，把的`id_rsa.pub`里面的内容复制进去。

然后回到Git Bash，试试能否ssh通。

<img src="Hexo：用GitHub搭建自己的博客网站\ssh.png" width="60%" height="60%">

### 6. 将hexo部署到GitHub

在这步中，我们将要把hexo和GitHub关联起来，使得hexo生成的文章都部署到GitHub上。

打开网站配置文件`_config.yml`，拉到最后，将`deploy`部分修改为：

```yml
deploy:
  type: git
  repo: https://github.com/YourGithubName/YourGithubName.github.io.git
  branch: master
```

其中，`YourGithubName`对应你的GitHub账户，并且注意`:`后必须要跟一个空格。

接下来安装`deploy-git`，也就是部署的命令，只有这样才能用命令将文章部署到GitHub上

```bash
npm install hexo-deployer-git --save
```

然后

```bash
hexo clean
hexo generate
hexo deploy
```

- **hexo clean**：清除之前生成的东西，在日后新部署文章的时候可以使用，现在加不加没什么区别
- **hexo generate**：生成静态文章，缩写`hexo g`
- **hexo deploy**：部署文章，缩写`hexo d`

出现下图说明部署成功

<img src="Hexo：用GitHub搭建自己的博客网站\deploy.png" width="60%" height="60%">

在浏览器地址栏中输入`https://yourname.github.io`就可以看到你的博客网站了！！像这样⬇

<img src="Hexo：用GitHub搭建自己的博客网站\初始化界面2.png" width="60%" height="60%">

### 7. 设置个人域名

是不是觉得`.github.io`逼格太低了？那就来氪金设置个人域名吧！

在[阿里云](https://wanwang.aliyun.com/?spm=5176.8142029.digitalization.2.e9396d3e46JCc5)上注册一个账号，再买一个域名，每个后缀的价格都不一样，最便宜的是`.top`，而应用最广泛的`.com`就比较贵。实名认证后进入控制台，展开左侧菜单栏，选择域名进入，你会看到自己购买的域名，点解析进入。

<img src="Hexo：用GitHub搭建自己的博客网站\解析.png" width="60%" height="60%">

<img src="Hexo：用GitHub搭建自己的博客网站\解析2.png" width="60%" height="60%">

选择添加记录，设置如下：

<img src="Hexo：用GitHub搭建自己的博客网站\添加记录.png" width="60%" height="60%">

然后重新进入之前创建的仓库，点击`Settings`，在`Options`中下拉到`GitHub Pages`部分，在`Custom domain`中输入自己的域名。随后在博客文件夹blog下新建一个名为`CNMAE`的文件，不要加后缀，在里面写上自己的域名。最后重新在Git Bash中

```bash
hexo clean
hexo g
hexo d
```

等一小会儿时间，再打开浏览器，输入自己的域名，就可以看到刚才的初始化界面啦

接下来就可以开始写文章并发布了。

```bash
hexo new "newArticleName"
```

它会在`source/_post`文件夹下新建一个同名的`markdown`文件，编辑完成后，再

```c++
hexo clean
hexo g
hexo d
```

等一会儿就可以看到更新了，是不是很！简！单！

#### 第二部分 hexo的基本配置

------

这部分我们来介绍hexo的基本配置、主题更换等。

### 1. hexo基本配置

blog文件夹下的`_config.yml`文件是整个hexo框架的配置文件，下面我们简单介绍几个常用配置，详细信息可以参考[官方](https://hexo.io/zh-cn/docs/configuration)的配置描述。

#### 网站 - Site

这部分参数包括了

- **title**：网站标题
- **subtitle**：网站副标题
- **description**：网站描述
- **author**：博客作者，也就是你的名字
- **language**：网站语言，中文使用`zh-CN`
- **timezone**：网站时区。默认使用电脑时区，或者自己设置`Asia/Shanghai`

#### 网址 - URL

这部分参数包括了

- **url**：网址，也就是你的网站域名 
- **root**：网站根目录，默认为`\` 
- **permalink**：生成文章永久链接时的格式，不同的参数表示不同的链接格式，官方文件有详细说明，这里给出几种例子 


  |               参数               |            描述             |
  | :------------------------------: | :-------------------------: |
  |    `:year/:month:day:title/`     |   2019/10/26/hello-world    |
  | `:year-:month-:day-:title.html/` | 2019-10-26-hello-world.html |
  |       `:category/:title/`        |     foo/bar/hello-world     |


- **permalink_defaults**：永久链接格式中各部分的默认值

#### 主题 - theme

`theme`参数决定了你选择什么主题，官网上有很多个主题，默认的是`landscape`，你可以在官网上下载自己喜欢的主题，放在`theme`文件夹下，同时将这个参数修改为主题文件夹名称即可。

#### 个别文件变量 - Font matter

`Font matter`是Markdown文件最上方以`---`分隔的区域，用于指定文件自己的变量，例如：

<img src="Hexo：用GitHub搭建自己的博客网站\font-matter.png" >

预先定义的参数有：

|     参数     |       描述       |
| :----------: | :--------------: |
|   `layout`   |       布局       |
|   `title`    |       标题       |
|    `date`    |     创建日期     |
|  `updated`   |     更新日期     |
|  `comments`  |     开启评论     |
|    `tags`    |       标签       |
| `categories` |       分类       |
| `permalink`  | 覆盖文章默认网址 |

**layout**是在每一次创建新文件时使用的布局，也就是说`new`这个命令实际上是

```bash
hexo new [layout] <title>
```

hexo有三种不同的布局，对应了三种不同的存储路径

- **post**：这是hexo默认使用的布局，新建的文件保存在`source/_posts`下 


- **page**：如果想另起一页，就可以使用 


```bash
hexo new page board
```


&emsp;&emsp;这句命令会让系统在`source`文件夹下创建一个`board`文件夹，以及文件夹中的`index.md`。
- **draft**：如果文章太长一次写不完，可以先写草稿文件，这样就不会被别人看到了。 


```bash
hexo new draft newArticle 
# 在source/_draft中创建一个newArticle.md文件。
hexo server --draft 
# 在本地端口中开启预览服务
hexo publish draft newpage 
# 将完成的草稿文件发送到`post`中发表
```


像上面例子中的`mathjax`参数是自己在主题文件夹下`_config.yml`中修改的，用来开启`Latex`的使用。

### 2. 更换主题

如果觉得默认主题不好看，那么就可以在[官网主题](https://hexo.io/themes/)中选择自己喜欢的进行修改。这里强烈推荐 [**NexT主题**](https://github.com/theme-next/hexo-theme-next)！非常简洁，赏心悦目。

<img src="Hexo：用GitHub搭建自己的博客网站\next.png">

直接从github上下载下来放到`theme`文件夹下，再把`theme`参数改成对应主题名字就ok了