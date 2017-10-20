# CSS-Sticky-Footer


## Intro

在网页设计中，存在一个相当古老但又相当常见的问题：有一个具有块级样式的页脚,当页面内容足够长时它一切正常,如图所示（ 图片来源：[ituring.com](http://www.ituring.com.cn/figures/2016/CSS/16.d07z.023.png) ）：  

![](http://www.ituring.com.cn/figures/2016/CSS/16.d07z.023.png)  

而当页面较短时就会出现问题,如图所示（ 图片来源：[ituring.com](http://www.ituring.com.cn/figures/2016/CSS/16.d07z.024.png) ）：  

![](http://www.ituring.com.cn/figures/2016/CSS/16.d07z.024.png)  
此时的问题在于，页脚不能像我们期望中那样“紧贴”在视口的最底部，而是紧跟在内容的下方。  **CSS Sticky Footer**可以帮我们解决这个问题。


## Features

- Responsive
- Without JavaScript

## Usage

1. 由[Ryan Faits](http://ryanfait.com/resources/footer-stick-to-bottom-of-page/)创造的footer布局  
	*缺点：HTML代码中会有一个空的div层。严格来说，是不符合语义网代码标准。*
	
	HTML代码:
	
	```html
	<div class="page-wrap">
		Content!
		<div class="push"></div>
	</div>
	<div class="footer">
		I'm the Sticky Footer.
	</div>
	```
	CSS代码:
	
	```css
	* {
		margin: 0;
	}
	html,
	body {
		height: 100%;
	}
	.page-wrap {
		min-height: 100%;
		/* equal to footer height */
		margin-bottom: -100px;
	}
	.push {
		/* equal to footer height */
		height: 100px;
	}
	.footer {
		height: 100px;
		text-align: center;
		color: #fff;
		background: #333;
		line-height: 100px;
	}
	```
2. 利用after伪元素替换上述方法中的空div  
	*缺点：内容区域的高度会超出body的高度*  
	
	HTML代码:
	
	```html
	<div class="page-wrap">
		Content!
	</div>
	<div class="footer">
		I'm the Sticky Footer.
	</div>
	```
	CSS代码:
	
	```css
	* {
		margin: 0;
	}
	html,
	body {
		height: 100%;
	}
	.page-wrap {
		min-height: 100%;
		/* equal to footer height */
		margin-bottom: -100px;
	}
	.page-wrap:after {
		display: block;
		content: "";
	}
	.footer,
		.page-wrap:after {
		height: 100px;
	}
	.footer {
		text-align: center;
		color: #fff;
		background: #333;
		line-height: 100px;
	}
	```
3. 目前较为完美的css2.1解决方案

	HTML代码:
	
	```html
	<div class="page-wrap">
		<div class="centent">
			Content!
		</div>
	</div>
	<div class="footer">
		I'm the Sticky Footer.
	</div>
	```
	CSS代码:
	
	```css
	* {
		margin: 0;
	}
	html,
	body {
		height: 100%;
	}
	.page-wrap {
		min-height: 100%;
	}
	.content {
		/* equal to footer height */
		padding-bottom: 100px;
	}
	.footer {
		position: relative;
		height: 100px;
		/* equal to footer height */
		margin-top: -100px;
		text-align: center;
		color: #fff;
		background: #333;
		line-height: 100px;
	}
	```
4. 通过CSS3的vh（ viewpoint height ）来计算整体视窗的高度（ 1vh等于视窗高度的1% ），然后减去底部footer的高度，从而求得内容区域的最小高度。
	*缺点：不支持低版本浏览器，且它不仅要求我们确保页脚内的文本永远不会折行，而且每当我们改变页脚的尺寸时，都需要跟着调整 min-height 值*
	
	HTML代码:
	
	```html
	<div class="page-wrap">
		Content!
	</div>
	<div class="footer">
		I'm the Sticky Footer.
	</div>
	```
	
	CSS代码:
	
	```css
	* {
		margin: 0;
		padding: 0;
	}
	.page-wrap {
		min-height: calc(100vh - 100px);
	}
	.footer {
		background: #333;
		color: #fff;
		line-height: 100px;
		text-align: center;
	}
	```
5. flex布局（ footer的高度不需要固定 ）  
	*缺点：不支持低版本浏览器，仅支持chrome 21+，Opera 12.1+，Firefox 22+，Safari 6.1+，IE 10+*
	
	HTML代码:
	
	```html
	<div class="page-wrap">
		Content!
	</div>
	<div class="footer">
		I'm the Sticky Footer.
	</div>
	```
	CSS代码:
	
	```css
	* {
		margin: 0;
	}
	body {
		display: flex;
		flex-flow: column;
		min-height: 100vh;
	}
	.page-wrap {
		flex: 1;
	}
	.footer {
		background: #333;
		color: #fff;
		line-height: 100px;
		text-align: center;
	}
	```