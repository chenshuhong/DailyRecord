## 1.布局基础要点
### 1.1 css标准盒模型，即w3c盒模型
CSS盒模型，它由内到外、被四条边界Content edge、Padding edge、Border edge和Margin edge划分为四个区域：Content area、Padding area、Border area和Margin area，在形状上，Content area（又称content-box）是实心矩形，其余是空心环形（空心部分是Content area）
Content area，是当前元素用来容纳所有子孙元素
Padding area，是当前元素用来隔离自身和子孙元素
Border area是当前元素用来显示自身的轮廓
Margin area，是当前元素用来隔离自身和相邻元素
而每个区域的尺寸，又分别由特定的CSS属性来控制，这些CSS尺寸属性（width、height、padding、border和margin），相当于一个个hook，我们可以通过设置这些“hook”来达到调整元素尺寸的目的。
