---
title: CSS
date: 2020-05-22 13:44:57
tags:
---
## 盒模型
####  标准盒子模型： box-sizing: content-box
{ width: 300px, height:300px, padding: 50px, border: 50px }

content = width = 300
padding = 50
border = 50
total = 500

####  IE盒子模型： box-sizing: border-box
{ width: 300px, height:300px, padding: 50px, border: 50px }

width = 300 = content + padding * 2 + border * 2

content = 100px


## Flex布局
**由Container（父元素）与Item（子元素）组成**
**Flex下overflow失效问题：在需要overflow的地方加上width=0**
</br>
Container{display: flex}
#### flex-direction (横向默认)
flex-direction: row 主轴为横向 row-reverse 反row
			</br>column 主轴为竖向 column-reverse 反column
			
#### flex-wrap

让items可以换行
	
flex-wrap: nowrap(默认)
		</br>wrap（可换行）
		</br>wrap-reverse（反向）
		
#### flex-flow

direction与wrap的组合

flex-flow：row wrap；

#### justify-content

**定义了item在主轴上的对齐方式**
</br> justify-content：center 居中</br> flex-start 默认值。项目位于容器的开头 </br>flex-end 项目位于容器的结尾 </br>space-between 项目位于各行之间留有空白的容器内**两边有空**</br>space-around	项目位于各行之前、之间、之后都留有空白的容器内**两边没空**

#### align-items

**定义了item在侧轴上的对齐方式（单行） 多行改为align-content 单个改为align-self（写的地方由container改成item）**	
stretch	
默认值。元素被拉伸以适应容器。

如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。

center	
元素位于容器的中心。

弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。

flex-start	
元素位于容器的开头。

弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。

flex-end	
元素位于容器的结尾。

弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。

baseline	
元素位于容器的基线上。

如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。

####  flex-grow

**定义项目的放大比例，默认为0，就是即使有剩余空间也不会放大 作用在item上，后面跟的值表示比例**

flex-grow：1 2 3  表示占六分之一，三分之一，二分之一

####  flex-shrink

**定义项目的缩小比例，默认为1，就是会随着container而缩小 作用在item上，后面跟的值表示比例**

flex-shrink：1 2 3  表示占六分之一，三分之一，二分之一

####  flex-basis

**定义了在分配多余空间之前，item占据的主轴空间**

类似定义一个item的宽度（row）

### flex

**前3个属性的集合**

默认 0 1 auto

## Grid
#### grid-template-rows/ grid-template-columns （用于container）
用于设定竖直/水平方向的划分
grid-template-rows：100px 100px 100px 100px 100px

 1fr 1fr 1fr 1fr 1fr **fr指的份数**</br>
= repeat（5，1fr）**不适用于grid-template-areas**
#### grid-template-areas
grid-template-areas： “header header header header header”
“. div div div .”**第一行grid中1-5被命名为header， 第二行2-4被命名为div**

#### row-gap/column-gap
定义行与行，列与列之间的距离

#### grid-row / grid-column（用于cell） grid-area
语法： grid-row：1/3 -> 占row的1到3格
				1/span 2->从1开始延伸2格	
grid-area： 1/1/4/3 -> row1 column1 row2 column2(左上角到右下角)


## 单位

#### em
针对父元素的font-size 1em=父元素的font-size大小

#### rem
针对根元素（html）在谷歌默认是16px

移动端多用rem，便于计算 图片的宽高，字体大小都用rem

