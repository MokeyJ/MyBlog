###  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">

搜索出来解释最多的是“强制浏览器的渲染方式，默认使用chrome来渲染，然后再按照IE该浏览器的最新版本来渲染”

但是深入一点，这里就不得不提Google的一个项目，那就是Chrome Frame（项目主页，需要FQ），这个项目就是在不改变IE的外观情况下使用Chrome内核，就好比如果IE是个人，那么这个人的四肢不变，但把大脑给换了一样。而上面的写法跟这个项目是有关系的，但是我们现在去访问这个页面会显示“Google Chrome Frame is no longer supported and retired as of February 25, 2014.”，也就是说在2014年的时候就已经不提供支持服务了。

* X-UA-Compatible确实是为了我们定义浏览器的渲染方式的；
* 如果存在客户端Chrome Frame并启用，那么浏览器访问页面会被Chrome内核渲染（这一点没太大意义，因为你开发的项目不能要求用户在客户端来安装Chrome Frame）；也就是说IE浏览器变身Chrome是可以的，但前提是客户端安装了Chrome Frame；
* 使用IE内核浏览器来访问，会渲染至该浏览器的最高版本，比如你使用IE9浏览器，那么就算在兼容模式切换至IE7，但仍会渲染成IE9的样子（当然IE7浏览器是不会渲染成IE9的）。

![Chrome Frame](https://www.csweigou.com/wp-content/uploads/2016/06/234.jpg)

比如现在我在客户端装了Chrome Frame，然后我的IE浏览器是IE11，也就是说我服务器端已经设置了X-UA-Compatible属性的值为IE=edge,chrome=1，客户端已经安装并启用Chrome Frame。我现在用IE浏览器打开指定网页。

![Chrome Frame1](https://www.csweigou.com/wp-content/uploads/2016/06/2355235.png)

在IE浏览器下看到了审查元素，而且点击审查元素出现了在Chrome下几乎一样的控制台。

![Chrome Frame2](https://www.csweigou.com/wp-content/uploads/2016/06/233333.jpg)

X-UA-Compatible还有各种其他的写法，这里就不再说了，可以按照上面的流程来尝试，然后必然或多或少会有一点自己的理解和收获。

转载自：浅析网页meta标签中X-UA-Compatible属性的使用 - 微构网络
