---
layout: post
title: "Octopress 配置"
date: 2014-05-12 11:10:28 +0800
comments: true
categories: Web
---

###友言+jiathis+Recent comments

###返回顶部 back to top

###原文链接

###404页面（不一定写）

###rake generate编译不过的问题

###Mathjax and kramdown--让Markdown支持Latex Math数学公式

在`source/_includes/custom/footer.html`第一行加入代码：

```
	<!-- mathjax config similar to math.stackexchange -->
	<script type="text/x-mathjax-config">
	MathJax.Hub.Config({
  	  jax: ["input/TeX", "output/HTML-CSS"],
  	  tex2jax: {
        inlineMath: [ ['$', '$'] ],
    	displayMath: [ ['$$', '$$']],
    	processEscapes: true,
    	skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
  	  },
  	  messageStyle: "none",
  	  "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"] }
	});
	</script>
	<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML" type="text/javascript"></script>
```

安装解析器kramdown，代替默认的rdiscount：

```
sudo gem install kramdown #Mac下sudo
```

修改`_config.yml`文件下`markdown:rdiscount`为`markdown:kramdown`。

**解决右击公式全屏空白的问题：**在`sass/base/_theme.scss`中如下位置添加`#main`：

```
body {
  > div#main {
    background: $sidebar-bg $noise-bg;
```

> 参考：
> 
> 1. [http://cn.soulmachine.me/blog/20130402/](http://cn.soulmachine.me/blog/20130402/)
> 2. [http://www.idryman.org/blog/2012/03/10/writing-math-equations-on-octopress/](http://www.idryman.org/blog/2012/03/10/writing-math-equations-on-octopress/)



