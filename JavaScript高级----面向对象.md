# JavaScrip面向对象

#### 回顾JavaScript

#####      JavaScript是什么

​           解释执行： 轻量级解释型的

​           语言特点：动态，头等函数    （又称函数是JavaScript中的一等公民）

​           执行环境：在宿主坏境下运行，浏览器是最常见的JavaScript宿主环境

​                             （在很多非浏览器环境中也使用JavaScript，例如node.js）

#####     JavaScript的组成

​           ECMAScript---语法规范

​                  1.变量，数据类型，类型转换，操作符

​                   2. 流程控制语句：判断，循环语句

​    		   3.数组，函数，作用域，预解析

​    		   4.对象，属性，方法，简单类型和复杂类型的区别

​    		    5.内置对象：Math，Date，Array，基本包装类型String，Number，Boolean

   Web APIs

​           BOM

​                onload页面加载事件，window顶级对象

​                定时器

​                location，history

​           DOM 

​                获取页面元素，注册事件

​                属性操作，样式操作

​                节点操作，节点层次

​                动态创建元素

​                事件：注册事件的方式，事件的三个阶段，事件对象

#### 面向对象   

#####       1. 什么是对象

​             对象是单个实物的抽象

​             对象是一个容器，封装了属性（property）和方法（method）

​             实际开发中，对象是一个抽象的概念，可以即将其理解为：数据集或功能集。

​             ECMAScript-262 将对象定以为：无序属性的集合，其属性可以包含基本值，对象或者函数

#####       2.什么是面向对象

​             面向对象编程是一种编程开发思想，是基于面向过程而言的，就是说面向对象是将功能等通过对象来实现，将功能封装进对象中，让对象去实现具体的细节；这种思想是将数据作为第一位，而方法或者说算法作为其次，这是对数据的一种优化，操作起来更加的方便，简化了过程。

#####      3.程序中面向对象的基本体现

​      假如我们要处理学生的成绩表，为了表示一个学生的成绩，**面向过程**可以用一个对象表示：

```javascript
var std1 = { name: 'Michael', score: 98 }
var std2 = { name: 'Bob', score: 81 }
```
而处理学生成绩可以通过函数实现，比如打印学生的成绩

```javascript
function printScore (student) {
  console.log('姓名：' + student.name + '  ' + '成绩：' + student.score)
}
```
​     如果采用面向对象的程序设计思想，首先不考虑程序的执行流程，而是  `student`这种数据类型应该被视为一个对象，这个对象有`name`和`score`这两个属性（property）

抽象数据行为模板（Class）

   ```javascript
  function Student(name, score) { 
      this.name = name;  this.score = score; 
      this.printScore = function() {   
          console.log('姓名：' + this.name + '  ' + '成绩：' + this.score); 
      }
  }            
   ```

根据模板创建具体实例对象（Instance）：

```javascript
var std1 = new Student('Michael', 98)
var std2 = new Student('Bob', 81)
```

实例对象有自己的具体行为

```javascript
std1.printScore() // => 姓名：Michael  成绩：98
std2.printScore() // => 姓名：Bob  成绩 81
```

Class是一种抽象概念，比如我们定义的Class---Student。是指学生这个概念，

实例（Instance）则是一个个具体的Student，比如Michael ，Bob是两个具体的Student。

所以面向对象的设计思想是：

- 抽象出Class（构造函数）
- 根据Class（构造函数）创建Instance（实例）
- 指挥Instance得结果

面向对象的抽象程度有比函数高，应为一个Class既包含数据，又包含操作数据的方法

##### 4.面向对象的特性

​      面向对象的三大特征：封装，继承、多态

​              1.封装：只隐藏对象的属性和实现细节，仅对外提供公共访问方式

​                             好处：将变化隔离、便于使用、提高复用性、提高安全性

​                             原则：将不需要对外提供的内容隐藏起来；把属性隐藏，提供公共方法对其访问

​               2.继承：提高代码复用性；继承是多态的前提

​                        注：①子类中所有的构造函数都会默认访问父类中的空参数的构造函数，默认第一行有super()；若无空参数构造函数，子类中需指定；另外，子类构造函数中可自己用this指定自身的其他构造函数。

​              3.多态：是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象

​                             好处：提高了程序的扩展性

​                             弊端：当父类引用指向子类对象时，虽提高了扩展性，但只能访问父类中具备的方法，不可访问子类中的方法；即访问的局限性。

前提：实现或继承关系；覆写父类方法。

[![iTPXtA.md.png](https://s1.ax1x.com/2018/11/06/iTPXtA.md.png)](https://imgchr.com/i/iTPXtA)

#### 创建对象

##### 1对象字面量

  对象字面量就是一个{}，里面的属性和方法均是**键值对**

例如：

```javascript
var o = {
            name: "生命壹号",
            age: 26,
            isBoy: true,
            sayHi: function() {
                console.log(this.name);
            }
        };
console.log(o);
```

##### 2.利用构造函数

```javascript
 //利用构造函数自定义对象
        var stu1 = new Student("smyh");
        console.log(stu1);
        stu1.sayHi();

        var stu2 = new Student("vae");
        console.log(stu2);
        stu2.sayHi();


        // 创建一个构造函数
        function Student(name) {
            this.name = name;    //this指的是构造函数中的对象实例
            this.sayHi = function () {
                console.log(this.name + "厉害了");
            }
        }
```

##### 3.工厂函数

​    通过该方法可以大批量的创建对象

```javascript
 /*
         * 使用工厂方法创建对象
         *  通过该方法可以大批量的创建对象
         */
        function createPerson(name, age, gender) {
            //创建一个新的对象
            var obj = new Object();
            //向对象中添加属性
            obj.name = name;
            obj.age = age;
            obj.gender = gender;
            obj.sayName = function() {
                alert(this.name);
            };
            //将新的对象返回
            return obj;
        }
```

   然后生成实例对象

```javascript
 var obj2 = createPerson("猪八戒", 28, "男");
        var obj3 = createPerson("白骨精", 16, "女");
        var obj4 = createPerson("蜘蛛精", 18, "女");
```

通过工厂函数模式我们解决了创建多个相似对象代码多余的问题，但是没有解决对象识别的问题（即怎么知道一个对象的类型）。

#### 构造函数

#####   一种更优雅的工厂函数：构造函数

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
  this.sayName = function () {
    console.log(this.name)
  }
}

var p1 = new Person('Jack', 18)
p1.sayName() // => Jack

var p2 = new Person('Mike', 23)
p2.sayName() // => Mike
```

##### 解析构造函数代码的执行

要创建`Person`实例，必须使用`new`

 new之后构造函数会经历一下四步：

1. 开辟内存空间，存储出创建的对象。
2. 将构造函数的作用域赋给新对象（因此this就指向了这个新对象）
3. 执行构造函数中的代码，设置对象属性和方法
4. 返回新创建的对象。

具体的伪代码如下：

```javascript
function Person (name, age) {
  // 当使用 new 操作符调用 Person() 的时候，实际上这里会先创建一个对象
  // var instance = {}
  // 然后让内部的 this 指向 instance 对象
  // this = instance
  // 接下来所有针对 this 的操作实际上操作的就是 instance

  this.name = name
  this.age = age
  this.sayName = function () {
    console.log(this.name)
  }

  // 在函数的结尾处会将 this 返回，也就是 instance
  // return this
}
```

##### 构造函数和实例对象的关系

在每个实例对象中同时有一个`constructor`属性，该属性指向创建该实例的构造函数：

```javascript
console.log(p1.constructor === Person) // => true
console.log(p2.constructor === Person) // => true
console.log(p1.constructor === p2.constructor) // => true
```

总结：

- 构造函数是根据具体的事物抽象出来的抽象模板
- 实例对象是根据抽象的构造函数模板得到的具体实例对象
- 每一个实例对象都具有一个`constructor`属性，指向创建该实例对象的构造函数（constructor是实例的属性的说法不严谨）
- 可以通过`constructor`属性判断实例和构造函数之间的关系（这种方式不严谨，推荐使用`instanceof`操作符。）

##### 构造函数的问题

​     使用构造函数最大的好处就是创建对象更方便了，但是其本身也存在一个浪费内存的问题

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
  this.type = 'human'
  this.sayHello = function () {
    console.log('hello ' + this.name)
  }
}

var p1 = new Person('Tom', 18)
var p2 = new Person('Jack', 16)
```

上述代码中，对于每一个实例对象，`type`和`sayHello`的内容都是一模一样的，每次生成实例对象都会重复内容，多占用一些内存，如果实例对象很多，会造成极大的内存浪费。

对于这种问题我们可以把需要共享的函数定义到构造函数外部

```javascript
function sayHello = function () {
  console.log('hello ' + this.name)
}

function Person (name, age) {
  this.name = name
  this.age = age
  this.type = 'human'
  this.sayHello = sayHello
}

var p1 = new Person('Top', 18)
var p2 = new Person('Jack', 16)

console.log(p1.sayHello === p2.sayHello) // => tru
```

如果有多个需要共享的函数的话，就会造成全局命名空间冲突的问题。

我们又可以把多个函数放到一个对象中用来避免全局命名空间冲突的问题

```javascript
var fns = {
  sayHello: function () {
    console.log('hello ' + this.name)
  },
  sayAge: function () {
    console.log(this.age)
  }
}

function Person (name, age) {
  this.name = name
  this.age = age
  this.type = 'human'
  this.sayHello = fns.sayHello
  this.sayAge = fns.sayAge
}

var p1 = new Person('lpz', 18)
var p2 = new Person('Jack', 16)

console.log(p1.sayHello === p2.sayHello) // => true
console.log(p1.sayAge === p2.sayAge) // => true
```

但是这样难免显得代码变得复杂了！

#### 原型

#####     原型`prototype`的概念

  我们所创建的每一个函数，解析器都会向函数中添加一个属性`prototype`。这个属性对应着一个对象，这个对象就是我们所谓的原型对象。

   如果函数作为普通函数调用prototype没有任何作用，当函数以构造函数的形式调用时，他所创建的实例对象中都会有一个隐含的属性，指向该构造函数的原型，我们可以通过`__proto__`来访问该属性。

 原型对象就相当于一个公共的区域，所有同一个类的实例都可访问到这个原型对象，我们可以将对象中共有的内容，统一设置到原型对象中。

##### 更好的解决方案

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
}

console.log(Person.prototype)

Person.prototype.type = 'human'

Person.prototype.sayName = function () {
  console.log(this.name)
}

var p1 = new Person(...)
var p2 = new Person(...)

console.log(p1.sayName === p2.sayName) // => true
```

这是所有实例的`typpe`属性和`sayName()`方法，其实都是同一个内存地址，指向`prototype`对象，因此就提高了运行效率。

##### 构造函数，实例，原型三者之间的关系

[![iTS65q.md.png](https://s1.ax1x.com/2018/11/06/iTS65q.md.png)](https://imgchr.com/i/iTS65q)

![iTSjMD.png](https://s1.ax1x.com/2018/11/06/iTSjMD.png)

总结：

- 任何函数都具有一个`prototype`属性，该属性是一个对象
- 构造函数的`prototype`对象默认都有一个`constructor`属性，指向`prototype`对象所在函数
- 通过构造函数的得到的实例对象内部会包含一个指向构造函数的`prototype`对象的指针`__proto__`
- 所有实例都直接或间接继承了原型对象的成员

##### 原型对象的搜索原则：原型链

[![iTpjf0.md.png](https://s1.ax1x.com/2018/11/06/iTpjf0.md.png)](https://imgchr.com/i/iTpjf0)

每次代码读取某个对象的某个属性时，都会执行一次搜索，目标是具有给定名字的属性

- 搜索首先从对象实例本身开始
- 如果在示例中找到了具有给定名字的属性，则返回该属性的值
- 如果没有找到，则继续搜索指针指向的原型对象，在原型对象中国查找具有给定名字的属性
- 如果在原型对象上找到了该属性，则返回该属性的值

总结：

1. 现在自己身上找，找到及返回
2. 自己身上找不到，则沿着原型链向上查找，找到即返回
3. 如果一直在原型链的末端还没有找到，则返回`null`

##### 实例对象写入原型对象成员

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
}

Person.prototype = {
  type: 'human',
  sayHello: function () {
    console.log('我叫' + this.name + '，我今年' + this.age + '岁了')
  }
}
```

该示例中，我们将`Person.prototype`重置到了一个新的对象。

这样为`Person.prototype`添加成员更简单了，但是同时原型对象丢失了`constructor`成员。

所以，为了保持`constructor`的指向正确，建议的写法是：

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
}

Person.prototype = {
  constructor: Person, // => 手动将 constructor 指向正确的构造函数
  type: 'human',
  sayHello: function () {
    console.log('我叫' + this.name + '，我今年' + this.age + '岁了')
  }
}
```

##### 原型对象使用建议

- 属性一般卸载构造函数内部

- 方法绑定在原型对象`prototype`上

- 一般在给`prototype`绑定完方法以后，再创建实例

- 如果对`prototype`进行了赋值，一定要修改`constructor`的指向，使其指回原来的构造函数

  ​

[![iT9vEd.md.png](https://s1.ax1x.com/2018/11/06/iT9vEd.md.png)](https://imgchr.com/i/iT9vEd)