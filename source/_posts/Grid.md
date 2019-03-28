---

title: CSS  Grid
date: 2018-12-31 10:53:15
tags:
	- css

---

这仅是一篇自学笔记。

<!-- more -->

使用`display: grid` 将容器定义为一个 grid(网格) 布局，使用 `grid-template-columns` 和 `grid-template-rows` 设置列和行的尺寸大小，然后通过 `grid-column` 和 `grid-row` 将其子元素放入这个网格中。

#### 术语说明
- 网络容器（Grid Container）
- 网格项（Grid Item）：直接子元素
- 网格线（Grid Line）：仅可以垂直的“列网格线column grid lines”，也可以是水平的“行网格线row gird lines”。
- 网格轨道（Grid Track）：网格线之间的空间。
- 网格单元格（Grid Cell）网格线分割独立出来的空间。
- 网格区域（Grid Area）：任意数量网格单元格组成的区域。

#### 网格容器(Grid Container) 属性
- display
    - grid ：生成一个块级网格
    - inline-grid ：生成一个内联网格

##### 定义网格数量及尺寸，以及位置

- grid-template-columns
- grid-template-rows
- grid-template-areas
- grid-template （简写）

##### 定义网格间隔
- grid-column-gap
- grid-row-gap
- grid-gap （简写）

##### 定义单元格对齐排版
- justify-items
- align-items
- place-items （简写）
- justify-content
- align-content
- place-content （简写）

##### 定义隐式单元格
- grid-auto-columns
- grid-auto-rows
- grid-auto-flow（？）

#### 网格项(Grid Items) 属性

##### 单元格定位（）
- grid-column-start
- grid-column-end
- grid-row-start
- grid-row-end
- grid-column （简写）
- grid-row （简写）
- grid-area （二次简写）

##### 单元格对齐排版
- justify-self
- align-self
- place-self （简写）


#### 简单使用

运用 `display: grid` / `grid-template-columns` / `grid-template-rows` 即可完成简单的布局：

```html
<div class="container">
  <div>1-1</div>
  <div>1-2</div>
  <div>1-3</div>
  <div>2-1</div>
  <div>2-2</div>
  <div>2-3</div>
  <div>3-1</div>
  <div>3-2</div>
  <div>3-3</div>
</div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  
  grid-template-columns: 1fr 2fr 3fr;
  grid-template-rows: 100px 100px auto;
}

.container div {
  background: #eee;
  text-align: center;
  color: #aaa;
  line-height: 100px;
  margin: 1px;
}
```

效果如下：

![image](37E67404BE6A46659A624CD4CB52C321)


#### 自动创建重复单元格

在定义 `grid-template-columns` 和 `grid-template-rows` 时，可以使用一个类似函数的定义语句 `repeat()`。

它的有两个参数：
- <repeat-value>  重复次数，或自动补充
- <template-value> 单元格定义值，同 `grid-template-*` 的值一样。

示例：

```html
<div class="container"></div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: 100px;
}

```

效果如下：

![image](CC3AA96A35D6410C8A90552CB17E241C)


##### 自动补充

使用 `auto-fill` 和 `auto-fit` 来自动计算单元格数量。

**auto-fill** 是计算使用尺寸除以单元格尺寸得出单元格数量，修改下css代码如下：

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: repeat(auto-fill, 90px);
  grid-template-rows: 100px;
}
```

![image](C792B691C9944302B842753AB3E31B83)

如上图，会确保不超出容器的前提下自动设置单元格数量。


**auto-fit** 是根据元素数量，判断需要多少个单元格。需要做一个对比，才能更直观的了解。

我们定义固定宽度的三列，超出数量的元素自动换行，css和效果如下：

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: 100px 100px 100px;
}
```

![image](25C21F39BE8B4C108A88D1F6241E388B)

然后我们再修改为，固定单元格宽度，然后根据元素数量自动创建单元格，如下：

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: repeat(auto-fit, 100px);
}
```

![image](063EA56711D04F7CAD2C0F583597BF3F)


---

#### 定义灵活尺寸的单元格

使用函数 `minmax()` 指定尺寸范围，它接受两个参数：

- min value
- max value

均支持固定宽度，和 `auto`。此函数在定义“隐式单元格”时相对有用。

---

#### 设置间隔

也就是所谓的“网格线”，在容器元素上使用 `grid-column-gap` 和 `grid-row-gap` 这两个属性，且他们只作用网格之间。

**Chrome 68+，Safari 11.2 Release 50+ 和Opera 54+ 浏览器支持 `column-gap` 和 `row-gap` 写法。**

例子如下：

```html
<div class="container">
  <div>1-1</div>
  <div>1-2</div>
  <div>1-3</div>
  <div>2-1</div>
  <div>2-2</div>
  <div>2-3</div>
  <div>3-1</div>
  <div>3-2</div>
  <div>3-3</div>
</div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: 100px 100px auto;
  grid-template-rows: 100px 100px auto;
  grid-column-gap: 10px;
  grid-row-gap: 10px;
}

.container div {
  background: #ddd;
  text-align: center;
  color: #aaa;
  line-height: 100px;
}
```

效果如下：

![image](056031E51EC34F0397C4F902B2AE8F49)

可以使用缩写方式 `grid-gap`，格式如下：

> grid-gap: <grid-row-gap> <grid-column-gap>;

```css
.container {
    grid-gap: 10px 10px;
    /* or */
    grid-gap: 10px;
}
```

**Chrome 68+，Safari 11.2 Release 50+ 和Opera 54+ 浏览器支持 `gap` 写法。**

---

#### 子元素对齐排版

分别使用容器属性 `justify-items` 和 `align-items`，一个是行对齐方式，另个是列对齐方式。

他们的值是一样的，都是在单元格内的对齐方式，分别是：

- start ：左对齐
- end ：右对齐
- center ：居中对齐
- stretch ：填充单元格宽高（默认）

其中 `start` `end` `center` 都不会影响子元素的大小。如果要在子元素内设置自己的对齐方式，则使用 `justify-self` 和 `align-self`。

还可以使用 `place-item` 合并两个属性的写法：

> place-items: <align-items> <justify-items>;

**目前Edge不支持 `place-items` 属性。**


---

#### 对齐排版

除了子元素的对齐方式，也可以对子元素的容器 “单元格” 进行排版，属性分别是 `justify-content` 和 `align-content`，一样是行和列的定义，同样有 `place-content` 合并两个属性的方式。

> place-content: <align-content> <justify-content>;

当在 `-columns` 和 `-rows` 两个属性中使用 `auto` 这个值时，默认会进行填充剩余部分 `stretch`。除了这个值，还有其他的选项：

- start
- end
- center
- stretch

以上属性和 `justify-items` 完全一样，除此之外还有，他们均不会控制单元格的大小：

- space-betweed ：利用剩余空间均匀设置每个单元格的间隔
- space-around ：同 `space-betweed`效果，且两侧留间隔的一半宽度。
- space-evenly ：同 `space-betweed`效果，且两侧留间隔宽度。

```html
<!-- // 同上 -->
```
```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto auto;
  grid-gap: 10px;
  
  /* 添加了此属性 */
  justify-content: start;
}

.container div {
  background: #ddd;
  text-align: center;
  color: #aaa;
  width: 100px;
  line-height: 100px;
}
```

演示 `justify-content: start` 值效果：

![image](4D9754F6A36C480DB1FBACE40FC2FACF)

默认 `justify-content: stretch` 效果：

![image](A5407D6B1BAE4C609F623A8387899164)

使用 `justify-content: space-between` 效果：

![image](430FAB7755BE40F9B404AB5B15D4EB21)

使用 `place-content: center` 效果：

![image](F85BD32E596D4864BB270B5973762CF6)

##### 单元格自己对齐

使用 `justify-self` 和 `align-self` 定义单元格自己的对齐方式，请求参数同容器对齐一样，以及这两个属性的简写 `place-self`.

---

#### 元素维度控制位置

容器下的元素，我们可以称之为“网格项”。

> **注：float, display: inline-block, display: table-cell, vertical-align, column-\* 属性对网格项无效。**

在子元素上使用 `grid-column-start`， `grid-column-end`， `grid-row-start`， `grid-row-end` 这四个属性来控制位置。

它们接受的值一样，分别是：

- <line> 网格线的编号
- span <number> 跨越网格轨道的数量
- span <name> 跨越网格名称
- auto 自动方式，

通过示例来更好的演示：

```html
<div class="container">
  <div class="box">.box</div>
</div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  /* 容器定义 */
  grid-template-columns: 100px 100px 100px auto;
  grid-template-rows: 100px 100px 100px auto;
  grid-gap: 10px;
}

.box {
  background: #ccc;
  text-align: center;
  color: #aaa;
  line-height: 100px;
  
  /* 元素的行位置定义 */
  grid-column-start: 2;
  grid-column-end: 4;
  
  /* 元素的列位置定义 */
  grid-row-start: 2;
  grid-row-end: 4;
}
```

先看下单元格的布局效果如下：

![image](F3F3574E5B164966949BDA96193A0B53)

元素设置定位后的效果：

![image](8B06E7691C254CEFBB413092AEB02D95)

通过效果可以得知，单元格会有自己的编号，从1开始的递增值，这里行和列，分别是1到4。所占位置包含 -start，但不含 -end。如上仅占位了行 2和3。

当只设置 `-start` 或 `-end` 时，会自动补充。
当 `-start` 为3时，占位第3行：

![image](38E15674916040E9BD527DF743210714)

当 `-end` 为3时，占位第2行：

![image](8281F03A5CB24177943CE761BDBC9FE9)


##### 简写方式：

使用 `grid-column` 和 `grid-row` 可以简写带 `-start` 和 `-end` 的定义。

书写方式：

> grid-column/grid-row: <start-line> / <end-line>;

刚刚的书写可以简化成：

```css
.box{
  ...
  
  grid-column: 2/4;
  grid-row: 2/4;
}
```

##### 轻松实现复杂布局

针对复杂的布局，使用单元格定位方式，可以轻松实现，例如效果：

![image](91538E02E1444F9EBF0F354222706A5B)

```html
<div class="container">
  <div class="box box-a">.box-a</div>
  <div class="box">.box-b</div>
  <div class="box box-c">.box-c</div>
</div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr  1fr;
  grid-gap: 10px;
}

.box {
  background: #ccc;
  text-align: center;
  color: #aaa;
}

/* 占 2*3 的空间 */
.box-a {
  grid-row: 1/4;
  grid-column: 1/3;
}

/* 占 1*2 的空间 */
.box-c {
  grid-row: 2/4;
}
```


---

#### 超出单元格外的布局

当我们使用 `grid-template-columns` 和 `-rows` 时，用于确定行和列的单元格数量时，我们的子元素数量需要小于或等于。但当元素大于单元格数量时，或者使用元素定位时（grid-column或grid-row），就会超出我们的预计，导致布局不可控了。

当然按理这种情况应该是可以被避免的，但是不能排除此场景。

我们用例子来演示一下：

```html
<div class="container">
  <div class="box">.box</div>
</div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  /* 列单元格有所修改：仅三列 */
  grid-template-columns: 50px 50px 50px;
  grid-template-rows: 100px 100px 100px auto;
  grid-gap: 10px;
}

.box {
  background: #ccc;
  text-align: center;
  color: #aaa;
  
  /* 定位到不存在的单元格位置时 */
  grid-column-start: 5;
}
```

先看下单元格布局：

![image](E09E27B0919A4160914E462A2721B4AC)

可以发现，第4和5列是自动生成的，且他们的宽度是等分的。如果按着这个规则，我们设置 `grid-column-start` 为 6 时，会自动生成 3 个等分的单元格：


针对这种情况提供了 `grid-auto-columns` 和 `grid-auto-rows`，可以称之为“隐式网格轨道”。

> grid-auto-columns/grid-auto-rows: <track-size>;

<track-size> 可以是长度值，百分比，空间分数（fr）。

针对上面的问题，我们可以这么设置：

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  background: #eee;
  
  grid-template-columns: 50px 50px 50px;
  grid-template-rows: 100px 100px 100px auto;
  grid-gap: 10px;
  
  /* 添加代码 */
  grid-auto-columns: 50px;
}

.box {
  background: #ccc;
  text-align: center;
  color: #aaa;
  
  grid-column-start: 5;
}
```

效果：

![image](7FC58460E07C4D319B3C02B06597B777)


---

#### 可视化结构

在单元格上使用 `grid-area` ，然后在容器上使用 `grid-template-areas` 将单元格与容器的指定位置的行和列进行关联。

**注：`grid-area` 的值非字符串，`grid-template-areas` 中占多行或多列时，需要重复名称，对于空格使用 `.` 占位。**

> grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>

示例如下：

```html
<div class="container">
  <div class="header">header</div>
  <div class="sidebar">sidebar</div>
  <div class="main">main</div>
  <div class="footer">footer</div>
</div>
```

```css
.container {
  width: 500px;
  height: 500px;
  display: grid;
  
  grid-template-columns: 100px auto;
  grid-template-rows: 100px auto 100px;
  grid-template-areas: 
    "header header"
    "sidebar main"
    "footer footer"
}

.container div {
  background: #eee;
  text-align: center;
  color: #aaa;
  line-height: 100px;
  margin: 1px;
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.main {
  grid-area: main;
}

.footer {
  grid-area: footer;
}
```

效果如下：

![image](64CAB25FB1DF4E4F9D3DE8649D138EF1)

通过这样的关联，我们可以创建不规则的布局了。

#### 简写格式

使用 `grid-template` 来合并 `-columns` / `-rows` / `-areas` 三个属性。

有点复杂，最后再来研究。


单元格上的 `grid-area` 属性，用作指定数值定位时，将上面的例子简写如下：

```css
/* 占 2*3 的空间 */
.box-a {
  grid-row: 1/4;
  grid-column: 1/3;
}

/* 简写后 */
.box-a {
  grid-area: 1/1/4/3;
}
```

---

### 值说明

`grid-gap`，`grid-template-columns`，`grid-template-rows` 支持的值有：

- 长度值（px等）
- 容器分数值（fr）
- 百分比值（%）
- calc() 函数计算值

其他属性都有特定的值。
