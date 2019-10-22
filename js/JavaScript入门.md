# JavaScript入门

###　JavaScript简史

JavaScript诞生于1995年，当时就职于 Netscape 公司的布兰登·艾奇(Brendan Eich),开始着手为计划于 1995 年 2 月发布的Netscape Navigator 2 开发一种名为**LiveScript ** 的脚本语言。Netscape 为搭上媒体热炒 Java 的顺风车,临时把 LiveScript 改名为 JavaScript。

所以其实JavaScript与Java并没有任何关系。



### 语法

#### 申明变量var

```javascript
var test ;
var Test;   // 在JavaScript中是区别大小写的，比如这里的test和Test是两个不同的变量定义变量时使用var操作符

var 　message ;   /*
                                      *这代码定义了一个message变量,这个变量可以用来保存任何值(向这样未被初始化的变量，保存一个特                                       *殊的值　--- undefined)
                                      */

var  message = 'hello world'   //也可以直接在定义是进行初始化操作

```

####　打印变量console.log

```javascript
var message = 'hello world'
console.log(message)
```

### 数据类型

#### 基本类型 

- Undefined

- NUll
- Boolean
- Number
- String

在JavaScript中提供了检查变量数据类型的方法为 --- typeof 

```javascript
var test = 'hello world'
typeof test

var message = 123
typeof message
```

##### Undefined

Undefined 类型只有一个值,即特殊的 undefined 。在使用 var 声明变量但未对其加以初始化时,
这个变量的值就是 undefined。

```javascript
var test
console.log( test == undefined )
```

##### Null

Null也是只有一个值的数据类型，即特殊的Null。

##### Boolean

该类型有两个字面值：true 和 false  , 由于JavaScript中是区别大小写的，所以True 和False并非属于Boolean类型。

所有类型的值都有与这两个 Boolean 值等价的值,通过Boolean()来转换。

```                     javascript
var  test = 'hello world'
Boolean(test)

var a = undefined
Boolean(a)
```

##### Number

1.浮点数值

所谓浮点数值,就是该数值中必须包含一个小数点,并且小数点后面必须至少有一位数字。虽然小
数点前面可以没有整数,但我们不推荐这种写法

```javascript
var floatNum1 = 1.1;
var floatNum2 = 0.1;
var floatNum3 = .1;

console.log(floatNum1)
console.log(floatNum2)
console.log(floatNum3)
```

因为浮点数保存的空间是整数保存空间的两倍。所以js会在尽可能的机会将浮点数转化为整形数。比如：

```javascript
var test = 10.0 
console.log(test)
```

2.NaN

NaN(not a number)是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作数
未返回数值的情况(这样就不会抛出错误了)。

例如：

```javascript
var test = 0 / 0 
console.log(test)
```

任何涉及到NAN的操作都会返回NAN , 例如:

```javascript
var test = NaN / 10
console.log(test)
```

NaN与任何值都不相等

```javascript
console.log(NaN == 10)
console.log(NaN == NaN)
```

既然NaN连自己等于自己不相等，那如何进行判断一个数据是否为NaN呢。js中提供了isNaN()的方法进行相应的判断。

```javascript
console.log(isNaN(NaN))
console.log(isNaN(12))
```

３.数值转换

- Number()         用于任何数据
- parseInt()         只用于将字符串
- parseFloat()　只用于字符串

```javascript
console.log(Number(true))
console.log(Number(false))

console.log(parseInt('23B'))

console.log(parseInt('23.12'))
console.log(parseFloat('23.12'))

```

##### String

字符串可以由双引号(")或单引号(')表示

```javascript
var  str1 = 'hello'
var  str2 = "world"

//模板字符串
var str = `我是${str2}`

console.log(str)
```

字符串操作:

**concat()**  用来讲一个或者多个字符串与原字符串进行拼接，返回一个新的字符串

```javascript
var  str1 = 'hello'
var  str2 = "world"

var str = str1.concat(str2)
console.log(str)
//字符串拼接还可以直接使用
console.log(str1+str2)
```

**indexOf()**  方法返回调用对象中第一次出现指定值的索引

```javascript
var str = 'blue sky'
console.log(str.indexOf('blue'))
console.log(str.indexOf('Blue'))
```

**includes()** 方法用于判断一个字符串是否包含在另一个字符串中，根据情况返回 true 或 false。

```javascript
var str = 'blue sky'
console.log(str.includes('blue'))
console.log(str.includes('Blue'))
```

**replace()** 方法返回一个由替换值替换一些或所有匹配的模式后的新字符串

#### 引用类型

- Object(对象)
- Array(数组)
- Function(函数)

##### Object

```javascript
//创建Object的方式有两种　
//第一种
var obj = new Object()
obj.name = "hello"
obj.year = 20

//第二种
var obj = {
    name : 'hello',
    year : 20
}

//取出对象中的属性方法也有两种
//第一种
console.log(obj.name)
//第二种
console.log(obj['year'])
```

##### Array

数组是数据的有向序列。但是数组的每一项都可以保存任何类型的数据。数组的大小是可以动态调整的,即可以随着数据的添加自动增长以容纳新增数据。

在读取和设置数组的值时,要使用方括号并提供相应值的基于 0 的数字索引

``` javascript
var arr = ['1' , 1 , true , {name : 'test'}]

arr[0]      //'1'
arr[1]      //1
arr[2]     // true
arr[3]     // {name : 'test'}

console.log(arr.length)             //获得长度

//遍历数组
for (var i = 0 ; i < arr.length ; i++){
    cosole.log(arr[i])
}

for(var item in arr){
    console.log(arr[item])
}

for(var item of arr){
    console.log(item)
}
```

**数组的操作**

判断是否为数组Array.isarray()

```javascript
var arr = ['1' , 1 , true , {name : 'test'}] 
Array.isArray(arr)                                   //true
```

push()与unshift()

虽然这两个函数都是对数组进行插入操作，但是这两个函数的插入操作是相反的。push()是在数组后面插入，unshift()是在数组前面进行插入。并返回该数组的新长度。

```javascript
var arr = ['1' , 1 , true , {name : 'test'}] 

arr.push('behide')
arr.unshift('font')

console.log(arr)        //["font", "1", 1, true, {…}, "behide"]
```

pop()与shift()

这两个函数都是对数组进行相关的删除操作，前面的出入操作相对应，pop()删除数组中的最后一个元素,shift()删除数组的第一个元素，并返回该元素的值，都会改变数组的长度。

```javascript
var arr = ['1' , 1 , true , {name : 'test'}] 

arr.pop()        // arr :  ["1", 1, true]

arr.shift()      //arr:  [1, true]
```

