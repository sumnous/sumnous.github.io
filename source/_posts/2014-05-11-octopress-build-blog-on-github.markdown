---
layout: post
title: "Octopress build blog on Github 个人建站实录"
date: 2014-05-11 16:10:28 +0800
comments: true
categories: Web
---

为什么选择Octopress：静态+Markdown+Git提交+不需要服务器+有基础的话折腾1-2个小时就能看到效果（这些都是我喜欢的）

这篇[《记录：Octopress建站之旅》](http://jackycode.github.io/blog/2014/02/23/record/)很易上手，有篇易懂易follow的教程是好的开始~(多亏池大 [@池建强](http://weibo.com/idreamland) 分享了 [@Jacky130](http://weibo.com/jackycode) 的博客，我才看到了这篇文章，才想自己动手来做这件事情)

###1. 首先安装Git和Ruby，检查是否安装好

```		
git --version
ruby --version
```	

###2. 安装Octopress到本地，之后的所有操作都在octopress文件下

```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
gem install bundler
rbenv rehash
bundle install
```

可能会有权限问题，请加sudo。在执行`rbenv rehash`的时候系统提示我没有此命令，于是参考[这里](http://jianshu.io/p/ACs3kA)

```
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
```

将$PATH写入~/.bash_profile，也可以参考[rbenv的git页面](https://github.com/sstephenson/rbenv#basic-github-checkout)

```
export RBENV_ROOT="${HOME}/.rbenv"
if [ -d "${RBENV_ROOT}" ]; then
  export PATH="${RBENV_ROOT}/bin:${PATH}"
  eval "$(rbenv init -)"
fi
```
检查rbenv是否可用`rbenv -v`。`rbenv rehash`这条命令，每当切换 ruby 版本和执行 bundle install 之后必须执行这个命令。

###3. 安装主题

<!--more-->

安装默认主题：

```sh
rake install
```

我选的是[WhiteLake](https://github.com/gehaxelt/CSS-WhiteLake)，也可以在[这里](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)选别的第三方主题。

```sh
git clone https://github.com/gehaxelt/CSS-WhiteLake.git .themes/whitelake
rake install['whitelake']
rake generate
```

###4. 在github上部署博客

首先有一个Github账户，创建一个repository，命名为yourGithubName.github.io

```sh
rake setup_github_pages #input your repository's url
rake generate
rake deploy
```

提交source：

```
git add .
git commit -am "this commit's content"
git push origin source
```

###5. 配置Octopress

`_config.yml`文件是今后要多次涉及到的重要配置文件，基本上安装的插件都会出现在这个文件中，可以通过更改true或者false来启用或者关闭，分为3部分：

+ main configs		设置博客的名字等等

+ Jekyll & Plugins		设置侧边栏，每页显示几篇博客，最近的博客显示几篇，read on等等

+ 3rd Party Settings		社会化工具，Github repositories，Twitter，Facebook，Disqus Comments，Google Analytics等等		

####增加页面

比如增加一个About的页面，修改`source/_includes/custom/`下的`navigation.html`文件。添加一条语句，并注意要更改About页面的url为`yourblogurl/about`，增加其他页面也同理，接下来真正的创建页面：

```sh
rake new_page[about]
```
将你想写的内容写在刚生成的`source/about/index.markdown`中，记得提交配置。

```sh
rake generate
git add .
git commit -am "config"
git push origin source
rake preview #http://localhost:4000
rake deploy
```

至此，基本的配置已经完成了。

###6. 发布新博客

将文章命名为“YYYY-MM-DD-post-title.markdown”，也可使用

```sh
rake new_post["title"]
```

帮你生成`source/_posts/YYYY-MM-DD-title.markdown`文件，写博文，然后提交。

```sh
rake generate
git add .
git commit -am "message"
git push origin source
rake preview #http://localhost:4000
rake deploy
```

关于“删除文章”，我总认为这有个小bug，只要文章的名字是命名规则的格式，即使不commit也会出现在博客上，很厌烦，一般直接删除markdown文件就好，为了避免未写完的文章出现在博客上，请写完博文再改名字，然后再提交。


基本上就这样了，剩下的想美化或者想增加功能啊等个性化设置可以继续探索。

###7. Some Tips

####代码高亮

使用**pygments**插件，可以支持N多种语言，语法超简单(只需在代码引用符号后添加语言的名字，就会自动配色)，可以看下这个兄弟的[探索吐槽](http://jinlong.github.io/blog/2013/03/30/octopress-syntax-highlight/)

需装python, ruby, rubypython

修改`_config.yml`中，Jekyll & Plugins的pygments项，从false改为true。

####这位仁兄的[Octopress各种配置](http://biaobiaoqi.me/blog/2013/07/10/decorate-octopress/)写得很详细，可供参考

####可以继续添加的东东

各种统计，tags，最新评论，返回顶部按钮，weiboshow，douban展示，原文链接以及版权信息等等

####推荐Mac上的Markdown写作工具[MOU](http://mouapp.com/)，界面很简单清新，可以支持数学公式。

> 主要参考链接: 
> 
> 1. [http://jackycode.github.io/blog/2014/02/23/record/](http://jackycode.github.io/blog/2014/02/23/record/)
> 2. [http://biaobiaoqi.me/blog/2013/07/10/decorate-octopress](http://biaobiaoqi.me/blog/2013/07/10/decorate-octopress)
> 3. [http://cn.soulmachine.me//blog/20130402/](http://cn.soulmachine.me//blog/20130402/)
> 4. [http://812lcl.com/blog/categories/octopress/](http://812lcl.com/blog/categories/octopress/)


