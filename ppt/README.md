### How to use

```
npm install nodeppt -g
nodeppt start
```

### 样式属性

```html
<span class="text-danger">.text-danger</span> <span class="text-success">.text-success</span><span class="text-primary">.text-primary</span>

<span class="text-warning">.text-warning</span><span class="text-info">.text-info</span><span class="text-white">.text-white</span><span class="text-dark">.text-dark</span>


<span class="blue">.blue</span><span class="blue2">.blue2</span><span class="blue3">.blue3</span><span class="gray">.gray</span><span class="gray2">.gray2</span><span class="gray3">.gray3</span>

<span class="red">.red</span><span class="red2">.red2</span><span class="red3">.red3</span>

<span class="yellow">.yellow</span><span class="yellow2">.yellow2</span><span class="yellow3">.yellow3</span><span class="green">.green</span><span class="green2">.green2</span><span class="green3">.green3</span>
```

### label and link

```html
<span class="label label-primary">.label.label-primary</span><span class="label label-warning">.label.label-warning</span><span class="label label-danger">.label.label-danger</span><span class="label label-default">.label.label-default</span><span class="label label-success">.label.label-success</span><span class="label label-info">.label.label-info</span>

<a href="#">link style</a> <mark>mark</mark>
```

### blockquote

和引用相关的 api

> nodeppt可能是迄今为止最好用的web presentation <small>三水清</small>

下面是另外一种样式

> 这是一个class是：pull-right的blockquote <small>small一下</small> {:&.pull-right}

### 图案

```html
<i class="fa fa-github"></i>
```

### 支持 HTML 和 markdown 语法混编
----

<div class="file-setting">
    <p>这是html</p>
</div>
<p id="css-demo">这是css样式</p>
<p>将html代码直接混编到**markdown**文件中即可</p>

我是js控制的颜色 black {:#testScriptTag}

<script>
    function testScriptTag(){
        document.getElementById('testScriptTag').style.color = 'black';
    }

</script>
<style>
#css-demo{
    color: red;
}
</style>

### 使用overview模式
---
按下键盘【O】键。看下效果。

在overview模式下，方向键下一页，【enter】键进入选中页

或者按下键盘【O】键，退出overview模式

### 宽度不够？？
---
按下键盘【W】键，切换到更宽的页面看效果，第二次按键返回

### 使用画笔
---
按下键盘【P】键：按下鼠标左键，在此处乱花下看看效果。

按下键盘【B/Y/R/G/M】：更换颜色，按下【1~4】：更换粗细

按下键盘【C】键：清空画板

### 图片动效

[magic data-transition="cover-circle"]
![](/girl.jpg)
====
![](/girl.jpg)
[/magic]

> [magic](https://github.com/ksky521/nodeppt/blob/master/README.md#magic)

### 动效
----
* 列表支持渐显动效哦 {:&.动效类型}
    * 使用方法 markdown 列表第一条加上
* 动效类型
    * fadeIn
    * rollIn
    * bounceIn
    * moveIn
    * zoomIn

### 背景动效
----
* kontext
* vkontext
* circle
* earthquake
* cards(可以)
* glue
* stick(可以)
* move(可以)
* newspaper(这个不错)
* slide
* slide2
* slide3
* horizontal3d
* horizontal
* vertical3d
* zoomin
* zoomout
* pulse

## 快速翻页
----
1. 输入页码，然后enter
2. 使用O键，开启纵览模式，然后翻页

## 动效样式强调
----

这段话里面的**加粗**和*em*字体会动效哦~

按下【H】键查看效果

## 支持zoom.js
----

增加了zoom.js的支持，在演示过程中使用`alt`+鼠标点击，则点击的地方就开始放大，再次`alt+click`则回复原状

## 笔记

[note]
##这里是note

使用n键，才能显示
[/note]