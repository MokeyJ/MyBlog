## js几种常见的继承方式及缺点

#### 组合继承
缺点: 方法都在构造函数中定义，函数复用无从谈起，所有的方法都会重新创建

```javascript
  function Parent(name){
    this.name = name;
    this.num = [1,2,3];
    this.sayHi = function(){
      alert(this.name);
    }
  }
  function Child(name,age){
    Parent.call(this,name);
    this.age = age;
  }
```


#### 原形链式继承
缺点: 包含引用类型的属性会被共享,还有constructor的指向问题

```javascript
  function Parent(name){
    this.name = name;
    this.num = [1,2,3];
  }
  Parent.prototype.sayHi = function(){
    alert(this.name);
  }
  function Child(name,age){
    this.name = name;
    this.age = age;
  }
  Child.prototype = new Parent();
  
  var ch1 = new Child('MonJ',24);
  console.log(ch1.name, ch1.age, ch1.num);
  ch1.sayHi();
  console.log(ch1 instanceof Child, ch1 instanceof Parent);
  console.log(ch1.__proto__.constructor);
  var ch2 = new Child();
  ch2.num.push(4);
  console.log(ch1.num);
```

#### 组合式继承
缺点: 无论什么情况下，都会调用两次超类型构造函数，且还有constructor的指向问题

```javascript
  function Parent(name){
    this.name = name;
    this.num = [1,2,3];
  }
  Parent.prototype.sayHi = function(){
    alert(this.name);
  }
  function Child(name,age){
    Parent.call(this,name);
    this.age = age;
  }
  Child.prototype = new Parent();
  
  var ch1 = new Child('MonJ',24);
  console.log(ch1.name, ch1.age, ch1.num);
  ch1.sayHi();
  console.log(ch1 instanceof Child, ch1 instanceof Parent);
  console.log(ch1.__proto__.constructor);
  var ch2 = new Child();
  ch2.num.push(4);
  console.log(ch1.num);
```

#### 组合式继承优化1
缺点: constructor的指向问题

```javascript
function Parent(name){
    this.name = name;
    this.num = [1,2,3];
  }
  Parent.prototype.sayHi = function(){
    alert(this.name);
  }
  function Child(name,age){
    Parent.call(this,name);
    this.age = age;
  }
  Child.prototype = Parent.prototype;
  
  var ch1 = new Child('MonJ',24);
  console.log(ch1.name, ch1.age, ch1.num);
  ch1.sayHi();
  console.log(ch1 instanceof Child, ch1 instanceof Parent);
  console.log(ch1.__proto__.constructor);
  var ch2 = new Child();
  ch2.num.push(4);
  console.log(ch1.num);
```

#### 组合式继承优化2

```javascript
  function Parent(name){
    this.name = name;
    this.num = [1,2,3];
  }
  Parent.prototype.sayHi = function(){
    alert(this.name);
  }
  function Child(name,age){
    Parent.call(this,name);
    this.age = age;
  }
  Child.prototype = Object.create(Parent.prototype);
  Child.prototype.constructor = Child;
  
  var ch1 = new Child('MonJ',24);
  console.log(ch1.name, ch1.age, ch1.num);
  ch1.sayHi();
  console.log(ch1 instanceof Child, ch1 instanceof Parent);
  console.log(ch1.__proto__.constructor);
  var ch2 = new Child();
  ch2.num.push(4);
  console.log(ch1.num);
```
