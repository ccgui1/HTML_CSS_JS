# 1.定位
## 1.1 为什么需要定位
1. 浮动可以让 多个块级盒子一行没有缝隙排列显示，经常用于横向排列盒子。
2. 定位则是可以让盒子自由的在某个盒子内移动位置或者固定屏幕中某个位置，并且可以压住其他盒子。
   

## 1.2 定位组成
定位： 将盒子定在某个位置，所以定位也是在摆放盒子，按照定位的方式移动盒子。   
- 定位 = 定位模式  + 边偏移

1. 定位模式
定位模式决定元素的定位模式，它通过CSS的position属性来设置，其值可以分为四个。

| 值     |     语义    |
| :----- |  :---------|
| static  | 静态定位    |
| relative | 相对定位   |
| absolute | 绝对定位   | 
| fixed    |  固定定位  |


2. 边偏移
边偏移就是定位的盒子移动到最终位置，有top,bottom,left和right4个属性。

|边偏移属性  |  示例     | 描述    |
|:----------|:----------|:--------|
|top      | top: 80px    |顶端偏移量，定义元素相对于其父元素上边线的距离|
|bottom   | bottom: 80px | 底部偏移量，定义元素相对于其父元素下边距的距离  |
| left   | left: 80px  | 左侧偏移量，定义元素相对于其父元素左边线的距离  |
| right  | right: 80px | 右侧偏移量，定义元素相对于其父元素的右边线的距离  |

## 1.3 静态定位(static)了解
静态定位是元素的默认定位方式，无定位的意思。    
语法： 
```CSS
选择器 { position: static; }
```
- 静态定位按照标准流特性摆放位置，它没有边偏移。
- 静态定位在布局时很少用到。


## 1.4 相对定位 relative（重要）
相对定位是元素在移动位置的时候，是相对于它原来的位置来说。    
语法：
```css
选择器 { position: relative; }
```
相对定位的特点:
- 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置）
- 原来在标准流的位置继续占有，后面的盒子仍然以标准流的方式对待它。（不脱标，继续保留原来位置）
因此，相对定位并没有脱标，它最典型的应用就是给绝对定位当爹。

## 1.5 绝对定位absolute（重要）
绝对定位是在元素在移动位子的时候，是相对于祖先元素来说的（拼爹型）   
语法： 
```css
选择器 { position: absolute; }
```
绝对定位的特点：
- 如果没有祖先元素或者祖先元素没有定位，则以浏览器为准定位。
- 如果祖先元素有定位（相对，绝对，固定定位），**则以最近一级的有定位祖先元素为参考点移动位置。**

##  1.6 子绝父相
子级是绝对定位的话，父级要用相对定位。

- 子级绝对定位，不会占有位置，可以放到父盒子里面的任何一个地方，不会影响其他的兄弟盒子。
- 父盒子需要加定位限制子盒子在父盒子内显示。
- 父盒子布局时，需要占有位置，因此父亲只能是相对定位。
  
hot案例
- HTML代码
```html
        <div class="box_bd">
            <ul class="clearfix">
                <li>
                    <a href="#">
                        <img src="images/pct1.png" alt="">
                        <p> Think PHP 5.0 博客系统实战项目演练</p>        
                    </a> 
                    <span class="level">高级</span>
                     <span>•</span> 
                    <span class="people_num">1125人在学习</span>
             <!-- hot模块图片-->
                    <em class="hot">
                         <img src="images/hot1.png" alt="">
                    </em>
                </li>
                <li
```

- 对应CSS代码
```css
/*父元素使用相对定位*/
.box_bd ul li {
    position: relative;
}

/*子元素使用相对定位*/
.hot{
   position: absolute;
   top: 0px;
   right: -4px;

}
```

## 1.7 固定定位
固定定位是元素固定于浏览器可视区的位置，主要使用场景：可以在浏览器页面滚动时元素的位置不会变。    
语法：
```js
选择器 { position: fixed; }
```
固定定位的特点：（务必记住）
1. 以浏览器的可视窗口参照点移动元素。 
- 跟父元素没有任何关系
- 不随滚条滚动

2. 固定定位不占用原先的位置。
   固定定位也是脱标的，其实固定定位也可以看做是一种特殊的绝对定位。

### 1.7.1 固定小技巧
- 固定在版心右侧位置
  小算法
  1. 让固定定位的盒子left: 50%  走到浏览器可视区（也可以看做版心）的一半位置。
  2. 让固定定位的盒子margin-left: 版心宽度的一半距离。多走版心宽度的一半位置。

代码参考
```html
    <style>
       .w {
           width: 800px;
           height: 1400px;
           background-color: pink;
           margin: 0 auto;
       }

       .fixed {
           position: fixed;
           /* 版心高度一半 */
           left: 50%;
           /* 版心宽度一半 ，如果为了留有空隙可以多几个像素*/
           margin-left: 420px;
           width: 50px;
           height: 150px;
           background-color: skyblue;
       }
    </style>

</head>
<body>
    <div class="fixed"></div>
    <div class="w">版心盒子</div>
</body>
```

### 1.8 粘性定位（了解）
粘性定位可以被认为是相对定位和固定定位的混合。Sticky粘性的。
语法：
```CSS
选择器 { position: sticky; top: 10px;}
```

粘性定位的特点
- 以浏览器的可视窗口位参照点移动元素（固定定位特点）
- 粘性定位占有原先的位置（相对定位特点）
- 必须添加top, left, right, bottom其中一个才有效。    

\
代码参考
```html
    <style>
        body {
            height: 3000px;
        }

       .nav {
          position: sticky;
          /* 当导航栏距离10像素时，就不在发生变动 */
          top: 10px;
          width: 800px;
          height: 50px;
          background-color: pink;
          margin: 100px auto;
       }
    </style>

</head>
<body>
    <div class="nav">我是导航栏</div>
</body>
```
注意：跟页面滚动搭配使用，兼容性较差，IE不支持。

## 1.8 定位叠放次序 z-index
在使用定位布局时，可能会出现盒子重叠的情况。此时，可以使用z-index来控制盒子的前后次序（z轴）   

\
语法:
```CSS
选择器 { z-index: 1;}
```

- 数值可以是正整数，负整数，默认是auto,数值越大，盒子越靠上。
- 如果属性值相同，则按照书写顺序，后来居上。
- 数字后面不能加单位。
- 只有定位的

示例代码
```html
    <style>
        .box {
            position: absolute;
            top:0px;
            height: 200px;
            width: 200px;
        }

        .xiongda {
            background-color: red;
            z-index: 999;
        }

        .xionger {
            background-color: green;
        }

        .qiangge {
            background-color: blue;
        }
    </style>

</head>
<body>
    <div class="box xiongda">熊大</div>
    <div class="box xionger">熊二</div>
    <div class="box qiangge">光头强</div>

</body>
```

## 1.9 定位的扩展。
### 1.9.1 绝对定位的盒子居中
加了绝对定位的盒子不能通过margin: 0 auto水平居中，但是可以通过以下计算方法实现水平和垂直居中。
- left:50%; 让盒子的左侧移动到父级元素水平中心位置
- margin-left: -100px; 让盒子向左移动自身宽度的一半。

垂直居中类似： 可以走top的一半，然后往上走margin-top：自身的高度的一半。
### 1.9.2 定位特殊性
绝对定位和固定定位也会浮动类似
1. 行内元素添加绝对或者固定定位，可以直接设置高度和宽度。
2. 块级元素添加绝对或者固定定位，如果不给宽度或者高度，默认大小是内容的大小。
3. 脱标的盒子不会触发外边距塌陷。（浮动元素、绝对定位,固定定位元素都不会触发外边距合并的问题。）



