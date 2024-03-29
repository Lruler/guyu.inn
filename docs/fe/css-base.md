---
title: CSS基础知识
---
这一篇主要介绍一些css相关知识，主要也就是一些概览，因为一些深入的内容都需要一篇单独的篇幅去讲，想系统学习css的还是去看看书比较好。

## CSS选择器及其优先级

| **选择器**     | **格式**      | **优先级权重** |
| -------------- | ------------- | -------------- |
| id选择器       | #id           | 100            |
| 类选择器       | #classname    | 10             |
| 属性选择器     | a[ref=“eee”]  | 10             |
| 伪类选择器     | li:last-child | 10             |
| 标签选择器     | div           | 1              |
| 伪元素选择器   | li:after      | 1              |
| 相邻兄弟选择器 | h1+p          | 0              |
| 子选择器       | ul>li         | 0              |
| 后代选择器     | li a          | 0              |
| 通配符选择器   | *             | 0              |

对于选择器的**优先级**：

- 标签选择器、伪元素选择器：1
- 类选择器、伪类选择器、属性选择器：10
- id 选择器：100
- 内联样式：1000

**注意事项：**

- !important声明的样式的优先级最高；
- 如果优先级相同，则最后出现的样式生效；
- 继承得到的样式的优先级最低；
- 通用选择器（*）、子选择器（>）和相邻同胞选择器（+）并不在这四个等级中，所以它们的权值都为 0 ；
- 样式表的来源不同时，优先级顺序为：内联样式 > 内部样式 > 外部样式 > 浏览器用户自定义样式 > 浏览器默认样式。

关键选择器（key selector）。选择器的最后面的部分为关键选择器（即用来匹配目标元素的部分）。CSS选择符是从右到左进行匹配的。当使用后代选择器的时候，浏览器会遍历所有子元素来确定是否是指定的元素等等


## transform优势
 `transform: translateZ(0)` 和 `transform: translate3d(0, 0, 0)` 都是 CSS 中的变换属性，它们都用于在 3D 空间中移动元素。尽管表面上看它们没有实际的移动作用，但实际上它们有一些重要的副作用。这两个属性的主要作用如下：

1. 触发硬件加速：当使用这两个属性时，浏览器会尝试使用 GPU（图形处理器）对该元素执行硬件加速，从而提高动画和页面的性能。GPU 加速可以减少 CPU 负担，使页面渲染更加流畅。

2. 创建新的层叠上下文：这两个属性会创建一个新的层叠上下文，有助于更好地控制元素的层叠顺序。层叠上下文是一个容器，它包含了一组层叠层次，使得元素在层叠顺序上更加有序。

3. 优化复合（compositing）：通过将元素分配到单独的图层，浏览器可以在不影响其他元素的情况下独立更新和绘制这些元素。这可以提高页面性能，特别是在执行动画或其他频繁更新的场景中。

总的来说，尽管 `transform: translateZ(0)` 和 `transform: translate3d(0, 0, 0)` 看似没有实际移动元素，但它们可以帮助优化页面性能、提高动画流畅度，并更好地控制元素的层叠顺序。

**为什么有时候⽤translate来改变位置⽽不是定位？**
translate 是 transform 属性的⼀个值。改变transform或opacity不会触发浏览器重新布局（reflow）或重绘（repaint），只会触发复合（compositions）。⽽改变绝对定位会触发重新布局，进⽽触发重绘和复合。transform使浏览器为元素创建⼀个 GPU 图层，但改变绝对定位会使⽤到 CPU。 因此translate()更⾼效，可以缩短平滑动画的绘制时间。 ⽽translate改变位置时，元素依然会占据其原始空间，绝对定位就不会发⽣这种情况。

## 深色模式
@media (prefers-color-scheme) 监控 但这只是根据系统来

但一般浏览器点击按钮的那个切换不是这么做的，会用css变量 然后改变顶部属性
比如
```css
    :root[data-theme="light"] {
      --bg: #efefef;
      --textColor: #282c34;
      --borderColor: #2c2c3a;
      --primary: #1bcfe7;
    }

    :root[data-theme="dark"] {
      --bg: #3d3a3a;
      --textColor: #f9fafd;
      --borderColor: #2c2c3a;
      --primary: #24acf2;
    }

    body {
      background-color: var(--bg);
      color: var(--textColor);
    }
```
然后自定义元素
```html
<html lang="en" data-theme="light">
```
change函数 这样就行了
```js
    function changeMode() {
      const darkMode =
        window.document.documentElement.getAttribute("data-theme") || "light";
      if (darkMode == "light") {
        window.document.documentElement.setAttribute("data-theme", "dark");
      } else {
        window.document.documentElement.setAttribute("data-theme", "light");
      }
    }
```

## 伪类和伪元素
[GPT-4] 在CSS中，伪类和伪元素是一种特殊的选择器，它们允许你根据元素的状态或位置来应用样式，而无需修改HTML结构或添加额外的类。以下是一些常用的伪类和伪元素：

伪类：

1. `:hover`：当鼠标悬停在元素上时应用样式。
2. `:active`：当元素被激活（例如，鼠标按下或触摸开始）时应用样式。
3. `:focus`：当元素获得输入焦点（例如，通过点击或键盘导航）时应用样式。
4. `:visited`：当链接被访问过时应用样式。
5. `:link`：当链接未被访问过时应用样式。
6. `:first-child`：当元素是其父元素的第一个子元素时应用样式。
7. `:last-child`：当元素是其父元素的最后一个子元素时应用样式。
8. `:nth-child(n)`：当元素是其父元素的第n个子元素时应用样式。
9. `:nth-last-child(n)`：当元素是其父元素的倒数第n个子元素时应用样式。
10. `:first-of-type`：当元素是其父元素中相同类型的第一个子元素时应用样式。
11. `:last-of-type`：当元素是其父元素中相同类型的最后一个子元素时应用样式。
12. `:nth-of-type(n)`：当元素是其父元素中相同类型的第n个子元素时应用样式。
13. `:nth-last-of-type(n)`：当元素是其父元素中相同类型的倒数第n个子元素时应用样式。
14. `:empty`：当元素没有子元素（包括文本节点）时应用样式。
15. `:not(selector)`：当元素不匹配给定选择器时应用样式。
16. `:checked`：当表单元素（如复选框或单选按钮）被选中时应用样式。
17. `:disabled`：当表单元素被禁用时应用样式。
18. `:enabled`：当表单元素处于启用状态时应用样式。
19. `:valid`：当表单元素满足验证要求时应用样式。
20. `:invalid`：当表单元素不满足验证要求时应用样式。

伪元素：

1. `::before`：在元素内容的前面插入生成的内容。
2. `::after`：在元素内容的后面插入生成的内容。
3. `::first-letter`：选择元素内容的第一个字母，可以用于实现首字下沉等效果。
4. `::first-line`：选择元素内容的第一行，可以用于设置特殊的文本样式。
5. `::selection`：选择用户选中的文本，可以用于自定义选中文本的样式。
6. `::placeholder`：选择输入框或文本区域的占位符文本，可以用于自定义占位符样式。
7. `::backdrop`：选择全屏模式下的背景遮罩，可以用于自定义遮罩样式。

注意：在CSS2中，伪元素使用单冒号（例如`:before`和`:after`）。从CSS3开始，为了与伪类区分开来，伪元素使用双冒号（例如`::before`和`::after`）。虽然现代浏览器通常同时支持单冒号和双冒号语法，但建议使用双冒号语法以遵循最新的规范。

## 隐藏元素的方法有哪些

+ display: none：渲染树不会包含该渲染对象，因此该元素不会在页面中占据位置，也不会响应绑定的监听事件。
+ visibility: hidden：元素在页面中仍占据空间，但是不会响应绑定的监听事件。
+ opacity: 0：将元素的透明度设置为 0，以此来实现元素的隐藏。元素在页面中仍然占据空间，并且能够响应元素绑定的监听事件。
+ position: absolute：通过使用绝对定位将元素移除可视区域内，以此来实现元素的隐藏。
+ z-index: 负值：来使其他元素遮盖住该元素，以此来实现隐藏。
+ clip/clip-path ：使用元素裁剪的方法来实现元素的隐藏，这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。
+ transform: scale(0,0)：将元素缩放为 0，来实现元素的隐藏。这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。

## link和@import的区别
两者都是外部引用CSS的方式，它们的区别如下：

+ link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
+ link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。
+ link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。
+ link支持使用Javascript控制DOM去改变样式；而@import不支持。

## transition和animation的区别

+ transition是过度属性，强调过度，它的实现需要触发一个事件（比如鼠标移动上去，焦点，点击等）才执行动画。它类似于flash的补间动画，设置一个开始关键帧，一个结束关键帧。
+ animation是动画属性，它的实现不需要触发事件，设定好时间之后可以自己执行，且可以循环一个动画。它也类似于flash的补间动画，但是它可以设置多个关键帧（用@keyframe定义）完成动画。

## display:none与visibility:hidden的区别
这两个属性都是让元素隐藏，不可见。两者区别如下：
（1）在渲染树中

+ display:none会让元素完全从渲染树中消失，渲染时不会占据任何空间；
+ visibility:hidden不会让元素从渲染树中消失，渲染的元素还会占据相应的空间，只是内容不可见。

（2）是否是继承属性

+ display:none是非继承属性，子孙节点会随着父节点从渲染树消失，通过修改子孙节点的属性也无法显示；
+ visibility:hidden是继承属性，子孙节点消失是由于继承了hidden，通过设置visibility:visible可以让子孙节点显示；

（3）修改常规文档流中元素的 display 通常会造成文档的重排，但是修改visibility属性只会造成本元素的重绘；

（4）如果使用读屏器，设置为display:none的内容不会被读取，设置为visibility:hidden的内容会被读取。

## 对requestAnimationframe的理解
实现动画效果的方法比较多，Javascript 中可以通过定时器 setTimeout 来实现，CSS3 中可以使用 transition 和 animation 来实现，HTML5 中的 canvas 也可以实现。除此之外，HTML5 提供一个专门用于请求动画的API，那就是 requestAnimationFrame，顾名思义就是请求动画帧。
MDN对该方法的描述：

> window.requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。

语法： window.requestAnimationFrame(callback);  其中，callback是下一次重绘之前更新动画帧所调用的函数(即上面所说的回调函数)。该回调函数会被传入DOMHighResTimeStamp参数，它表示requestAnimationFrame() 开始去执行回调函数的时刻。该方法属于宏任务，所以会在执行完微任务之后再去执行。
取消动画： 使用cancelAnimationFrame()来取消执行动画，该方法接收一个参数——requestAnimationFrame默认返回的id，只需要传入这个id就可以取消动画了。
优势：

+ CPU节能：使用SetTinterval 实现的动画，当页面被隐藏或最小化时，SetTinterval 仍然在后台执行动画任务，由于此时页面处于不可见或不可用状态，刷新动画是没有意义的，完全是浪费CPU资源。而RequestAnimationFrame则完全不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，因此跟着系统走的RequestAnimationFrame也会停止渲染，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销。
+ 函数节流：在高频率事件( resize, scroll 等)中，为了防止在一个刷新间隔内发生多次函数执行，RequestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销，一个刷新间隔内函数执行多次时没有意义的，因为多数显示器每16.7ms刷新一次，多次绘制并不会在屏幕上体现出来。
+ 减少DOM操作：requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率，一般来说，这个频率为每秒60帧。

setTimeout执行动画的缺点：它通过设定间隔时间来不断改变图像位置，达到动画效果。但是容易出现卡顿、抖动的现象；原因是：

+ settimeout任务被放入异步队列，只有当主线程任务执行完后才会执行队列中的任务，因此实际执行时间总是比设定时间要晚；
+ settimeout的固定时间间隔不一定与屏幕刷新间隔时间相同，会引起丢帧。

## 盒模型
标准盒模型和IE盒模型的区别在于设置width和height时，所对应的范围不同：

+ 标准盒模型的width和height属性的范围只包含了content，
+ IE盒模型的width和height属性的范围包含了border、padding和content。
可以通过修改元素的box-sizing属性来改变元素的盒模型：
+ box-sizeing: content-box表示标准盒模型（默认值）
+ box-sizeing: border-box表示IE盒模型（怪异盒模型）


## z-index属性在什么情况下会失效
通常 z-index 的使用是在有两个重叠的标签，在一定的情况下控制其中一个在另一个的上方或者下方出现。z-index值越大就越是在上层。z-index元素的position属性需要是relative，absolute或是fixed。

z-index属性在下列情况下会失效：

+ 父元素position为relative时，子元素的z-index失效。解决：父元素position改为absolute或static；
+ 元素没有设置position属性为非static属性。解决：设置该元素的position属性为relative，absolute或是fixed中的一种；
+ 元素在设置z-index的同时还设置了float浮动。解决：float去除，改为display：inline-block；

## 说一说css中的文档流
HTML文档流（Document Flow），也称为文档布局或文档流动，是指在浏览器中渲染HTML文档时，元素按照其在HTML文档中出现的顺序进行布局和排列的过程。它是HTML文档中元素相对于其父元素和兄弟元素的默认布局行为。

在文档流中，HTML元素按照从上到下、从左到右的顺序进行渲染，并且元素在默认情况下会占据其在文档中指定的空间。文档流是HTML布局的基础，它决定了元素在页面中的位置和相互之间的关系。

浮动，绝对定位，固定定位，flex和grid布局中的子元素，display: none 这些属性会让元素脱离文档流

## 隐藏元素的方法有哪些

1. display: none：渲染树不会包含该渲染对象，因此该元素不会在页面中占据位置，也不会响应绑定的监听事件。
2. visibility: hidden：元素在页面中仍占据空间，但是不会响应绑定的监听事件。
3. opacity: 0：将元素的透明度设置为 0，以此来实现元素的隐藏。元素在页面中仍然占据空间，并且能够响应元素绑定的监听事件。
4. position: absolute：通过使用绝对定位将元素移除可视区域内，以此来实现元素的隐藏。
5. z-index: 负值：来使其他元素遮盖住该元素，以此来实现隐藏。
6. clip/clip-path ：使用元素裁剪的方法来实现元素的隐藏，这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。
7. transform: scale(0,0)：将元素缩放为 0，来实现元素的隐藏。这种方法下，元素仍在页面中占据位置，但是不会响应绑定的监听事件。

## CSS3中有哪些新特性

+ 新增各种CSS选择器 （: not(.input)：所有 class 不是“input”的节点）
+ 圆角 （border-radius:8px）
+ 多列布局 （multi-column layout）
+ 阴影和反射 （Shadoweflect）
+ 文字特效 （text-shadow）
+ 文字渲染 （Text-decoration）
+ 线性渐变 （gradient）
+ 旋转 （transform）
+ 增加了旋转,缩放,定位,倾斜,动画,多背景

## 对line-height 的理解及其赋值方式
（1）line-height的概念：

+ line-height 指一行文本的高度，包含了字间距，实际上是下一行基线到上一行基线距离；
+ 如果一个标签没有定义 height 属性，那么其最终表现的高度由 line-height 决定；
+ 一个容器没有设置高度，那么撑开容器高度的是 line-height，而不是容器内的文本内容；
+ 把 line-height 值设置为 height 一样大小的值可以实现单行文字的垂直居中；
+ line-height 和 height 都能撑开一个高度；

（2）line-height 的赋值方式：

+ 带单位：px 是固定值，而 em 会参考父元素 font-size 值计算自身的行高
+ 纯数字：会把比例传递给后代。例如，父级行高为 1.5，子元素字体为 18px，则子元素行高为 1.5 * 18 = 27px
+ 百分比：将计算后的值传递给后代

line-height会引起页面重排

## 对BFC的理解
先来看两个相关的概念：

+ Box: Box 是 CSS 布局的对象和基本单位，⼀个⻚⾯是由很多个 Box 组成的，这个Box就是我们所说的盒模型。
+ Formatting context：块级上下⽂格式化，它是⻚⾯中的⼀块渲染区域，并且有⼀套渲染规则，它决定了其⼦元素将如何定位，以及和其他元素的关系和相互作⽤。

块格式化上下文（Block Formatting Context，BFC）是Web页面的可视化CSS渲染的一部分，是布局过程中生成块级盒子的区域，也是浮动元素与其他元素的交互限定区域。

通俗来讲：BFC是一个独立的布局环境，可以理解为一个容器，在这个容器中按照一定规则进行物品摆放，并且不会影响其它环境中的物品。如果一个元素符合触发BFC的条件，则BFC中的元素布局不受外部影响。
创建BFC的条件：

+ 根元素：body；
+ 元素设置浮动：float 除 none 以外的值；
+ 元素设置绝对定位：position (absolute、fixed)；
+ display 值为：inline-block、table-cell、table-caption、flex等；
+ overflow 值为：hidden、auto、scroll；

BFC的特点：

+ 垂直方向上，自上而下排列，和文档流的排列方式一致。
+ 在BFC中上下相邻的两个容器的margin会重叠
+ 计算BFC的高度时，需要计算浮动元素的高度
+ BFC区域不会与浮动的容器发生重叠
+ BFC是独立的容器，容器内部元素不会影响外部元素
+ 每个元素的左margin值和容器的左border相接触

BFC的作用：

+ 解决margin的重叠问题：由于BFC是一个独立的区域，内部的元素和外部的元素互不影响，将两个元素变为两个BFC，就解决了margin重叠的问题。
+ 解决高度塌陷的问题：在对子元素设置浮动后，父元素会发生高度塌陷，也就是父元素的高度变为0。解决这个问题，只需要把父元素变成一个BFC。常用的办法是给父元素设置overflow:hidden。
+ 创建自适应两栏布局：可以用来创建自适应两栏布局：左边的宽度固定，右边的宽度自适应。

## position的属性有哪些，区别是什么
+ absolute： 生成绝对定位的元素，相对于static定位以外的一个父元素进行定位。
+ relative： 生成相对定位的元素，相对于其原来的位置进行定位。
+ fixed： 生成绝对定位的元素，指定元素相对于屏幕视⼝（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变，⽐如回到顶部的按钮⼀般都是⽤此定位⽅式。（具有破坏性，会导致其他元素位置的变化。）
+ sticky： 粘性定位的元素是依赖于用户的滚动，在 position:relative 与 position:fixed 定位之间切换。元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。
+ static： 默认值，没有定位，元素出现在正常的文档流中，会忽略 top, bottom, left, right 或者 z-index 声明，块级元素从上往下纵向排布，⾏级元素从左向右排列。
+ inherit： 规定从父元素继承position属性的值

## 让一个元素水平垂直居中

- **水平居中**

  - 对于 行内元素 : `text-align: center`;

  - 对于确定宽度的块级元素：

    （1）width和margin实现。`margin: 0 auto`;

    （2）绝对定位和margin-left: (父width - 子width）/2, 前提是父元素position: relative

  - 对于宽度未知的块级元素

    （1）`table标签配合margin左右auto实现水平居中`。使用table标签（或直接将块级元素设值为 display:table），再通过给该标签添加左右margin为auto。

    （2）inline-block实现水平居中方法。display：inline-block和text-align:center实现水平居中。

    （3）`绝对定位+transform`，translateX可以移动本身元素的50%。

    （4）flex布局使用`justify-content:center`

- **垂直居中**

  1. 利用 `line-height` 实现居中，这种方法适合纯文字类
  2. 通过设置父容器 相对定位 ，子级设置 `绝对定位`，标签通过margin实现自适应居中
  3. 弹性布局 flex :父级设置display: flex; 子级设置margin为auto实现自适应居中
  4. 父级设置相对定位，子级设置绝对定位，并且通过位移 transform 实现
  5. `table 布局`，父级通过转换成表格形式，`然后子级设置 vertical-align 实现`。（需要注意的是：vertical-align: middle使用的前提条件是内联元素以及display值为table-cell的元素）。

## css变量
```css
var: 
根节点声明变量，后续使用 var(--xxxx)

calc:
可以计算 calc(var(--xxx) + 4px)

语法：attr( attribute-name <type-or-unit>? [, <fallback> ]? )
传统的attr()语法只能让HTML属性作为字符串使用，且只能使用在伪元素中，例如：

<span data-title="提示">按钮</span>
span:hover::after {
    content: attr(data-title);
}
但是全新的attr()语法那可就完全不得了了，可以让HTML属性值转换成任意的CSS数据类型。

例如如下所示的HTML和CSS语句：

<button bgcolor="skyblue" radius="4">按钮</button>
<button bgcolor="#00000040" radius="1rem">按钮</button>
<button bgcolor="red" radius="50%">按钮</button>
<button bgcolor="orange" radius="100% / 50%" title="by zhangxinxu(.com)">按钮</button>
button {
    background-color: attr(bgcolor color);
    border-radius: attr(radius px, 4px);
}

clamp() 函数的作用是把一个值限制在一个上限和下限之间，当这个值超过最小值和最大值的范围时，在最小值和最大值之间选择一个值使用。它接收三个参数：最小值、首选值、最大值。
```

### 移动端

移动端上因为屏幕尺寸和分辨率不同 会导致同样大小的像素在不同设备上显示的大小不同

就比如我在pc写了一个1px的横线，它在移动端上就很有可能显现出来2px的大小

所以移动端一般建议用相对单位开发。

像素表示屏幕显示单位的基本元素。分辨率指屏幕上所显示的像素数目


在 CSS 中，`margin` 和 `padding` 的百分比值是根据其父元素的宽度来计算的，而不是根据元素本身的宽度或高度。这意味着，无论是水平方向（左右）还是垂直方向（上下）的 `margin` 或 `padding`，都是基于父元素宽度的百分比来计算的。

例如，假设一个元素的父元素宽度为 500px，那么：

- 如果设置 `margin-left: 10%;`，那么左边距的实际值将为 50px（即 500px * 10%）。
- 如果设置 `padding-top: 20%;`，那么上边距的实际值将为 100px（即 500px * 20%）。

需要注意的是，这种基于父元素宽度的百分比计算方式在某些情况下可能导致布局不如预期。因此，在使用百分比值设置 `margin` 和 `padding` 时，请确保了解其计算方式以避免潜在问题。


flex:flex-grow flex-shrink flex-basis

flex-grow:定义放大比例，默认为0，规定项目相对于其他灵活的项目进行扩展的量
flex-shrink: 定义了项目的缩小比例，仅在宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值，默认为1
flex-basis:给上面两个属性分配多余空间之前, 计算项目是否有多余空间, 默认值为 auto, 即项目本身的大小

flex:1 ===  flex-grow: 1; flex-shrink: 1; flex-basis: 0%;


## 为什么css要放在头部 js要放在尾部
首先整个页面展示给用户会经过html 的解析与渲染过程。

而外链css无论放在html的任何位置都不影响html的解析，但是影响html的渲染。

如果将css放在尾部，html的内容可以第一时间显示出来，但是会阻塞html行内css的渲染。

浏览器的这个策略其实很明智的，想象一下，如果没有这个策略，页面首先会呈现出一个行内css样式，待CSS下载完之后又突然变了一个模样。用户体验可谓极差，而且渲染是有成本的。

如果将css放在头部，css的下载解析是可以和html的解析同步进行的，放到尾部，要花费额外时间来解析CSS，并且浏览器会先渲染出一个没有样式的页面，等CSS加载完后会再渲染成一个有样式的页面，页面会出现明显的闪动的现象。

## css加载会造成阻塞吗

先说下结论：

+ css加载不会阻塞DOM树的解析
+ css加载会阻塞DOM树的渲染
+ css加载会阻塞后面js语句的执行
为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以下几种方法:
+ 使用CDN(因为CDN会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)
+ 对css进行压缩(可以用很多打包工具，比如webpack,gulp等，也可以通过开启gzip压缩)
+ 合理的使用缓存(设置cache-control,expires,以及E-tag都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决防范是在文件名字后面加一个版本号)
+ 减少http请求数，将多个css文件合并，或者是干脆直接写成内联样式（内联样式的一个缺点就是不能缓存）

**原理解析**
浏览器渲染的流程如下：

+ HTML解析文件，生成DOM Tree，解析CSS文件生成CSSOM Tree
+ 将Dom Tree和CSSOM Tree结合，生成Render Tree(渲染树)
+ 根据Render Tree渲染绘制，将像素渲染到屏幕上。
从流程我们可以看出来:

+ DOM解析和CSS解析是两个并行的进程，所以这也解释了为什么CSS加载不会阻塞DOM的解析。
+ 然而，由于Render Tree是依赖于DOM Tree和CSSOM Tree的，所以他必须等待到CSSOM Tree构建完成，也就是CSS资源加载完成(或者CSS资源加载失败)后，才能开始渲染。因此，CSS加载是会阻塞Dom的渲染的。
+ 由于js可能会操作之前的Dom节点和css样式，因此浏览器会维持html中css和js的顺序。因此，样式表会在后面的js执行前先加载执行完毕。所以css会阻塞后面js的执行。
