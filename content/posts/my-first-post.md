---
title: "My First Post"
date: 2019-10-22T21:59:38+08:00
draft: true
---

我的第一篇博客
原生JS实现抽奖
```
var playBtn = document.getElementById('play');
// 获取所有td元素，获取到伪数组
var tdAry = document.getElementsByTagName('td');
// 将伪数组的长度存储在tdLen变量中
var tdLen = tdAry.length;
// 设置计时器变量，刚开始为空
var startTime = null;
// 自己构造数组，使橘红色背景能够按照自己想要的方向进行循环移动
var tdList = [0, 1, 2, 4, 7, 6, 5, 3];
// 设置橘红色背景标识
var tdId = 0;
// 设置已经奔跑的次数，刚开始为0次
var time = 0;
// 固定跑3圈，一圈8次
var fixNum = 24
// 定义最大随机数
var MaxNum;
// 定义随机数，开始和结束的阈值
var randomNum;
// 获取中奖结果元素
var results = document.getElementsByClassName('results')[0];
 
// 绑定点击事件，当鼠标点击开始按钮后，触发playStart函数
playBtn.onclick = playStart;
 
function playStart() {
    // 如果计时器不为空，那就意味着这个线程已经在跑了，就直接退出。
    if (startTime != null) {
        return;
    }
    results.style.display = 'none';
    // 奔跑的次数
    time = 0;
    // 最大随机数，取值[0, 8]，确保每个都能被选到
    MaxNum = parseInt(Math.random() * 9) + fixNum;
    // 随机阈值，控制刚开始跑几步加速，以及剩几步减速，取值范围[3, 7]
    randomNum = parseInt(Math.random() * 5 + 3);
    // 开启计时器，每200毫秒执行一次move函数
    startTime = setInterval(move,200);
 
}
 
function move() {
    // 每执行一次奔跑次数time就加1
    time++;
    // 每次运行当前的背景色清空
    tdAry[tdList[tdId]].className = "";
    // 每执行一次背景色标识就加1
    tdId++;
    // 判断如果标识大于7的话就标识tdId就等于0，否则的话就等于它本身，这个步骤如果没有进行判断和赋值的话，tdId就会一直自增下去，那么对应的td元素将没有，后台就会报错
    tdId = tdId > 7 ? 0 : tdId;
    // 设置当前的td背景色
    tdAry[tdList[tdId]].className = "active";
 
    //如果奔跑的次数等于随机阈值的话，那么当前的计时器清空，重新开启一个新的计时器，并且是每20毫秒执行一次，这个步骤是控制加速的
    if (time == randomNum) {
        clearInterval(startTime);
        startTime = setInterval(move,20);
    }
 
    // 如果奔跑的次数加上随机的阈值的话，那么就将当前的加速的计时器清空，并且重新开启一个每200毫秒的计时器，这个步骤是控制减速的
    if (time + randomNum >= MaxNum) {
        clearInterval(startTime);
        startTime = setInterval(move,200);
    }
 
    // 如果奔跑的次数大于等于最大的奔跑次数，那么清空当前计时器，并且计时器等于null，直接返回出去，一次抽奖结束。这个步骤是控制抽奖结束。
    if (time >= MaxNum) {
        clearInterval(startTime);
        startTime = null;
        // switch语句判断抽奖结果，这部分比较简单，就不赘述了。
        switch(tdList[tdId]) {
            case 0:
                results.innerText = '今天吃转转乐';
                results.style.display = 'block';
                break;
            case 1:
                results.innerText = '今天吃蜀九香';
                results.style.display = 'block';
                break;
            case 2:
                results.innerText = '今天吃KFC';
                results.style.display = 'block';
                break;
            case 4:
                results.innerText = '今天吃海底捞';
                results.style.display = 'block';
                break;
            case 7:
                results.innerText = '今天吃外卖';
                results.style.display = 'block';
                break;
            case 6:
                results.innerText = '今天吃土';
                results.style.display = 'block';
                break;
            case 5:
                results.innerText = '今天吃牛排';
                results.style.display = 'block';
                break;
            case 3:
                results.innerText = '今天吃草本汤';
                results.style.display = 'block';
                break;
        }
        return;
    }
 
}

```