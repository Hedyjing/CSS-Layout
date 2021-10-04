# CSS-Layout
## 布局中的尺寸与位置
### 盒子模型
- 从内到外依次是content, padding, border, margin
- padding不能为负值, margin可以为负值
- 背景色会平铺到非margin的区域
> margin传递: 会把父元素添加传递margin, 解决方案: 
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
### 定位样式
> position定位类型, top, right, bottom, left决定了该元素的最终位置
- static

  默认文档流的定位
- relative
  1. 在文档中的正常位置给偏移给定的值
  2. 不影响其他元素布局, 在正常文档流下
  3. 相对于自身进行偏移
- absolute
  1. 绝对定位脱离了文档流, 不占据空间
  2. 具备内联盒子的特性: 宽度由内容决定
  3. 具备块级盒子的特性: 支持所有样式
  4. 绝对定位元素相对于最近的非static祖先元素定位. 当这样的祖先元素不存在时, 则相对于可视区定位(不指定定位方式默认为static)
- fixed
  1. 固定定位与绝对定位相似, 但是会固定在可视区中, 以可视区域进行偏移
  2. 脱离文档流, 和绝对定位的特性相似
- sticky

  可以看作是relative和固定定位的混合, 元素在跨越特定阈值前为相对定位, 之后为绝对定位
> z-index
- 默认为0, 大的值在上面, 如果有嵌套, 则和以父元素的z-index为准

## flex弹性布局
> 概念: 弹性盒子是一种用于按行或列布局元素的一维布局方法(一行一列). 元素可以膨胀以填充额外的空间, 收缩以适应更小的空间

### 主轴于交叉轴
- 主轴默认水平从左到右排列
- 交叉轴默认垂直从上到下排列
- flex容器的属性
  1. flex-direction
    > 改变轴方向

      - row(默认)
      - row-reverse 主轴从右到左
      - column 主轴从上到下
      - column-reverse 主轴从下到上
  2. flex-wrap
    > 换行

      - nowarp(默认不换行)
      - wrap
      - wrap-reverse

      有几行就把容器平分成几分, 然后把这一行放在刚行的最顶端
      
      如果容器没有设置高度, 那么就不会平分, 一行挨着一行
  3. flex-flow
    > direction和wrap的简写, 比如: flex-flow: column wrap
  
  4. justify-content
    > 主轴对齐

      - flex-start(默认)
      - flex-end
      - center
      - space-around
        子项左右两边分配一样, 中间间隔是左右两边间隔的二倍
      - space-between
        左右两边无空隙
      - space-evenly
        所有空隙都相等      
  5. align-items
    > 不需要设置换行就可以生效
    > 交叉轴每一行中的对齐方式

      - stretch(默认)
      - flex-start
      - flex-end
      - center
      - baseline
        	项目的第一行文字的基线对齐
  6. align-content
    > 交叉轴,整体多行的对齐, 不换行时该属性不生效, 所以要设置flex-wrap属性

      - stretch(默认) 高度拉升效果
      - flex-start
      - flex-end
      - center
      - space-around
        行上下两边分配一样, 中间间隔是上下两边间隔的二倍
      - space-between
        上下两边无空隙
      - space-evenly
        所有空隙都相等    
- flex子项属性
  1. order
    > 默认值是0, 改变某一个flex子项的排序位置
  2. flex-grow
    > 占用剩余空间的比例, 默认值是0, 表示不占用剩余的空白间隙扩展自己的宽度

      - flex-grow:1 占满剩余的所有空间
      - flex-grow:0.5 多占剩余空间的一半
      - 大于等于1都会占满整个空间
      - 当多个元素时, 所有flex-grow的和加起来大于1时, 占满整个剩余空间, 按照比例给原色分配
  3. flex-shrink
    > 默认值是1, 表示flex容器空间不足时, 元素的收缩比例, 1就表示溢出的空间,
    
      - flex-shrink大于等于1才会不溢出, 小于1会溢出
  4. flex-basis
    > 默认值是auto, 指定了flex元素在主轴方向上的初始大小

    - 优先级大于width/height
    - 用来给宽高改变方向, 当主轴变化时自动改变方向
    - 可选值有, 100% auto 固定值 0
  5. flex
    > flex属性是flex-grow, flex-shrink, flex-basis的简写
  6. align-self
    > 默认值是auto, 控制单独某一个flex子项的垂直对齐方式
      
      - auto和父容器align-items的值一样
### 居中方案
- flex居中
- margin: auto
- 绝对定位50%
### 一些布局方案
  - 不定项居中
  - 均分列布局
    > 适用于移动端底部的导航
  - 子项分组布局
  - 等高布局
  - 两列&三列布局
  - sticky-footer布局
    利用flex-grow
  - 溢出项布局
    利用flex-shrink

## grid网格布局
  > 二维布局
  > grid容器属性

    - justify-items
      水平方向
    - align-items
      垂直方向
    - place-items
      简写
    以上三项默认值是stretch, 指定了子项在网格中的对齐方式
    ---------------------
    - justify-content
    - align-content
    - place-content
    以上三项默认值是stretch, 指定了所有网格整体在grid容器中的对齐方式
    ----------------------------
    - grid-auto-flow
      默认值为row
    - grid-auto-rows
    - grid-auto-columns
    以上三项指定隐式网格
    ----------------------
    - grid-template-rows
    - grid-template-columns
      基于网格行和列的维度, 去定义网格线的名称和网格轨道的尺寸大小
    - grid-template-areas
      使用命名方式定义网格区域, 需配合grid-area属性进行使用
    - grid-template
      是以上三个template的简写
    -------------------------
    - grid-row-gap
    - grid-column-gap
    - grid-gap
      以上三个用于设置元素行列之间的间隙大小, 推荐使用row-gap, column-gap, gap可以用在其他布局中
  > grid子项属性

    - grid-column-start
    - grid-column-end
    - grid-row-start
    - grid-row-end
    以上四项表示grid子项所占据的区域的起始和终止位置, 包括水平方向和垂直方向默认值为auto, 不写全的话后面的元素会在后面排列, 写上值的话后面的元素会自动填充空的区域
    - grid-row
    - grid-column
    - grid-area
    以上三项是grid-column/row-start/end 的简写
      - 指定区域的名字
      - grid-row-start, grid-column-start, grid-row-end, grid-column-end属性的缩写, 额外支持grid-templage-areas设置的网格名称
      位置不对应会自动填充
    -------------------------
    - justify-self
    - align-self
    - place-self
    跟place-item用法相同, 只不过是操作指定的子项

  > 网格方法

    - repeat()
      repeat()方法及auto-fill可选值, 指定可重复的数值
    - minmax()
      指定最小最大值