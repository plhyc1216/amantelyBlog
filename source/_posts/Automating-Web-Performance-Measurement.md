title:自动化web性能评测
---
Web性能对于一个网站的用户体验来说举足轻重。如果你最近刚好在关注如何提高你的网站性能的话，可能你已经听说过了[PageSpeed_Insights](https://developers.google.com/speed/pagespeed/insights/)-一个分析页面然后提供一些关于如何让它们在不同平台上都有最佳的性能表现的建议

PageSpeed 的打分结果取决于多个因素，如页面脚本的压缩程度、图片是否经过优化、内容是否使用gzip、点击区域的大小适当以及是否规避了目标网页重定向等。

[研究](http://www.akamai.com/html/about/press/releases/2009/press_091409.html)发现,如果一个页面加载时间超过了3秒，那么40%的人们会选择放弃等待。所以，在开发流程中关注页面在用户设备上的加载速度已经越发必要了。

###构建过程中的性能指标
虽然人工的到[PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)去查看页面评分也还不错，不过大量的开发者们已经在探索在项目构建过程中获取类似的性能评分是否可行了。

答案当然是肯定的~

###PSI for Node 简介
很高兴今天能为大家介绍node中的PSI，一个可以与[Gulp](http://gulpjs.com/)、[Grunt](http://gruntjs.com)以及其他构建系统谐作的新模块。这个模块可以连接到PageSpeed_Insights服务并返回一个详细的web性能报告。下面我们来看下它的报告中包含的指标：

![][1]

上面的结果会让你对需要对网站做哪方面的改善一目了然。例如，'调整内容尺寸，使其符合视窗设置'中该项的得分为5.92，这意味着这方面我们还能做一些工作;而'清除首屏中阻止呈现的资源'得分为22,意味着你可能需要使用`async`属性来延迟js文件的加载。

####降低PageSpeed_Insights的使用复杂度
如果你之前已经尝试过使用PageSpeed_Insights的API或者是试着去使用我们基于其构造的工具，很可能你必须去注册一个专用的APIkey。虽然我们都知道这可能只需要几分钟时间，但是我们还是可以将其从日常工作中去掉。

我们很开心的告诉你PageSpeed_Insights服务允许人们可以不使用APIkey最多每5s发送一次请求（对许多人来说已经足够了）。如果你需要更加频繁的使用它或者需要更加谨慎的产品构建，可能你自然会去注册一个key。

PSI模块同时支持有key和无key两种方案。如何注册一个[API_Key](https://developers.google.com/speed/docs/insights/v1/getting_started#auth)的方法文档中有详细说明。

####使用入门
要将PSI并入工作流中有两种可选方案。你可以将其集成到你的项目构建过程中去，也可以是将其作为一个系统中的全局工具来运行。

####构建过程
在Grunt或是Gulp等构建系统中使用PSI是相当直观的。如果你使用的是用Gulp构建的项目，那么你可以直接安装和使用PSI。

#####安装
使用npm安装PSI并用--save-dev参数来将其存入到你的package.json文件中去。
```
npm install psi --save-dev
```
然后像下面这样在你的gulpfile文件中为其定义一个Gulp任务（就像我们的[示例](https://github.com/addyosmani/psi-gulp-sample)中那样）
```
var psi = requrie('psi');
gulp.task('psi', function (cb) {
    psi({
        nokey: true, // or use key:'YOUR_API_KEY'
        url: site,
        strategy: 'mobile'
    }, cb)
});
```
之后你就可以用下面的命令来执行这个任务：
```
gulp psi
```
如果你用的是Grunt,那么你可以使用James Cryer写的[grunt-pagespeed](https://github.com/jrcryer/grunt-pagespeed)，它现在也是用的PSI来提供性能报告。

#####安装
```
npm install grunt-pagespeed --save-dev
```
然后在你的Gruntfile中来加载这个插件：
```
grunt.loadNpmTasks('grunt-pagespeed')
```
并像这样来配置它：
```
    pagespeed: {
        options: {
            nokey: true,
            url: 'http://amantely.com',
            strategy: 'mobile'
        }
    }
```
之后你就可以使用下面的命令用来运行这个任务：
```
grunt pagespeed
```
####安装为全局工具
你同样也可以将PSI安装为系统中的全局工具。同样，我们使用npm来安装这个工具：
```
$ npm install -g psi
```
之后你就可以直接在终端窗口向PageSpeed_Insights请求一个站点的报告，没有key的时候：
```
psi http://www.amanely.com --nokey --strategy=mobile
```
有key的时候：
```
psi http://www.amanely.com --key=YOUR_API_KEY --strategy=mobile
```
以上！

> Written with [StackEdit](https://stackedit.io/).


  [1]: http://i.imgur.com/1ub50lI.png