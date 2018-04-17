## 格式化上下文 Formatting Context
格式化上下文，它指的是具有某种CSS格式化规则（布局规则）的上下文环境，在这个上下文环境内的所有子元素，都将根据其特定的CSS格式化规则来进行排列。
### 1.BFC
#### 1.1定义
BFC, 全称是block formatting context，它是一个独立封闭的渲染区域，在这个区域内的所有元素，从区域的顶部起，一个接一个地根据自身的布局特性进行排列：在这个区域内的块级元素 ，按从上到下的顺序显示，相邻的块级元素可以使用margin隔离，但在垂直方向上相邻的块级元素会发生margin合并；在这个区域内的inline-level或inline-level-block元素，则按从左到右的顺序显示（W3C组织说BFC内部的元素都是一个接一个地垂直显示，我觉得不是很严格，因为BFC内部也可以容纳inline-level和inline-level-block元素，所以这里我的解释和W3C还是稍微有一些不一样）。具有BFC格式化环境的元素，我们称之为BFC元素，可以说，BFC定义了BFC元素content区域的渲染规则。
#### 1.2创建方式
- 根元素或其它包含它的元素
- 浮动元素（元素的float不是none）
- 绝对定位元素（position:absolute）
- 固定定位元素（position：fixed）
- 内联块（display:inline-block）
- 表格单元格（display:table-cell）
- 表格标题（display:table-caption）
- overflow不为visible的块元素
- display:flow-root
- contain为以下值得元素：layout，content，strict
- 弹性项（display：flex或inline-flex元素的子元素）
- 网格项（display:grid或inline-grid元素的子元素）
- 多列容器（元素的column-count或column-width不为auto，包括column-count：1的元素）
-column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中。
#### 1.3特性
1.对应一个独立、封闭的渲染区域，子元素的CSS样式不会影响BFC元素外部；  
2.浮动子元素参与BFC父元素的高度计算，也就是BFC元素能够识别浮动元素（将元素声明为BFC元素，也是clearfix解决父元素塌陷问题的一种常用方法）；  
3.占据文档流的BFC元素（可使用overflow: auto创建），能够识别浮动的兄弟元素；  
4.占据文档流的BFC元素（可使用overflow: auto创建），width为auto时，会占满当前行的剩余宽度；
## 2.IFC
### 2.1定义
IFC, 全称是inline formatting context，其内部的元素，在水平方向上，一个接一个地显示；在垂直方向上，每个元素可以设置不同的对齐方式；IFC内部的元素，被一行行的矩形框所包含，这些虚拟的矩形框，我们称为行框（line box）。IFC的作用区域，可以看成是包含其所有子元素的行框组成的矩形区域。
### 2.2创建方式
和BFC相比，它的创建方式是被动的、隐式的，是由所包含的子元素来创建：只有在一个区域内仅包含可水平排列的元素时才会生成，这些子元素可以是文本、inline-level元素或inline-block-level元素。
### 2.3特性
- IFC内部的元素，按从左到右、从上到下的顺序排布；
- IFC内部的每个元素，都可以通过设置vertical-align属性，来调整在垂直方向上的对齐；
- 包含这些内部元素的矩形区域，形成的每一行，被称为line box（行框，后面会详细介绍）；
## FFC和GFC
FFC（flex formatting context）和GFC（grid formatting context），分别是flex布局和grid布局的内容
