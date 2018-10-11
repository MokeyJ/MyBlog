## meta name="renderer"浏览器内核控制

由于众所周知的情况，国内的主流浏览器都是双核浏览器：基于Webkit内核用于常用网站的高速浏览。基于IE的内核用于兼容网银、旧版网站。以360的几款浏览器为例，我们优先通过Webkit内核渲染主流的网站，只有小量的网站通过IE内核渲染，以保证页面兼容。在过去很长一段时间里，我们主要的控制手段是一个几百k大小网址库，一个通过长期人工运营收集的网址库。

尽管我们努力通过用户反馈、代码标签智能判断技术提高浏览器的自动切核准确率。但是在很多情况下，我们仍然无法达到百份百正确。因此，我们新增加了一个控制手段：内核控制Meta标签。只要你在自己的网站里增加一个Meta标签，告诉360浏览器这个网址应该用哪个内核渲染，哪么360浏览器就会在读取到这个标签后，立即切换对应的内核。并将这个行为应用于这个二级域名下所有网址。

目前该功能已经在所有的360安全浏览器实现。我们也建议其它浏览器厂商一起支持这个实现。让这个控制标签成为行业标准。

```html
<html>
  <head>
    <meta name="renderer" content="webkit|ie-comp|ie-stand">
  </head>
  <body>
  </body>
</html>
```

content的取值为webkit,ie-comp,ie-stand之一，区分大小写，分别代表用webkit内核，IE兼容内核，IE标准内核。
 
若页面需默认用极速核，增加标签：<meta name="renderer" content="webkit"> 

若页面需默认用ie兼容内核，增加标签：<meta name="renderer" content="ie-comp"> 

若页面需默认用ie标准内核，增加标签：<meta name="renderer" content="ie-stand">

各渲染内核的技术细节

|内核|Webkit|IE兼容|IE标准|
|----|----|----|----|
文档模式|Chrome 21|IE6/7|IE9/IE10/IE11(取决于用户的IE)
HTML5支持|YES|NO|YES
ActiveX控件支持|NO|YES|YES
