## line box(行框)
### 1.定义
前面在介绍IFC时，我们提到过line box的定义：包含IFC内部的所有子元素的虚拟矩形区域，形成的每一行，称为line box。由于它是矩形的，中文常见将之翻译为行框。
### 2.模型结构（七线谱）
line box的模型结构，形如七线谱，其中有六条重要的线：top线、text-top线、middle线、baseline线、text-bottom线和bottom线  
其中top线到text-top线的区域和bottom线到text-bottom的区域，又称为行半距（half-leading），两个行半距之和，为一个行距；text-top线到text-bottom线的区域，称之为内容区域（content-area）
### 3.行框高度的计算
行框的高度，即一行的top线和bottom线间的垂直距离，这个垂直距离为：上下两个行半距的高度和一个内容区域的高度之和。影响行框高度计算的因素来自两方面，一是自身line-height属性的设置，二是内部inline-level子元素的margin box高度的取值和line-height、vertical-align两个属性的设置。关于其计算规则，具体罗列如下：
- 一个元素的行框高度，可由该元素的line-height属性设置；
- 一个元素的行框高度，受不可置换（span、a、label等）的子元素的内容高度（text-top到text-bottom的垂直距离）影响（内容高度又受font-size属性和浏览器的解析规则影响，但主要由font-size决定；相同的font-size，在不同的浏览器，计算出来的内容高度也不一样，最终导致的行框高度也不一样）；
- 一个元素的行框高度，可由不可置换（span、a、label等）的子元素的line-height属性设置；
- 一个元素的行框高度，可由可置换行内元素（如img）或display属性为inline-block、inline-table的这一类inline-block-level子元素的margin box高度和vertical-align属性决定，当vertical-align为top或bottom时，行框的高度达到最小，刚好为子元素的margin box高度；
- 如果同时满足以上设置条件，那么行框的高度取最大值；
### 4.line-height和vertical-align
其实这两个属性的关系可由行框和行框内的inline-level元素来体现。line-height属性决定inline-level元素所在行框的高度，它是inline-level元素在一行内垂直方向上的显示范围；vertical-align属性则决定inline-level元素在一行内的垂直对齐方式，即决定inline-level元素在一行内垂直方向上的最终位置。下面我们来深入介绍这两个属性：
#### 4.1line-height属性
##### 4.1.1line-height属性的作用
line-height属性一般用于块级元素设置其内部每一行的高度，即默认行高；line-height属性也可以用于不可置换元素（如span、a）设置所在行框的高度。也就说，每一行计算出来的最终行高，既受父元素line-height属性的影响，也受子元素line-height属性的影响。
##### 4.1.2line-height属性的取值
line-height的取值有<length>、<number>、<percentage>和关键字normal（默认值）
##### 4.1.3line-height属性对元素高度的影响
当一个块元素不设置height，而且这个块元素仅有一行时，那么其height刚好等于line-height；  
当一个块元素不设置height，而且这个块元素有多行时，那么其height刚好等于每一行的line-height之和  
不可置换行内元素为单行时，其height等于text-top线到text-bottom线的距离，所以line-height的取值不会影响到其height，其height由font-size和浏览器的默认解析机制决定  
不可置换元素为多行时，其height等于第一行的text-top线到最后一行的text-bottom线的距离，此时line-height的取值就会影响到其height，其height＝line-height * 行数 - (line-height - 每一行text-top线到text-bottom的距离)，即height＝line-height * 行数 - 2 * half-heading  
不可置换的行内子元素的line-height属性，可以决定所在行框的高度;如果一个父元素不设置height，那么其height为所有行的高度之和；  
#### vertical-align属性
vertical-align的作用之一：就是用于设置inline-level元素自身在“行框”内的垂直对齐方式，其控制范围在一行内。较常用的值有top、middle、baseline（默认值）和bottom，不常用的有text-top、text-bottom、sub和super，几乎不用的有<length>和<percentage>。
