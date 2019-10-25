---
title: "My First Post"
date: 2019-10-24T21:59:38+08:00
draft: true
---


一. mixin

听起来是个很「高大上」的新功能，但是。。。。其实就是为了把「对象a」的所有属性，复制一份到「对象b」中。

function mixin(a, b) {
  for(let key in a) {
    b[key] = a[key];
  }
}
其实就是这么简单的代码。现在ES6语法中有更简单的方式。

Object.assign(b, a);
二. 柯里化

我们说「函数」的时候，一般是「x -> y」的映射，两个参数时，「(x, y) -> z」。

比如:

f(x, y) = x + 2*y;
// 我们固定x，设x=1；
f(1, y) = 1 + 2*y = g(y)
上面这个过程就是「柯里化」。注：不一定只有x，y两个参数，可以是多个参数，然后固定其中一个就可以。

一些应用：

var sum = 0;

function add(x) {
    if(x === undefined) {
        return sum;
    } else {
        console.log('x', x)
        sum += x;
        console.log('sum', sum)
        return add;
    }
}


add(1)(2)(3)();  // 6, 结果在sum中
var result = 0;

function sum(...args) {
    if(args.length === 0) {
        return result;
    } else {
        args.map(v => {
            result += v;
        });
        return sum;
    }

}

sum(1,2,3)  // 6

sum(1)(2)(3)  // 6

sum(1,2)(3)  // 6  都存在result变量中
三. 高阶函数
至少满足以下一个条件，即为「高阶函数」。

接受一个或者多个函数作为输入
输出一个函数
举例：

function add(x, y) {
    return x + y;
}


let f = Function.prototype.bind.call(add, undefined, 1);

// 等价于
// let f = add.bind(undefined, 1);
上述中，bind的参数中其实就有「函数」。

0人点赞
Javascript


作者：Jason_Shu
链接：<a href='https://www.jianshu.com/p/0773b86e5193'>https://www.jianshu.com/p/0773b86e5193</a>
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。