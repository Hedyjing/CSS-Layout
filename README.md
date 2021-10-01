# CSS-Layout
## 布局中的尺寸与位置
### 盒子模型
- 从内到外依次是content, padding, border, margin
- padding不能为负值, margin可以为负值
- 背景色会平铺到非margin的区域
> margin传递解决方案
1. 给父元素加border
2. 用padding替代
3. BFC
4. 弹性布局(最好的解决方案)
> margin上下叠加解决方案
1. 只给一个元素设置margin
2. 使用flex布局
3. BFC
### 块级盒子和内联盒子
> 块级盒子特性
- 独占一行
- 支持所有样式
- **不写宽度时和父元素宽度相同**
- 所占区域是矩形
> 内联盒子特性
- 不换行
- 不支持宽高属性
- 不写宽度的时候, 宽度由内容决定
- 所占区域不一定是矩形
- 内联标签之间有空隙
> 总结: 不要选择内联盒子做布局, 主要是强调作用
> 可以通过display属性判断盒子是块级的还是内联的
### 自适应盒模型
> 概念: 自适应盒模型指的是, 当盒子不设置宽度时, 盒模型相关组成部分的处理方式是如何的
- 子容器设置了宽度后, 设置padding, border, margin会溢出父元素, 可以用不设置子元素的width来解决
### 标准盒模型和怪异盒模型
> 标准模型中, 宽高是content的大小
> 怪异模型中, 宽度是所有可见宽度, border+padding+content
> 怪异盒子通过box-sizing属性设置, 值为: border-box
- 默认content-box: width, height -> content
- border-box: width, height -> content + padding + border
#### 怪异盒子应用
> 设置一些padding和border时向内扩张而不溢出
1. 量取尺寸时不用再去计算一些值, 当设置padding和border时, 不会改变视觉上的宽高
2. 百分比宽高时, 不溢出父元素的宽高

### 浮动样式
- 浮动会脱离文档流(body)
- 浮动会导致正常文档流的高度塌陷, 要清除浮动解决: 
  - clear属性
  - BFC
  - 空标签
  - .clearfix::after{} 伪类在
### 浮动特性
- 浮动只会影响后面的元素, 不会影响前面的元素
- 文本不会被浮动元素覆盖
- 具备内联盒子的特性: 宽度由内容决定
- 具备块级盒子的特性: 支持所有样式
- 浮动放不下会自动换行