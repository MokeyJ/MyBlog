#### crossorigin

那些没有通过标准CORS检查的正常script 元素传递最少的信息到 {domxref('GlobalEventHandlers.onerror', 'window.onerror')}。可以使用本属性来使那些将静态资源放在另外一个域名的站点打印错误信息。

```html
<script src="" crossorigin="anonymous"></script>
```
在HTML5中，一些 HTML 元素提供了对 CORS 的支持， 例如 <img> 和 <video> 均有一个跨域属性 (crossOrigin property)，它允许你配置元素获取数据的 CORS 请求。 这些属性是枚举的，并具有以下可能的值：

|关键字|描述|
|---|---|
|anonymous|对此元素的CORS请求将不设置凭据标志。|
|use-credentials|	对此元素的CORS请求将设置凭证标志; 这意味着请求将提供凭据。|

默认情况下 （即未指定crossOrigin属性时）, CORS 根本不会使用。“anonymous" 关键字说明不会通过 cookies，客户端 SSL 证书或 HTTP 认证交换用户凭据。

即使是无效的关键字和空字符串也会被当作 anonymous 关键字使用。

你可以使用下面的<script> 元素告诉一个浏览器执行来自 https://example.com/example-framework.js 的脚本而不发送用户凭据。

```HTML
<script src="https://example.com/example-framework.js" crossorigin="anonymous"></script>
```
