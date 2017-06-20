---
layout: post
title: bwaiox教你使用jekyll搭建github博客
---

# 使用jekyll建立github博客

#### 简介

> [Markdown](http://zh.wikipedia.org/wiki/MarkDown)是一种轻量级的「标记语言」，很适合写博客。

#### 环境介绍
  笔者使用的本地环境为建立于virtual box内的linux mint 18.1操作系统。编辑器为vim。并且在装好系统后，执行以下指令，以保证本地可以运行jekyll
```
sudo apt install build-essential
sudo apt install git
sudo apt install zlib1g-dev
sudo apt install ruby2.3-dev
sudo apt install nodejs
sudo gem sources --remove https://rubygems.org/
sudo gem sources -a http://gems.ruby-china.org/
sudo gem install bundler
sudo gem install jekyll
```
> 很多文章中的gem source都是淘宝源，但现在淘宝已经推荐ruby-china了
并且你需要将自己的RSA key添加到github以获取权限

#### 本文将记述笔者建立github博客的步骤，并在文章最后进行总结。希望通过本文读者也能建立自己的github博客。

## 一，建立github账号
  这部分内容过于简单，笔者就不再记述了。

## 二，建立个人的博客repo
  在登录github后，点击右上角的'+'，选择'New repository'创建自己的博客repo。repo的名字按照"你的ID.github.io"的格式来写。
> 笔者由于之前已经创建了自己id的repo，在演示期间为了防止重复，创建的repo名字后加了'test'，读者创建repo时一定要将示例的bwaioxtest替换为自己的githubID

![示例图1](http://i38.photobucket.com/albums/e150/1967262017/0_zpstxenzjzd.png)

## 三，在本地建立博客编写环境
* #### 准备环境
  先将github上的repo clone到本地`git clone git@github.com:你的ID/你的ID.github.io.git`
![示例图2](http://i38.photobucket.com/albums/e150/1967262017/2_zpssv9sy6zf.png)

  然后建立Gemfile文件(后面的工具会用到)，并输入以下内容
```
source 'https://gems.ruby-china.org/'
gem 'github-pages', group: :jekyll_plugins
```

  然后我们执行`bundle install`来安装所需要的环境
  ![示例图3](http://i38.photobucket.com/albums/e150/1967262017/3_zpssmj97bxz.png)

  *中间还有一堆log*

  ![示例图4](http://i38.photobucket.com/albums/e150/1967262017/4_zpsoholc8ll.png)

  
* #### 写博客前准备
  jekyll生成博客网站时需要一个_config.yml文件来读取配置，这个文件中记录着生成博客的必备信息。如生成网站用的模板等。
  在这里我们选用[minima](http://github.com/jekyll/minima)来作为博客的主题模板。所以我们向_config.yml中写入如下信息`theme: minima`。

* #### 开始写第一篇文章
> 在minima中，发布的文章需要放在_posts目录下，并且每篇文章中可以有一些设置选项（页面风格，标题等），通过在文章头部的两行---来实现

  先建立_posts目录`mkdir _posts`，后面就可以向这里提交我们的博客了，但这之前，我们还需要先建立我们的首页index.md用来作为我们文章的展示平台。这里只需要向index.md中写入
```
---
layout: home
---
```
  每一篇_posts下的文章，文件名需要的格式为yyyy-mm-dd-标题.md，我们可以写下第一篇文章了。如2017-06-16-blog1.md，并输入文章内容
```
---
layout: post
title: 我的第一篇jekyll日志
---
### 格式可以使用markdown语法
```
![示例图5](http://i38.photobucket.com/albums/e150/1967262017/5_zpsipfthl1m.png)

  使用jekyll的本地预览功能看一下效果，`jekyll serve`时，
![示例图6](http://i38.photobucket.com/albums/e150/1967262017/6_zpszdykaawy.png)

  打开浏览器访问http://127.0.0.0:4000就能看到我们的博客效果了
![示例图7](http://i38.photobucket.com/albums/e150/1967262017/7_zpszvtu4bq7.png)

## 四，继续优化自己的博客
  通过刚才的效果图可见，我们的博客还是十分简陋的。但毕竟有了一个基础，我们可以继续添加自己的内容，让网站更丰富一些。
![示例图8](http://i38.photobucket.com/albums/e150/1967262017/8_zpsgkukxxhj.png)

  我们再来看一下网站的效果
![示例图9](http://i38.photobucket.com/albums/e150/1967262017/9_zpsbfoolxhj.png)

## 五，将博客更新到github上
  一切准备就绪，将网站发布到github上吧。
  首先我们需要将jekyll自动生成的网站目录_site忽略掉，只提交我们的配置文件和日志md文件就可以了`echo "_site" > .gitignore`，即可让git工具忽略掉_site目录。
![示例图10](http://i38.photobucket.com/albums/e150/1967262017/10_zps6ymi8eda.png)

  现在可以把修改先用`git add .`添加到git管理，提交到本地`git commit -m "version 1"`，随后`git push origin master:master`即可
![示例图11](http://i38.photobucket.com/albums/e150/1967262017/11_zps69cg5vwa.png)

  这时，别人就可以通过**http://你的ID.github.io**来访问你的github博客了

#### 总结
  首先建立好github账号和repo，并且准备好自己机器的写作环境，选择自己心仪的jekyll模板后，我们就可以写作了。其中用到的git命令也比较简单，基本就是本文所列。难点在于如何根据模板创作出漂亮的博客页面，这需要对模板做深入的理解，必要时需要读者自行对模板进行修改。最后祝大家写作开心。
  欢迎在大家下方评论区留言。
