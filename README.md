# CSS3选择器
[css3笔记](https://github.com/yangxuefeng753/yxf/blob/master/Css3%E7%AC%94%E8%AE%B0.md)
## 兄弟选择器：
1. 相邻兄弟选择器
	匹配的是相邻兄弟元素
	匹配当前元素的【后面的一个】元素，前提是两个元素必须有一个父元素
	语法：selector1+selector2
2. 通用兄弟选择器
	匹配当前元素【后面的所有】兄弟元素
	语法：selector1~selector2
## 属性选择器;
1. [属性名]   
>	匹配带有指定属性的元素
2. 元素名[属性名]
>	例如：p[id] 匹配所有包含id属性的p元素
3. 元素名[属性1][属性2]...
>	匹配既包含属性1又包含属性2的指定元素
>	例如：div[id][class] - 匹配包含id属性和class属性的div元素
4. 元素名[属性=值]
>	例如：input[type=text] - 匹配所有type属性值为text的input元素  - 匹配输入框
5. 元素[属性~=值]
>	匹配指定的属性值中，包含【独立值】单词的元素
6. 元素[属性*=值]
>	匹配指定的属性中，属性值中包含【值】的元素
7. 元素[属性^=值]  
>	属性值以【值】开头的元素	
8. 元素[属性$=值]  
>	属性值以【值】结尾的元素
## 目标伪类选择器：用于匹配当前活动的*锚点*元素
>语法： :target
元素状态伪类选择器：表单元素居多
	:enabled 匹配每个已启用的元素
	:disabled 匹配每个被禁用的元素
	:checked 匹配每个已被选中的input元素（单选框，复选框）
```
p:first-child{
/*选中作为【第一个子元素】存在的指定p元素*/
	color:red;
}
p:last-child{
/*选中作为【最后一个子元素】存在的指定元素*/
	color:blue;
}
```
:only-child 匹配其父元素中唯一的子元素
```
<p>
	<a>百度</a>
</p>
```
> a:only-child 可以匹配
```
<p>
	<a>百度</a>
	<a>职坐标</a>
</p>
```
a:only-child 不能匹配
语法： :not(selector)
	input:not([type=text])  选中所有type不为text的input元素
## 伪元素选择器
>特点:获取指定元素中某一部分文本而用的。
1、:first-letter
>用于选取指定选择器（元素）的首字母
2、:first-line
>用于选取指定选择器（元素）的首行文本
3、::selection
>匹配被用户选取的部分
## 内容生成
>通过CSS向已有的元素中增加文本（图片内容）
### 选择器：
>	1. :before  向匹配的元素之前增加生成的内容，定位到元素的开始位置
	2. :after   向匹配的元素之后增加生成的内容，定位到元素的结束位置
>属性：content
```
div:before{
	content:"生成内容"  / url(图片路径) /  计数器
}
```
---
#### 如何解决：子元素margin-top/margin-bottom 越界问题
解决方案：
1. 给父元素加border——有副作用
2. 给父元素加overflow:hidden——有副作用
3. 给父元素加前置内容生成" ",显示样式为table——无任何副作用
示例如下：
```
越界元素:before{
	content:" ";
	display: table;
}
```
---
#### 如何解决：
1. 所有的子元素浮动对父元素(父元素塌陷现象)
2. 后续元素造成的影响（布局乱套-浮动元素会覆盖未做浮动的元素 字围现象）
解决方案：
1. 给父元素加height——有局限性
2. 给父元素加overflow:hidden——有副作用
3. 给父元素加子元素 clear:both——语义有问题
4. 给父元素添加后置的内容生成" ",显示样式为table，清除浮动clear:both——无任何副作用
示例如下：
```
元素:after{
	content:" ";
	display: table;
	clear:both;
}
```
---
**计数器： 通过css定义，在其他元素中可以使用该计数器生成的数字属性：**
1. counter-reset  用于初始化一个计数器并设置初始值
注意：如果不设置初始值，默认从0开始，设置的值可以是正，负数
>语法：{counter-reset:counter1 10}
>     {counter-reset:counter1 10 counter2 100}
---
> 关于计数器的用法：
如果整个页面任何一个元素都能使用该计数器，那么必须把计数器定义到body元素中，切忌将计数器定义到某一个元素中。因为如果把计数器定义到某一个元素中那么计数器永远都是初始值
```
body{
	counter-reset:c1 10 c2 20;
}
```
2. counter-increment:设置计数器的名称和步长（增量）
```
div{
	counter-increment:c1 10;
}
```
3. 调用计数器（函数），counter(counterName)
counterName - 计数器的名称
>作用：使用计数器创建出来的数字文本
