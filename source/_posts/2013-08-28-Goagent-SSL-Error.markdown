---
layout: post
title: "解决Mac下Chrome浏览器用Goagent打开HTTPS网站SSL证书错误不受信任问题"
date: 2013-08-28 16:10:28 +0800
comments: true
categories: Mac
---



mac下用goagent FQiang总是会遇到https信任问题，每次访问网站都得点，很烦人，搜了一下，这个解决方法比较好。

打开［应用程序］>［实用工具］>［钥匙串访问］，并在左侧导航选择［系统］。

选择顶部的［文件］>［导入项目］，并定位到goagent安装目录的localCA.crt。选择导入。提示输入系统密码。

双击新导入的GoAgent CA证书，展开［信任］选项，确保所有的选择都是［总是信任］。重启浏览器即可。

[windows下解决方案](http://blog.netsh.org/posts/goagent-https-ssl-error_1013.netsh.html)

[mac、iOS下解决方案](http://blog.netsh.org/posts/mac-goagent-https-error_1443.netsh.html)

推荐mac下工具**GoAgentX**，参考[教程](http://iaiai.iteye.com/blog/1608369)


