## new 运算符执行的过程

1. 一个新对象被创建。它继承自foo.prototype
2. 构造函数foo被执行。执行的时候，相应的参数会被传入，同时上下文this会被指定为这个新实例。 new foo 等同于 new foo()，只能用在不传递任何参数的情况
3. **如果构造函数返回了一个对象**，那么这个对象会取代整个new出来的结果。如果构造函数没有返回对象，那么new出来的结果为步骤1创建的对象。

接下来 我们用代码模拟一下js中new运算符的一个过程
```javascript
  var new2 = function(f,argArr){
    var obj = Object.create(f.prototype);
    var k = f().apply(obj,argArr);
    if(instanceof k === 'object'){
      return k;
    }else{
      return obj;
    }
  }
```

### 补充： Object.create(prototype, descriptors)

创建一个具有指定原型且可选择性地包含指定属性的对象。

**参数**

|参数|描述|
|---|---|
|prototype|必需。  要用作原型的对象。  可以为 null。 |
|descriptors|可选。  包含一个或多个属性描述符的 JavaScript 对象。 “数据属性”是可获取且可设置值的属性。  数据属性描述符包含 value 特性，以及 writable、enumerable 和 configurable 特性。  如果未指定最后三个特性，则它们默认为 false。  只要检索或设置该值，“访问器属性”就会调用用户提供的函数。  访问器属性描述符包含 set 特性和/或 get 特性。|

**返回值**

一个具有指定的内部原型且包含指定的属性（如果有）的新对象。

**异常**

如果以下任一条件为 true，则引发 TypeError 异常：

* prototype 参数不是对象且不为 null。
* descriptors 参数中的描述符具有 value 或 writable 特性，并具有 get 或 set 特性。
* descriptors 参数中的描述符具有不为函数的 get 或 set 特性。

**备注**

若要停止原型链，可以使用采用了 null prototype 参数的函数。  所创建的对象将没有原型。  

```javascript
  var obj = {name : 'MonkeyJ'};
  var o = Object.create(obj);
  o.__proto__ === obj; //true
```

