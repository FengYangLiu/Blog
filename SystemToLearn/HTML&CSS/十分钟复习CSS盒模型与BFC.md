# css盒模型与BFC
1. 本文为收集整理总结网上资源
2. 旨在系统复习css盒模型与bfc
3. 节省复习时间
4. 阅读10分钟

## 什么是盒模型
> 每一个文档中，每个元素都被表示为一个矩形的盒子,它都会具有内容区、padding、border、margin

![盒模型](https://developer.mozilla.org/files/72/boxmodel%20(1).png)


### 盒模型主要分两种

1. 标准盒模型
2. IE盒模型(怪异盒模型)

两者的区别：
1. 标准盒模型的宽高则为内容区域的宽高
2. IE盒模型则宽高为 border + padding + 内容区


![两种盒模型](http://oqz6fw5uj.bkt.clouddn.com//18-6-30/83764866.jpg)


### 如何切换盒子模型?

> 使用box-sizing来进行切换

1. border-box 切换为IE盒模型
2. content-box 默认属性 为标准模式


## 盒模型的边距重叠
 主要分三种重叠， 重叠规则：一大一小取最大,一正一负取和
1. 相邻元素之间的重叠
2. 父子嵌套的重叠
3. 空的块级元素

### 1.相邻元素之间

![相邻元素之间的重叠](http://www.w3school.com.cn/i/ct_css_margin_collapsing_example_1.gif)

```
// css
* {
  margin:0;
  padding:0;
  border:0;
}

#d1 {
  width:100px;
  height:100px;
  margin-top:20px;
  margin-bottom:20px;
  background-color:red;
}

#d2 {
  width:100px;
  height:100px;
  margin-top:10px;
  background-color:blue;
}

// html
<div id="d1">
</div>

<div id="d2">
</div>

```

### 2.父子嵌套重叠
![父子重叠](http://www.w3school.com.cn/i/ct_css_margin_collapsing_example_2.gif)

```
// css

* {
  margin:0;
  padding:0;
  border:0;
}

#outer {
  width:300px;
  height:300px;
  background-color:red;
  margin-top:20px;
}

#inner {
  width:50px;
  height:50px;
  background-color:blue;
  margin-top:10px;
}

// html 
<div id="outer">
  <div id="inner">
  </div>
</div>


```

### 3.空的块级元素
![空的块级元素](http://www.w3school.com.cn/i/ct_css_margin_collapsing_example_3.gif)

![空的块级元素与相邻元素](http://www.w3school.com.cn/i/ct_css_margin_collapsing_example_4.gif)


## BFC (边距重叠处理方案)

### 什么是BFC
> 块格式化上下文（Block Formatting Context，BFC） 是Web页面的可视化CSS渲染的一部分，是布局过程中生成块级盒子的区域，也是浮动元素与其他元素的交互限定区域。


#### 块级盒
> 每个块级盒子都会参与块格式化上下文（block formatting context）的创建，而每个块级元素都会至少生成一个块级盒子，即主块级盒子（principal block-level box）

有时候定义了一个块级元素,设置了宽高虽然占据一行在chrome下会发现除了元素以外的一个包裹盒子像margin一样的颜色,这个就是块级盒;
![块级盒](http://oqz6fw5uj.bkt.clouddn.com//18-6-30/28250527.jpg)

每一个块级元素会生成一个
#### 块级盒子的几种特性
1. 块级盒会在垂直方向，一个接一个地放置，每个盒子水平占满整个容器空间
2. 块级盒的垂直方向距离由上下 margin 决定，同属于一个 BFC 中的两个或以上块级盒的相接的 margin 会发生重叠
3. BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
4. 计算 BFC 的高度时，浮动元素也参与计算

#### 如何创建BFC?
1. 根元素或包含根元素的元素
2. 浮动元素（元素的 float 不是 none）
3. 绝对定位元素（元素的 position 为 absolute 或 fixed）
4. overflow 值不为 visible 的块元素
5. display的值为inline-block、table-cell、table-caption

#### BFC的应用？
1. 清除浮动
2. 布局
3. 解决块级盒边距重叠

##### 布局
![布局](http://oqz6fw5uj.bkt.clouddn.com//18-6-30/51693033.jpg)

原理就是触发BFC重新计算元素尺寸

```
// html
<div></div>
<p>
	开始清除浮动清除浮动清除浮动....
</p>

// css
	*{
		margin: 0;
		padding: 0;
	}
		div{
			width: 100px;
			height: 100px;
			background: green;
			float: left;
		}
		p{
			background: #f0faa5;
			overflow: hidden;
		}

```

##### 清除浮动
![清除浮动，计算高度](http://oqz6fw5uj.bkt.clouddn.com//18-6-30/23937932.jpg)

```
// html
<section class="divwrap">
		<div class="div1">
			float1	
		</div>
		<div class="div2">
			float2
		</div>
	</section>
	
//css
*{
    margin: 0;
    padding: 0;
}
div{
	width: 100px;
	height: 100px;
	background: green;
	float: left;
}
.div2{
	background: red;
}
.divwrap{
	border:3px solid #000;
	overflow: hidden;
}
```

##### 解决边距重叠
![解决上下边距问题](http://oqz6fw5uj.bkt.clouddn.com//18-6-30/148375.jpg)

```
// html
<div class="BFC">
    	<p>
	    	hello world
	    </p>
	</div>

	<p>
	    hello world
	</p>
	<p>
	    hello world
	</p>

// css
    *{
		margin: 0;
		padding: 0;
	}
	.BFC{
	    overflow:hidden;
	}
	p{
	    color:black;
	    background:#D499B9;
	    line-height:100px;
	    width:200px;
	    text-align:center;
	    margin:50px;
	}
	
```

## 最后
> 最后感谢每个阅读的小伙伴与所有写博客分享的人

## 参考资料

1. [MDN-CSS盒模型](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
2. [MDN-外边距合并](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
3. [w3school-外边距重叠](http://www.w3school.com.cn/css/css_margin_collapsing.asp)
4. [MDN-视觉格式化模型](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Visual_formatting_model)
5. [MDN-块格式化上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
6. [芋头君-CSS之BFC详解](http://www.html-js.com/article/1866)
7. [OBKoro1-布局概念 关于CSS-BFC深入理解](https://juejin.im/post/5909db2fda2f60005d2093db)


