#### 1.window对象

##### Window 对象表示浏览器中打开的窗口,是客户端js中最高层对象之一。

##### Window 对象是全局对象,要引用当前窗口根本不需要特殊的语法，可以把那个窗口的属性作为全局变量来使用。例如，可以只写 [document](http://www.w3school.com.cn/jsref/dom_obj_document.asp)，而不必写 window.document 。同样，可以把当前窗口对象的方法当作函数来使用，如只写 alert()，而不必写 Window.alert() 。

##### window对象何时创建：

##### 当浏览器打开窗口时，无论该窗口是否打开了网页，当遇到了body或者frameset或者frame元素时都会创建一个window对象。



#### 2.ES6中的箭头函数

```js
#当函数体中只有一句的时候可以省略大括号
<script type="text/javascript">
var sum = (a,b) => a*b;
alert(sum(5,7));
#等价于：
var sum = (a,b) => {
    return a*b;
}
alert(sum(5,7));

</script>
```

##### 	上面的箭头函数等价于：

``` js
<script type="text/javascript">
var sum = function (a,b) {
        return a*b;
    }
alert(sum(5,7));
</script>
```



#### 3.js中的普通对象

普通对象一般由{}括起来，里面是一些以**键值对**形式出现的属性和方法。

##### 例子：

```js
var obj = {
    a:10,
    b:"我是字符串",
    testFunction:function(){
        console.log("我是一个obj对象中的testFunction方法");
    }
}
```

##### 以上定义了一个obj变量，该变量指向一个普通对象（或者可以说obj就是一个对象），该对象中有两个属性a和b，它们的值分别是10和“我是字符串”，还有一个testFunction方法。



#### 4.this关键字

##### this指的是当前对象的引用。

例子：该例子中有一个“this作用域”的问题

``` js
var obj = {
        a:10,
        func:function () {
            alert(this.a);
        },
        test:function () {
            alert("obj的this："+this);
            var that = this;//1.此处将obj对象赋给that变量
            window.setTimeout(function () {
                alert("setTimeout的this："+this);
                //this.func(); //因为此处的this是window对象，所以不能够调用obj对象的func方法
                that.func();//2.此处就可以利用指向obj对象的that变量来调用func方法了
            },1000);
        }
    }
    obj.test();
```

利用箭头函数简化上面的"this作用域的问题"

##### 箭头函数中的this是它上一层函数（方法）所属于的对象的引用

``` js
var obj = {
        a:20,
        func:function () {
            alert(this.a);
        },
        test:function () {
            alert("obj中的this对象："+this);
            window.setTimeout(()=>{
                this.func();
            },1000);
        }
    }
```



##### 说明：换成箭头函数后，就可以直接使用this关键来调用obj的fanc方法了，因为此时的this（箭头函数中的this）是它上一层函数（方法）所属于的对象的引用，也就是test函数（方法）所属于的对象是obj对象。

