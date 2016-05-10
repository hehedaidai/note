#CSS的单位及css3的calc()及line-height百分比

说到css的单位，大家应该首先想到的是px,也就是像素，我们在网页布局中一般都是用px，但是近年来自适应网页布局越来越多，em和百分比也经常用到了。然后随着手机的流行，web app和hybrid app的开发，都用到了css3技术，在css3中，新增了许多单位，rem、vw和vh、vmin和vmax、ch和ex等等，那现在对这些单位分别做一下详细的介绍吧。
``


##em

做前端的应该对em不陌生，不是什么罕见的单位，是相对单位，参考物是父元素的`font-size`，具有继承的特点。如果字体大小是16px（浏览器的默认值），那么` 1em = 16px。`

不过，这样使用很复杂，很难很好的与px进行对应，因此，前端开发的前辈们总结了一个经验

`body {
font-size: 62.5%;
}`
那么，这样之后` 1em = 10px `在布局等使用的时候好换算了很多。

##百分比

百分比相信大家更不会陌生了，百分比一般宽泛的讲是相对于父元素，但是并不是十分准确。

1. 对于普通定位元素就是我们理解的父元素
2. 对于`position: absolute;`的元素是相对于已定位的父元素`（offset parent）`
3. 对于`position: fixed;`的元素是相对于 `ViewPort`
`viewport：`可视窗口，也就是浏览器的window那么大。

例外情况

1.  使用了`padding、margin `等，实际百分比和你想要的百分比是有区别的。（关于这个，解决方法之一，就是我们可以使用css3的`calc()`属性，具体，您请继续往下看，在文章最后我会解释。）
2. ` line-height`百分比的一些情况，通常结果是百分比 计算后的值。（关于这个，您请继续往下看。。。）

##‘vh ’和 ‘vw’

IE10＋ 和现代浏览器都支持这两个单位。

* ‘vw’ Viewport宽度，‘ 1vw ’等于viewport宽度的1%
* ‘vh’ Viewport高度， ‘1vh ’等于viewport高的的1%
* vw和vh会随着viewport变化自动变化，再也不用js控制全屏了。

甚至有些人丧心病狂的字体大小都用vw和vh控制，来达到字体和viewport大小同步的效果。

##‘vmin’和‘vmax’

##IE10+ 和现代浏览器都已经支持‘vmin’

‘webkit’浏览器之前不支持‘vmax’，新版已经支持，所有现代浏览器已经支持，但是IE 全部 不支持‘vmax’

* ‘vmin’ ’vw‘和’vh‘中比较 小 的值
* ’vmax‘ ’vw‘和’vh‘中比较 大的值
这两个属性也会随着’viewport’变化

##‘ch’和‘ex’

IE9+ 和现代浏览器都已经支持,这两个单位时根据 当前‘font-family ’的相对单位。

‘ch’ 字符0的宽度
‘ex’ 小写字符x的高度

![](http://i5.buimg.com/2b26fa3c5778675e.jpg)

当font-family改变的时候这两个单位的值也会变化，不同字体表现的样式不一样。

##css3的`calc()`

上面我们已经提到了`calc()`，下面我们就具体说一说吧！

浏览器支持IE9+、FF4.0+、Chrome19+、Safari6+

`calc()`语法非常简单，就像我们小时候学加 （+）、减（-）、乘（*）、除（/）一样，使用数学表达式来表示：

`.haorooms {
`  width: calc(expression);`
`}`
这样`padding`和`margin`和百分比一起用，问题就可以解决了。

例如，我们margin是20px。那么我们就可以写成

`.haorooms{`
`  width: calc(100% - 20px);  //注：减号前后要有空格，否则很可能不生效！！`
`}`
也可以这么用：

`.box {`
`    background: #f60;`
`    height: 50px;`
`    padding: 10px;`
`    border: 5px solid green;`
`     width: 90%;/*写给不支持calc()的浏览器*/`
`    width:-moz-calc(100% - (10px + 5px) * 2);`
`    width:-webkit-calc(100% - (10px + 5px) * 2);`
`    width: calc(100% - (10px + 5px) * 2);`
`}`

`line-height`百分比

`line-height`百分比在面试中可能经常问到。例如你知道`line-height:120%`和`line-height:1.2`的区别吗？

现在就说一下行高带单位和不带单位的区别，例如下面的例子：

`line-height:26px; `表示行高为26个像素
`line-heigth:120%;`表示行高为当前字体大小的120%
`line-height:2.6em;` 表示行高为当前字体大小的2.6倍
带单位的行高都有继承性，其子元素继承的是计算值，如父元素的字体大小为14px，定义行高`line-height:2em;`则计算值为 28px，不会因其子元素改变字体尺寸而改变行高。(例如：父元素14px，子元素12px,那么行高就是28px，子元素虽然字体是12，行高还是父元素的行高)

`line-height:2.6;`表示行高为当前字体大小的2.6倍
不带单位的行高是直接继承，而不是计算值，如父元素字体尺寸为14px，行高line-height:2;他的行高为28px;子元素尺寸为12px，不需要再定义行高，他默认的行高为24px。（例如：子元素12px，他的行高是24,不会继承父元素的28）
