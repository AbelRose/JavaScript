### JavaScript

- JavaScript是一种运行在***浏览器***中的***解释型***的编程语言.能够跨平台、跨浏览器驱动网页，与用户交互。

  通常我们都把JavaScript代码放到`<head>`中

  ```js
  <html>
      <head>
          <script>
              alert("Hello World !")
          </script>
      </head>
      <body>
          Hello World !
      </body>
  </html>
  ```

  或者使用.js的一个单独的文件

  ```js
  <head>
    <script src="/static/js/abc.js"></script>
  </head>
  ```

  JavaScript严格区分大小写，如果弄错了大小写，程序将报错或者运行不正常。

- 数据类型

  - Number: 不区分整数和浮点数(NaN无法计算结果时 Not a Number, Infinity 表示无限大)

  - 字符串: '' 或者 "" 

  - 布尔值: && || !

  - 比较运算符: 

    要特别注意相等运算符`==`。JavaScript在设计时，有两种比较运算符：

    第一种是`==`比较，它会***自动转换*** 数据类型再比较，很多时候，会得到***非常诡异*** 的结果；

    第二种是`===`比较，它***不会自动转换*** 数据类型，

    如果数据类型不一致，返回`false`，如果一致，再比较。

    由于JavaScript这个***设计缺陷***，*不要*使用`==`比较，***始终坚持使用`===`比较***。

    > 另一个例外是`NaN`这个特殊的Number与所有其他值都不相等，包括它自己：
    >
    > NaN === NaN; // false
    >
    > 唯一能判断`NaN`的方法是通过`isNaN()`函数：
    >
    > isNaN(NaN); // true

    注意浮点数的相等的比较

    1 / 3 === (1 - 2 / 3); // false 这个不是JS缺陷 而是在运算过程中 会产生误差

    要比较两个浮点数是否相等，只能计算它们之***差的绝对值***，看是否小于***某个阈值***：

    Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true

  - null 和 undefined

    `null`表示一个“空”的值，它和`0`以及空字符串`''`不同，`0`是一个***数值***，`''`表示***长度为0的字符串***，而`null`表示“空”。 大多数用null

    `undefined`，它表示“未定义”

  - 数组: JavaScript的数组可以包括任意数据类型. 创建数组可以用 new Array(1, 2, 3); 但是一般都直接用[] 

  - 对象: JavaScript的对象是一组由键-值组成的无序集合，例如：

    ```js
    var person = {
        name: 'Bob',
        age: 20,
        tags: ['js', 'web', 'mobile'],
        city: 'Beijing',
        hasCar: true,
        zipcode: null
    };
    ```

    键(又称对象的属性)都是字符串类型，值可以是任意数据类型。获取一个对象的属性 ***对象变量.数姓名***

- 变量

  - 在JavaScript中，使用等号`=`对变量进行赋值。可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量，但是要注意只能用`var`申明一次

    这种变量本身类型不固定的语言称之为***动态语言*** 。(Java 是静态语言)

  - strict 模式

    如果一个变量没有通过var声明就被使用 那么该变量就被声明为***全局变量*** 

    ```js
    i = 10; // i现在是全局变量
    ```

    使用`var`申明的变量则不是全局变量，它的范围被限制在该变量被申明的函数体内（函数的概念将稍后讲解），同名变量在不同的函数体内互不冲突。

    > 后续在ECMA的规范中推出了strict模式 当为使用var声明变量就使用的 将会导致运行错误.
    >
    > 启动strict 模式的方法是在JavaScript代码的第一行加上
    >
    > 'use strict';
    >
    > /* 这是一个字符串，不支持strict模式的浏览器会把它当做一个字符串语句执行，支持strict模式的浏览器将开启strict模式运行JavaScript */

- 字符串: 转义 \n表示换行 \t表示制表符 \本身也要转义 \\ 还可以表示ASCII码或者Unicode字符 多行字符串用反引号 `` 表示。

  > *需要特别注意的是*，字符串是不可变的(数组里的元素时可以变化的)，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果 
  >
  > ```js
  > <script>
  >             var s = 'Test';
  >             s[0] = 'X';
  >             alert(s); // s仍然为'Test'
  >         </script>
  > ```
  >
  > 

  模板字符串: 自动替换变量${} 

- 数组: *请注意*，直接给`Array`的`length`赋一个新的值会导致`Array`大小的变化：

  `Array`可以通过索引把对应的元素修改为新的值，因此，对`Array`的索引进行赋值会直接修改这个`Array`：

  >*请注意*，如果通过索引赋值时，索引超过了范围，同样会引起`Array`大小的变化
  >
  >还句话说, JavaScript 的数组是允许越界的 和很多其他语言不同

  *slice()方法: 如果里面什么都不传的话 就会从头到尾街区所有的元素，常用做**数组的复制***

  ```
  var arr = [1, 2, 3];
  var arr_copy = arr.slicr();
  ```

  push() 和 pop() 

  push(): 向Array() 的***末尾***添加若干元素 pop() 把Array() 的***末尾最后一个元素***抹掉

  ubshift() 和 shift()

  unshift() 向Array() 的***头部***添若干元素 shift() 向把***头部第一个元素***删掉

  splice() 是修改Array的***“万能方法“*** 从指定的索引开始删除若干元素，然后再从该位置添加若干元素：

  concat() 连接数组 并返回一个新的数组(并没有修改 ) 实际上，`concat()`方法可以接收任意个元素和`Array`，并且自动把`Array`拆开，然后全部添加到新的`Array`里

  join`join()`方法是一个非常实用的方法，它把当前`Array`的每个元素都***用指定的字符串连接***起来，然后返回连接后的字符串：

  ```
  var arr = ['A', 'B', 'C', 1, 2, 3];
  arr.join('-'); // 'A-B-C-1-2-3'
  ```

  如果`Array`的元素不是字符串，将***自动转换为字符串***后再连接。

- 对象: 一种无序的集合数据类型 由若干个键值对组成(用于描述现实世界的某个对象)

  用 var xxx {...} 表示 如果用到了属性 直接用xxx.属性名就可以了. 属性名都是字符串 属性的值可以是任意数据类型

  > 注意如果属性名 包含其他的特殊字符 就必须用''扩起来 用['属性名']来访问 xxx['属性名']

  检测对象是否含有某个属性，用in 操作符。 '属性名' in xxx 

  > 如果`in`判断一个属性存在，这个属性不一定是对象的，它可能是对象继承得到的
  >
  > 判断是否对象自身自带而不是继承的，用hasOwnProperty() 方法

- if判断

  如果`if`的条件判断语句结果不是`true`或`false`怎么办？例如：

  ```js
  var s = '123';
  if (s.length) { // 条件计算结果为3 不是0
      //
  }
  ```

  JavaScript把`null`、`undefined`、`0`、`NaN`和空字符串`''`视为`false`，其他值一概视为`true`，因此上述代码条件判断的结果是`true`。

- 循环

  for...in... 可以把一个对象的***所有属性***一次循环出来(若要滤掉继承的属性用hashOwnProperty())

  ```js
  for (var key in o) {
      if (o.hasOwnProperty(key)) {
          console.log(key); // 'name', 'age', 'city'
      }
  }
  ```

  > for...in... 对***Array***的循环得到的是***String***而不是Number

- Map 和 Set

  JavaScript的默认对象表示方式`{}`可以视为其他语言中的`Map`或`Dictionary`的数据结构，即一组键值对。

  但是他的***键必须是String***，但有时候要用到其他数据类型来表示键。引入了Map和Set的概念

  Map() 初始化Map() 需要一个***二维数组*** 或者直接初始化一个空的Map var map = ***new Map()***;

  Set() key不可以重复只存储key 不存value

- Iterable

  遍历Array可以采用下标循环 但是遍历Map和Set无法使用下标 通过***for...of*** 遍历

  `for ... of`循环和`for ... in`循环有何区别？

  for...in 遍历的是对象的属性名称 (Array其实也是一个对象)

  当我们手动给`Array`对象添加了额外的属性后，`for ... in`循环将带来意想不到的意外效果：

  ```js
  var a = ['A', 'B', 'C'];
  a.name = 'Hello';
  for (var x in a) {
      console.log(x); // '0', '1', '2', 'name'
  }
  ```

  for ... of 循环则完全修复了这些问题，它只循环集合本身的元素：

  ```js
  var a = ['A', 'B', 'C'];
  a.name = 'Hello';
  for (var x of a) {
      console.log(x); // 'A', 'B', 'C'
  }
  ```

  > 然而，更好的方式是直接使用`iterable`内置的`forEach`方法，它接收一个函数，每次迭代就自动回调该函数。以`Array`为例：
  >
  > ```js
  > 'use strict'; var a = ['A', 'B', 'C']; 
  > a.forEach(function (element, index, array) {
  >     // element: 指向当前元素的值
  >     // index: 指向当前索引
  >     // array: 指向Array对象本身
  >     console.log(element + ', index = ' + index);
  > });
  > ```

  如果对某些参数不感兴趣，由于JavaScript的函数调用不要求参数必须一致，因此可以忽略它们。

  例如，只需要获得`Array`的`element`：

  ```js
  var a = ['A', 'B', 'C'];
  a.forEach(function (element) {
      console.log(element);
  });
  ```

- 函数 

  抽象: 通过抽象 我们不关心底层的具体实现过程 直接在更高的层次上思考问题。

  函数也可以是一个对象 可以用匿名函数 var abs = function() {};

  > 在调用函数的时候 可以传入任意函数 而不影响使用。为了避免参数x收到undefined 使计算结果为NaN
  >
  > 可以进行检查 if (typeof x != 'number')...

  JavaScript还有一个免费赠送的关键字`arguments`，它只在函数内部起作用，并且永远指向当前函数的调用者传入的***所有参数***。`arguments`类似`Array`但它不是一个`Array`：

  利用arguments, 可以获得调用者传入的所有参数(即使函数不定义任何参数 还是可以拿到参数的值) 常用于判断传入参数的个数

  ```js
  if (arguments.length === 2) {...}
  ```

  rest参数 ES6后 函数可以写成 function foo (a, b, ...rest) {...}; 不需要arguments就可以得到全部参数了。多余的参数以数组的形式交给变量rest.

  JavaScript的函数在查找变量时从自身函数定义开始，***从“内”向“外”查找***。如果内部函数定义了与外部函数重名的变量，则内部函数的变量将***“屏蔽”***外部函数的变量。

  变量提升: JavaScript的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升”到函数顶部(即在顶部先声明)

  ```js
  'use strict';
  
  function foo() {
      var x = 'Hello, ' + y; // y 并不会报错 因为y在后面声明了
      console.log(x); // Hello, undefined
      var y = 'Bob';
  }
  
  foo();
  ```

  ```js
  function foo() {
      var y; // 提升变量y的申明，此时y为undefined
      var x = 'Hello, ' + y;
      console.log(x);
      y = 'Bob';
  }
  ```

  在函数内部应该声明所有的变量，常见的是用一个var 声明出所有的变量。

  全局作用域: 全局作用域的变量实际上被绑定到`window`的一个属性

  名字空间: 全局变量会绑定到`window`上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突，并且很难被发现。

  减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个***全局变量***(自己定义的)中

  ```js
  // 唯一的全局变量MYAPP:
  var MYAPP = {};
  
  // 其他变量:
  MYAPP.name = 'myapp';
  MYAPP.version = 1.0;
  
  // 其他函数:
  MYAPP.foo = function () {
      return 'foo';
  };
  ```

  把自己的代码全部放入唯一的名字空间MYAPP 会大大减少全局冲突的可能

  局部作用域: JS的变量作用域是函数内部 而语句块中是无法定义具有局部作用域的变量的 所以在ES6的时候新加了一个let关键字 可以声明一个块级别的变量

  常量: const  

  解构赋值: 同时对一组变量进行赋值(若从一个对象中取到若干属性也可使用 var{name, age, passport} = person) 使用场景是交换两个变量的值或者获取当前页面的域名和路径

- 方法: 绑定到对象的函数称为方法。

  > 用`var that = this;`，你就可以放心地在方法内部定义其他函数，而不是把所有语句都堆到一个方法中。
  >
  > 要***指定*** 函数的`this`指向哪个对象，可以用函数本身的`apply`方法，它接收两个参数，
  >
  > 第一个参数就是需要绑定的`this`变量，第二个参数是`Array`，表示函数本身的参数。
  >
  > 另一个与`apply()`类似的方法是`call()`，唯一区别是：
  >
  > - `apply()`把参数打包成`Array`再传入；
  > - `call()`把参数按顺序传入。

  装饰器; 利用apply() 还可以改变函数的行为。JavaScript的所有对象都是动态的 即使是内置的函数也可以重新指向新的函数

  现在假定我们想统计一下代码一共调用了多少次`parseInt()`，可以把所有的调用都找出来，然后手动加上`count += 1`，不过这样做太傻了。最佳方案是用我们自己的函数替换掉默认的`parseInt()`：

  ```js
  'use strict';
  
  var count = 0;
  var oldParseInt = parseInt; // 保存原函数
  
  window.parseInt = function () {
      count += 1;
      return oldParseInt.apply(null, arguments); // 调用原函数
  };
  ```

  ```js
  // 测试:
  parseInt('10');
  parseInt('20');
  parseInt('30');
  console.log('count = ' + count); // 3
  ```

- 高阶函数: JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么***一个函数就可以接收另一个函数作为参数***，这种函数就称之为高阶函数。

  map(): 定义在JavaScript的`Array`中，我们调用`Array`的`map()`方法，***传入***我们自己的***函数***，就得到了一个***新的Array***作为结果

  reduce: 把一个函数作用在这个`Array`的`[x1, x2, x3...]`上，这个函数必须***接收两个参数***，`reduce()`把结果继续和序列的下一个元素做***累积计算***。

- filter:  把`Array`的某些元素过滤掉，然后返回剩下的元素。`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`true`还是`false`决定保留还是丢弃该元素。filter()接收的回调函数，其实可以有多个参数。var r = arr.filter(function (element, index, self) 去重:     return self.indexOf(element) === index;

- sort:  和正常的排序不同.`Array`的`sort()`方法默认把所有元素先转换为String再排序，结果`'10'`排在了`'2'`的前面，因为字符`'1'`比字符`'2'`的ASCII码小。 `sort()`方法也是一个高阶函数，它还可以接收一个比较函数来实现自定义的排序。 

  ```js
  arr.sort(function (x, y) {
      if (x < y) {
          return -1; // 若是倒序的 则 return 1
      }
      if (x > y) {
          return 1;  // 若是倒序的 则 return -1
      }
      return 0;
  ```

  

  Array:  `every()`方法可以判断数组的所有元素是否满足测试条件。  

  ​		   `find()`方法用于查找符合条件的第一个元素，如果找到了，返回这个元素，否则，返回`undefined`： 

- 闭包: 函数作为返回值。

  ```js
  function lazy_sum(arr) {
      var sum = function () {
          return arr.reduce(function (x, y) {
              return x + y;
          });
      }
      return sum; // 返回的不是结果而是求和函数 当调用f()的时候才真正计算求和的结果
  }
  ```

  在这个例子中，我们在函数`lazy_sum`中又定义了函数`sum`，并且，内部函数`sum`可以引用外部函数`lazy_sum`的参数和局部变量，当`lazy_sum`返回函数`sum`时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。

  > 每次调用lazy_sum() 的时候 都会返回一个新的函数 (即使传入相同的参数)

  在没有`class`机制，只有函数的语言里，借助闭包，同样可以封装一个私有变量。我们用JavaScript创建一个计数器：

  ```js
  'use strict';
  
  function create_counter(initial) {
      var x = initial || 0;
      return {
          inc: function () {
              x += 1;
              return x;
          }
      }
  }
  ```

- 箭头函数 

  ```js
  x => x * x
  ```

  ```js
  x => { // 若是多个参数x, y 用(x, y) 括号括起来 
      if (x > 0) {
          return x * x;
      }
      else {
          return - x * x;
      }
  }
  ```

  > 箭头函数内部的`this`是词法作用域，由上下文确定。总是指向词法作用域，也就是调用者obj

- generator

  generator和函数不同的是，generator由`function*`定义（注意多出的`*`号），并且，除了`return`语句，还可以用`yield`返回多次。

  调用方法: var f = fib(); f.next(); 

  `next()`方法会执行generator的代码，然后，每次遇到`yield x;`就返回一个对象`{value: x, done: true/false}`，然后“暂停”。返回的`value`就是`yield`的返回值，`done`表示这个generator是否已经执行结束了。如果`done`为`true`，则`value`就是`return`的返回值。

  当执行到`done`为`true`时，这个generator对象就已经全部执行完毕，不要再继续调用`next()`了。

  调用方法: for...of 不需要自己判断done for( var x of fib(10)) {console.log(x);}
  
- 标准对象: 

  - Date: 

    1. JavaScript的Date对象月份值从0开始，牢记0=1月，1=2月，2=3月，……，11=12月。
    2. 使用Date.parse()时传入的字符串使用实际月份01~12，转换为Date对象后getMonth()获取的月份值为0~11。

  - RegExp 

    1. 用`\d`可以匹配一个数字，`\w`可以匹配一个字母或数字,

    2. `.`可以匹配***任意***字符, 用`*`表示***任意个***字符（包括0个）

    3. 用`+`表示至少一个字符，用`?`表示0个或1个字符，用`{n}`表示n个字符，用`{n,m}`表示n-m个字符

    4. `\s`可以匹配一个空格（也包括Tab等空白符），所以`\s+`表示至少有一个空格

    5. 特殊字符 用`\` 转义

    6. `[a-zA-Z\_\$][0-9a-zA-Z\_\$]{0, 19}`更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。

    7. `^`表示行的开头，`^\d`表示必须以数字开头。

       `$`表示行的结束，`\d$`表示必须以数字结束。

  - JSON

    1. JSON定死了字符集必须是UTF-8，表示多语言就没有问题了。为了统一解析，JSON的字符串规定必须用双引号`""`，Object的键也必须用双引号`""`

    2. 如果我们收到一个JSON格式的字符串，只需要把它反序列化成一个JavaScript对象，就可以在JavaScript中直接使用这个对象了。

    3. 序列化:

       要输出得好看一些，可以加上参数，按缩进输出：

       ```js
       JSON.stringify(xiaoming, null, '  ');
       ```

       ```js
       JSON.stringify(xiaoming, ['name', 'skills'], '  '); // 筛选指定属性
       ```

       ```js
       JSON.stringify(xiaoming, convert, '  '); // 还可以传一个函数 每次都县执行函数后再输出
       ```

    4. 反序列化:

       拿到一个JSON格式的字符串，我们直接用`JSON.parse()`把它变成一个JavaScript对象

- 面向对象编程

  类和实例是大多数面向对象编程语言的基本概念。不过，在JavaScript中，这个概念需要改一改。JavaScript不区分类和实例的概念，而是通过***原型（prototype）***来实现面向对象编程。

  ```js
  xiaoming.__proto__ = Student; // xiaoming 的原型指向了Student
  ```

  ![xiaoming-prototype](JavaScript.assets/l)

  JavaScript的***原型链***和Java的***Class***区别就在，它没有“Class”的概念，***所有对象都是实例***，所谓继承关系不过是把***一个对象***的原型指向***另一个对象***而已。

  > *请注意*，上述代码仅用于演示目的。在编写JavaScript代码时，不要直接用`obj.__proto__`去改变一个对象的原型
  >
  > `Object.create()`方法可以传入一个原型对象，并创建一个基于该原型的新对象，但是新对象什么属性都没有，因此，我们可以编写一个函数来创建`xiaoming`(函数里面有 Object.create(Student) 方法)

  - 创建对象

    JavaScript对每个创建的对象都会设置一个原型，指向它的原型对象。

    当我们用`obj.xxx`访问一个对象的属性时，JavaScript引擎先在***当前对象***上查找该属性，如果没有找到，就到***其原型对象***上找，如果还没有找到，就一直***上溯到`Object.prototype`对象***，最后，如果还没有找到，就只能返回`undefined`。

    > 注意: 不要把prototype 原型链搞得太长

    ```js
    function Student(name) {
        this.name = name;
        this.hello = function () {
            alert('Hello, ' + this.name + '!');
        }
    }
    ```

    如果不写new 这就是一个普通的函数 如果写了new 就会变成一个构造函数 并返回一个对象 。

    用`new Student()`创建的对象还从原型上获得了一个`constructor`属性，它指向函数`Student`本身

    ![protos](JavaScript.assets/l)

    `xiaoming`和`xiaohong`各自的`hello`是一个函数，但它们是两个不同的函数，虽然函数名称和代码都是相同的！ 把hello函数移动到这些对象的公共原型上就可以了(Student.prototype)

    ![protos2](JavaScript.assets/l)

    > 注意: 调用构造函数千万不要忘记写`new`。
    >
    > 为了区分普通函数和构造函数，按照约定，构造函数首字母应当大写，而普通函数首字母应当小写，这样，一些语法检查工具如[jslint](http://www.jslint.com/)将可以帮你检测到漏写的`new`。

    模板:

    ```js
    // 首字大写 表示一个构造函数
    function Student(props) {
        this.name = props.name || '匿名'; // 默认值为'匿名'
        this.grade = props.grade || 1; // 默认值为1
    }
    // 把共有共享方法提取到上一级的prototype
    Student.prototype.hello = function () {
        alert('Hello, ' + this.name + '!'); // 有的时候是return 
    };
    
    //封装所有的new方法 不需要new老调用
    function createStudent(props) {
        return new Student(props || {})
    }
    ```

  - 原型继承

    Student 扩展出 PrimaryStudent

    必须借助一个***中间对象来实现正确的原型链***，这个中间对象的原型要***指向***`Student.prototype`。为了实现这一点，参考***道爷***（就是发明JSON的那个道格拉斯）的代码，***中间对象***可以用一个***空函数`F`***来实现：

    ```js
    // PrimaryStudent构造函数:
    function PrimaryStudent(props) {
        Student.call(this, props);
        this.grade = props.grade || 1;
    }
    
    // 空函数F:
    function F() {
    }
    
    // 把F的原型指向Student.prototype:
    F.prototype = Student.prototype;
    
    // 把PrimaryStudent的原型指向一个新的F对象，F对象的原型正好指向Student.prototype:
    PrimaryStudent.prototype = new F();
    
    // 把PrimaryStudent原型的构造函数修复为PrimaryStudent:
    PrimaryStudent.prototype.constructor = PrimaryStudent;
    
    // 继续在PrimaryStudent原型（就是new F()对象）上定义方法：
    PrimaryStudent.prototype.getGrade = function () {
        return this.grade;
    };
    
    // 创建xiaoming:
    var xiaoming = new PrimaryStudent({
        name: '小明',
        grade: 2
    });
    xiaoming.name; // '小明'
    xiaoming.grade; // 2
    
    // 验证原型:
    xiaoming.__proto__ === PrimaryStudent.prototype; // true
    xiaoming.__proto__.__proto__ === Student.prototype; // true
    
    // 验证继承关系:
    xiaoming instanceof PrimaryStudent; // true
    xiaoming instanceof Student; // true
    ```

    ![js-proto-extend](JavaScript.assets/l)

    如果把继承这个动作用一个`inherits()`函数封装起来，还可以隐藏`F`的定义，并简化代码：

    ```js
    function inherits(Child, Parent) {
        var F = function () {};
        F.prototype = Parent.prototype;
        Child.prototype = new F();
        Child.prototype.constructor = Child;
    }
    ```

    小结

    JavaScript的原型继承实现方式就是：

    1. 定义新的构造函数，并在内部用`call()`调用希望“继承”的构造函数，并绑定`this`；
    2. 借助中间函数`F`实现原型链继承，最好通过封装的`inherits`函数完成；
    3. 继续在新的构造函数的原型上定义新方法。

  - class继承

    新的关键字`class`从ES6开始正式被引入到JavaScript中。`class`的目的就是让定义类更简单。(注意没有function关键字)

    ```js
    class Student {
        constructor(name) {
            this.name = name;
        }
    
        hello() {
            alert('Hello, ' + this.name + '!');
        }
    }
    ```

    有extend关键字

    ```js
    class PrimaryStudent extends Student {
        constructor(name, grade) {
            super(name); // 需要通过super(name)来调用父类的构造函数，否则父类的name属性无法正常初始化。
            this.grade = grade;
        }
    
        myGrade() {
            alert('I am at grade ' + this.grade);
        }
    }
    ```

- 浏览器: 

  - AJAX: Asynchronous JavaScript and XML-  JavaScript执行异步网络请求

    如果要让用户留在当前页面中，同时发出新的HTTP请求，就必须用JavaScript发送这个新请求，接收到数据后，再用JavaScript更新页面，这样一来，用户就感觉自己仍然停留在当前页面，但是数据却可以不断地更新。

    当创建了`XMLHttpRequest`对象后，要先设置`onreadystatechange`的回调函数。在回调函数中，通常我们只需通过`readyState === 4`判断请求是否完成，如果已完成，再根据`status === 200`判断是否是一个成功的响应。

  - CORS: 全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。

    会检查 Access-Control-Allow-Origin

    ![js-cors](https://www.liaoxuefeng.com/files/attachments/1027024093709472/l)

- jQuery ("Write Less, Do More")

  - 消除浏览器差异
  - 简洁的操作DOM的方法 
  - 轻松实现动画、修改CSS等各种操作

  符号

  - $ 是jQuery的别名.本质上就是一个函数也是对象(除了直接调用外 还有很多的其他属性)

    注意: 当发生占用的时候 

    ```js
    $; // jQuery(selector, context)
    jQuery.noConflict();
    $; // undefined
    jQuery; // jQuery(selector, context)
    ```

  选择器 (快速定位到一个或者多个DOM节点)   ==**$('#dom-id')**==

  ​	按ID查找: $('#DOM节点的id')

  ​    按照tag查找: $('tag名')

  ​	按照class查找: $('.class名') (可以多个查找直接用.连起来)

  ​	按照属性查找: $('[name=email]')

  - 层级选择器 (Descendant Selector)

    如果两个DOM 元素具有层级关系, 就可以用**$('ancestor descendant')** 来选择, 层级间用空格隔开

  - 子选择器(Child Selector) 

    子选择器**`$('parent>child')`**类似层级选择器，但是限定了层级关系必须是父子关系，就是`<child>`节点必须是`<parent>`节点的直属子节点。

  - 查找和过滤

    find() 方法: 在某个结点的所有子字节点中查找。若要从某个结点的上一层结点查找 用parent()方法。对于位于同一层的节点, 用nex() 和 prev() 方法

    filter() 方法: 可以过滤调不符合选择条件的节点.

  - 操作DOM

    jQuery对象的`text()`和`html()`方法分别获取**节点**的文本和**原始**HTML文本(或者append()方法)

    > **无参**数调用`text()`是**获取**文本，**传入**参数就变成**设置**文本，HTML也是类似操作

    显示和隐藏DOM元素，jQuery直接提供`show()`和`hide()`方法

    `attr()`和`removeAttr()`方法用于操作DOM节点的属性

    对于表单元素，jQuery对象统一提供`val()`方法获取和设置对应的`value`属性

  - 事件

    `on`方法用来绑定一个事件，我们需要传入事件名称和对应的处理函数。

    鼠标事件: 键盘事件: 

    其他事件: (有一个ready()事件 使用较多)

    ```js
    $(document).ready(function () {
        // on('submit', function)也可以简化:
        $('#testForm).submit(function () {
            alert('submit!');
        });
    });
    ```
  
    甚至可以是
  
    ```js
    // document对象的ready事件处理函数。
    $(function () {
        // init...
    });
    ```
  
    事件参数: mousemove`和`keypress 事件可以绑定到Event上作为参数 
  
    取消绑定: off('click', function) 
  
    事件触发条件: `change`事件
  
    
  
  - 动画
  
    show() / hide() / toggle()
  
    > toggle根据当前状态决定是show还是hide
  
    slideUp() / slideDown() / slideToggle() 
  
    > 这个垂直方向的
  
    fadeIn() / fadeOut() / fadeToggle()
  
    > 淡入淡出效果
  
    奥义: animate()
  
    ```js
    var div = $('#test-animate');
    div.animate({
        opacity: 0.25,
        width: '256px',
        height: '256px'
    }, 3000, function () {
        console.log('动画已结束');
        // 恢复至初始状态:
        $(this).css('opacity', '1.0').css('width', '128px').css('height', '128px');
    });
    ```
  
    串行动画: delay() 
  
    > 更复杂的动画效果
  
    
  
  - AJAX
  
    `ajax(url, settings)`函数需要接收一个URL和一个可选的 `settings`对象
  
    > 分别是:async, method, contentType, data, headers, dataType
  
    get $.get() 
  
    post: $.post()
  
    getJSON(): $.getJSON()
  
    
  
- 错误处理

- underscore

- Node.js

- React











































































