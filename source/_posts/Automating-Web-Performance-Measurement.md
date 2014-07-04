##自动化web性能评测
Web性能对于一个网站的用户体验来说举足轻重。如果你最近刚好在关注如何提高你的网站性能的话，可能你已经听说过了[PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)-一个分析页面然后提供一些关于如何让它们在不同平台上都有最佳的性能表现的建议。

PageSpeed 的打分结果取决于多个因素，如页面脚本的压缩程度、图片是否经过优化、内容是否使用gzip、点击区域的大小适当以及是否规避了目标网页重定向等。

[研究](http://www.akamai.com/html/about/press/releases/2009/press_091409.html)发现,如果一个页面加载时间超过了3秒，那么40%的人们会选择放弃等待。所以，在开发流程中关注页面在用户设备上的加载速度已经越发必要了。

###构建过程中的性能指标
虽然人工的到[PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)去查看页面评分也还不错，不过大量的开发者们已经在探索在项目构建过程中获取类似的性能评分是否可行了。

答案当然是肯定的~

###PSI for Node 简介
很高兴今天能为大家介绍node中的PSI，一个可以与[Gulp](http://gulpjs.com/)、[Grunt](http://gruntjs.com)以及其他构建系统谐作的新模块。这个模块可以连接到PageSpeed Insights 服务并返回一个详细的web性能报告。下面我们来看下它的报告中包含的指标：![报告预览][1]


> Written with [StackEdit](https://stackedit.io/).


  [1]: http://i.imgur.com/1ub50lI.png