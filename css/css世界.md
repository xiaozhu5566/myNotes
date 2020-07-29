# 《css世界》 张鑫旭

## 盒尺寸四大家族
### 深入理解content

替换元素：通过修改某个属性呈现的内容可以被替换的元素。

替换元素的基线一般是元素的下边缘。

<input type="button"> white-space: pre;  当内容比较多时，不会自动换行。
<button> white-space: nomal; 会自动换行

对于firefox浏览器，src缺省的<img>不是替換元素。

<img>元素的默认声明：object-fit: fill
object-fit: fill、contain(保持比例)、none;

getComputedStyle


content 
attr()属性值内容生成
url()

content计数器
counter-reset
content-increment
counter()/counters()

### padding
> 内联元素的padding只会影响水平方向，不会影响垂直方向。这句话是不正确的。
因为内联元素的垂直表现完全受line-heght与vetical-align的影响，垂直方向发生了层叠。视觉上没有收影响，可以用background-color证明。

内联元素的padding,在不影响布局的情况下，增加链接或按钮的可点击区域。

padding不支持负值，margin支持。

对于内联元素padding会断行的。

书中说，原生<button>的padding在各大浏览器中的表现行为不泰一致，因此一般采用<a>标签模拟。
也可以这样：
<button id="btn">
<label for="btn">

## margin
margin: auto; 实现块级元素的右对其，左对齐，居中； (不只是float)
margin-left: auto; margin-right: auto; margin: 0 auto;

height: 100%;只有父级元素设定具体的高度时才有效。

display: inline;的非替换元素的垂直margin是无效的。

垂直居中对齐的一种方法：
```css
{
  position: absolute;
  top:0; right: 0; bottom: 0; left: 0;
  width: 100px; height: 50px;
  margin: 0;
}
```

writing-mode 改变默认的文档流

浮动和绝对定位可以让元素块状化。

父级和第一个元素或者和最后一个元素会发生margin合并：
```html
<div>
  <p style="margin: 50px">hello</p>
</div>
``` 
(因为，我们会在父级设置下面的属性，因此不常发现父级与子级元素也会发生margin合并。)
解决方法：
父元素设置为块状格式化上下文元素 (父级overflow:hidden;)
设置border-top/padding-top（*-bottom）



## border
当没有指定border-color的时候，会还使用当前元素 color计算值作为边框色。 
border: transparent;业界与增加元素的点击区域（移动端）；
三角形绘制

## 内联元素与流
## 内联元素基石 line-height

对于非替换元素的纯内联元素，其可视高度完全有line-height决定
em-box = content-area = font-size(在宋体的情况下)

行距 = line-height - font-size

line-height其实是影响不了替换元素的，而是“幽灵空白节点（strut）”的缘故。
line-htight对块级元素页没有作用，只不过通过改变块级中的内联元素的间接的改变块级元素的高度。

line-height可以使内联元素近似垂直居中，是近似。

注意“幽灵空白节点”，很多"怪异"的现象都可以用他来作解释。
注意line-height的数字、百分比、长度值的继承的区别。

vetical-align起作用的前提： 内联元素、display: table-cell.
浮动、绝对定位会让元素块状化。
text-align两端对齐需要内容超出一行。

替换元素的基线是元素的下边缘，文本的基线是”x“的底部。

基线网上1/2x-height处是middle的位置。

大小不固定的弹窗永远居中例子p144.


line-height的各类属性值： 
nomal
数字
长度
百分比

其中（em、百分比）子元素会继承计算过后的值。


## 第6章 流的破坏和保护
### float
float布局，容错性不好，还有一些兼容性问题。
块状化：float除了none，都会使元素块状化 --> display: block;

float特性：
包裹性、块状化并格式化上下文、破坏文档流、没有任何margin合并

getComputedStyle()

行框盒子如果和浮动元素有重叠垂直高度有重叠，则行框盒子在正常定位状态下只会**跟随浮动元素**，而不会发生重叠。

clear属性：官方解释，元素盒子的变不能和**前面**的浮动元素相邻。 

BFC -- 块级格式化上下文。
BFC元素不会发生margin合并。
常见的触发BFC的情况：
+ <html>根元素
+ float值部位none;
+ overflow: auto\scroll\hidden
+ display: table-cell\table-caption\inline-block
+ position值不是relative\static


overflow裁剪的是border-box

url地址锚链定位，是让元素定位在浏览器窗体的上边缘，focus锚点定位是让元素在浏览器窗体范围内显示即可，不一定是上边缘。



