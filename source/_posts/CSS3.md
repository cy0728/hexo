---
date: 2019-07-26
cover: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1588051543473&di=67f191093aa1a813125aa3036b4aaf85&imgtype=0&src=http%3A%2F%2Fimg0.imgtn.bdimg.com%2Fit%2Fu%3D2340366615%2C2853341379%26fm%3D214%26gp%3D0.jpg
---

# CSS3简介

>  如同人类的的进化一样，CSS3是CSS2的“进化”版本，在CSS2基础上，**增强** 或**新增** 了许多特性， 弥补了CSS2的众多不足之处，使得Web开发变得更为高效和便捷。 

## CSS3的现状

- PC端浏览器支持程度差，需要添加私有前缀
- 移动端支持优于PC端
- 不断改进中
- 应用相对广泛

关于私有前缀：

> 在标准还未确定时，部分浏览器已经根据最初草案实现了部分功能，为了与之后确定下来的标准进行兼容，所以每种浏览器使用了自己的私有前缀与标准进行区分，当标准确立后，各大浏览器将逐步支持不带前缀的css3新属性
>
> 目前已有很多私有前缀可以不写了，但为了兼容老版本的浏览器，可以仍沿用私有前缀和标准方法，逐渐过渡。
>
> 一般来说，移动端更新迭代很快，对CSS3支持良好, 因此我们在移动端没必要写太多的前缀，因为移动端的ios和Android的浏览器都是webkit内核。

```
谷歌、苹果浏览器：-webkit-
火狐浏览器：-moz-
IE浏览器：-ms-
欧朋浏览器：-o-
```

```css
div {
    width: 200px;
    height: 200px;
    background-color: pink;
    margin: 100px auto;

    /*谷歌浏览器和safari浏览器的前缀 -webkit-*/
    -webkit-transform: rotate(45deg);
    /*火狐浏览器的前缀 -moz-*/
    -moz-transform: rotate(45deg);
    /*ie浏览器的前缀 -ms-*/
    -ms-transform: rotate(45deg);
    /*opera浏览器的前缀 -o-*/
    -o-transform: rotate(45deg);
    /*规范化后的写法*/
    transform: rotate(45deg);
}
```

【css3初体验】

# CSS3选择器

## 关系选择器

![img](images/s1.png)

## 属性选择器

![img](images/s2.png)

## 伪类选择器

> 伪类选择器的语法：都带有一个 冒号 `:`

### child系列（重点）

![img](images/s3.png)

思考：

```
1. 第一列变成红色
2. 最后一列变成红色
3. 倒数第二列变成红色
```

### 其他伪类选择器

```
:of-type系列，  用法与child系列很像，但是找的是子元素中对应类型的下标（了解，用的不多）
:focus    查找获取到焦点的文本框
:checked 获得选中的checkbox
:disabled 获得不可用的框
:enabled 获得可用的框
:not(selector)选择不匹配selector的那些元素
:target  获取当前活跃的锚链接
```

## 伪元素选择器

### before和after

```
注意事项：
//1.    必须指定content属性，可以在content属性中写入文本内容，但是通常为空字符串。
//2.    默认是行内元素，无法设置宽高，需要指定display:block或者position:absolute
E::before :在元素子节点的最前面添加一个内容。
E::after  :在元素子节点的最后面添加一个内容。
```

关于单冒号和双冒号问题：

```
关于:before与::before的区别
:before是css2中伪元素的写法，但是呢，在css3中严格规定，伪类采用单冒号，伪元素需要使用双冒号。为了兼容旧的代码，当浏览器碰到了:before之后，会自动的转换成::before。
如果需要兼容老的浏览器，比如IE678，推荐使用:before
如果不需要兼容老的浏览器，比如移动端，推荐使用::before
```

### 其他伪元素选择器

```
::first-letter  :获取元素的第一个字符
::first-line   :获取元素的第一行
::selection   ：获取选中的元素
```

# CSS3阴影

## 如何查看css3文档

学会使用工具，可以让我们事半功倍。

```
[]        表示全部可选项
||        表示或者
|        表示多选一
？       表示0个或者1个
*        表示0个或者多个
{2,3}        表示范围
```

## 文字阴影

> text-shadow:文字阴影

```
语法： text-shadow：水平偏移 垂直偏移 羽化大小 颜色
```

## 边框阴影

> box-shadow:边框阴影

```
none： 无阴影 
<length>：第1个长度值用来设置对象的阴影水平偏移值。可以为负值 
<length>：第2个长度值用来设置对象的阴影垂直偏移值。可以为负值 
<length>：如果提供了第3个长度值则用来设置对象的阴影模糊值。不允许负值 
<length>：如果提供了第4个长度值则用来设置对象的阴影外延值。可以为负值 
<color>：设置对象的阴影的颜色。 
inset：设置对象的阴影类型为内阴影。该值为空时，则对象的阴影类型为外阴影
```

# CSS3背景

> 在css2中已经有background属性了，用于设置盒子的背景相关的一些样式，在CSS3中新增加了几个背景相关的几个属性。

## background-size

> 用户设置背景图片的尺寸大小

```javascript
//注意：这两种设置方式会导致图片失真。
/*background-size:设置背景图片的大小*/
background-size: 600px 400px;

/* 百分比是相对于盒子自身的宽度和高度 */
background-size: 100% 100%;
```

不失真的设置方式（等比例缩放）

```javascript
/*containe保证等比例缩放,但是会出现留白*/
background-size: contain;

/*cover保证等比例缩放,并且不会留白，但是出现有一部分图片不显示*/
background-size: cover;
```

【演示：01-background-size的使用.html】

【案例：02-全屏背景.html】

## background-clip

> 设置背景区域的大小

```javascript
/*盒子的背景区域是整个盒子，包括边框和padding*/
/*默认值，设置背景区域包括了边框*/
background-clip: border-box;

/*背景区域只包含padding和content*/
background-clip: padding-box;

/*背景区域只包含content*/
background-clip: content-box;
```

【演示：03-background-clip.html】

## background-origin

> 设置背景图片的原点的位置，默认是padding的地方开始

```javascript
background-image: url(images/bg.jpg);
/*设置原点从border开始*/
background-origin: border-box;

/*设置原点从padding开始,默认值*/
background-origin: padding-box;

/*设置原点从content开始*/
background-origin: content-box;
```

【演示：04-background-origin.html】

## 多重背景

> background设置背景的时候，可以设置多个背景图片，使用逗号隔开。注意颜色只能设置一次，并且通常来说，颜色都是在最后面进行设置。
>
> background是一个合写的属性，如果在background之前设置了background相关的样式，会被覆盖掉。

```css
background: url(images/mn1.jpg) no-repeat top left, url("images/mn2.jpg") no-repeat right bottom, pink;
```

【多重背景-语法.html】

【多重背景-小泡泡.html】

【多重背景的应用.html】

# CSS3渐变

## 线性渐变

> linear-gradient指沿着某条直线朝一个方向产生的渐变效果。

```javascript
//注意：渐变实际上相当与一张图片，因为需要加给background-image才会生效
//渐变的两个要求：有区间，有颜色变化。
//最简单的渐变
background-image: linear-gradient(red, green);
//设定渐变的方向
background-image: linear-gradient(to right, red, green);
//也可以设定渐变的角度
background-image: linear-gradient(45deg, red, green);
//设定渐变的范围
background-image: linear-gradient(to right, red 20%, green 80%)
//每一个区间表示渐变颜色的范围
background-image: linear-gradient(to right, red 20%, green 20%)

```

【演示：01-渐变-线性渐变.html】

【演示：02-导航按钮.html】

【案例：03-渐变-案例-发廊效果.html】

## 径向渐变

> radial-gradient指从一个中心点开始沿着四周产生渐变效果

```CSS
/*1. 最简单的渐变*/
background-image: radial-gradient(red, green);

/*2. 指定圆的半径和圆心*/
background-image: radial-gradient(200px at center, red, green);

/*3. 指定椭圆*/
background-image: radial-gradient(200px 80px at center, red, green);

/*4. 指定范围*/
background-image: radial-gradient(200px at center, green 50%, red 50%);

```

# CSS3盒子模型



> CSS3中可以通过box-sizing 来指定盒模型，即可指定为content-box、border-box，这样我们计算盒子大小的方式就发生了改变。

可以分成两种情况： 

+ box-sizing: border-box 计算方式为content = width – border - padding 
+ box-sizing: content-box 计算方式为content = width