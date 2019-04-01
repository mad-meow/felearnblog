# 一些已解决或暂未解决的CSS问题

## 1. [CSS样式应用优先级](#css-priority)
>参考链接：
- CSS权威指南第三版
- [CSS样式优先级(菜鸟教程)](http://www.runoob.com/w3cnote/css-style-priority.html)
- [CSS从右往左的解析顺序(CSDN)](https://blog.csdn.net/jinboker/article/details/52126021)

优先规则:
1. 所有引入的CSS样式文件为同步加载解析，与文档头部定义的样式表无优先级差别，相同优先度的后出现CSS样式会**覆盖**前面出现的CSS样式。
2. 浏览器根据选择器计算出对应特殊性，根据特殊性的值选择优先声明，特殊性的值表述为: x,x,x,x，左边为高位，高位值优于低位值。
3. 元素**内联样式**上的特殊性为 1,0,0,0。
4. 每个选择器ID，特殊值加 0,1,0,0。 #id
5. 每个类属性、属性选择或伪类，特殊值加 0,0,1,0。 .class = [attr] = :pseudo-class
>**注意：**选择器[id="id"]是属性选择器，其优先级是 0,0,1,0。
6. 每个元素和伪元素，特殊值加 0,0,0,1。 tag = :pseudo-element
7. 结合符(空格，>，+符号)和通配符(*)**没有特殊性**。
8. !important关键字**优先于特殊性**，!important样式之间才有比较性。
9. 大多数框模型属性(包括margin、padding、background、border)是**不能继承**的。


## 2. [CSS伪元素与伪类](#css-pesudo-class-element)
### a) [伪类:](#pesudo-classes)
伪类基于当前元素处于的特定**状态**。[参考链接](http://www.runoob.com/css/css-pseudo-classes.html)。
1. **链接状态：** `:link, :visited, :hover, :active`;
2. **表单状态：** `:checked, :enabled, :disabled, :valid, :invalid, :in-range, :out-of-range, :optional, :required, :read-only, :read-write, :focus, :default`
3. **元素位置：**
    - ` :first-child, :last-child, :nth-child(n), :nth-last-child(n), :only-child`
    - `:first-of-type, :last-of-type, :nth-of-type(n), :nth-last-of-type(n), :only-of-type`
4. **其他：** `:root, :not(selector), :empty, :target, :lang(language)`   

### b) [伪元素](#pesudo-elements)
伪元素对元素中的特定内容进行操作，其动态性低于伪类。事实上设计伪类的目的，就是去选取诸如第一个字母、第一行等。[参考链接](http://www.runoob.com/css/css-pseudo-elements.html)。  
`::before, ::after, ::first-letter, ::first-line, ::selection`  
>**注意：**`::`是CSS3中用来区别**伪类**与**伪元素**的标识，CSS2中只用`:`。

## 3. [块元素与行内元素](#block_inline)
html中的元素标签可以分为**块元素**和**行内元素**两大类，但是通过css的`display`属性可以交换这两类元素的显示排布方式。[示例](./examples/cssproblems/block-inline.html)
### a) [块元素(block element)](#block_element)
- 块元素通常作为其他元素(块元素或行内元素)的容器；
- 块元素总是占据一行，前后有换行符；
- 可以指定块元素的高度(height)、行高(line-height)、上下外边距(margin-top/bottom)；
- 块元素的宽度(width)默认为父级元素的`content`的宽度(width)，即100%。如果手动指定的width超过100%，则超出部分显示在外面(可通过父级上的`overflow`裁剪，**注意`overflow`将从边框border内侧开始裁剪**)。

### b) [行内元素(inline element)](#inlien_element)
- 行内元素一般都是基于语义的基本元素，只能容纳文本或者其他行内元素；
- 行内元素与其他行内元素处于同一行上，会保留源码中的空格；
- **不能指定** 行内元素的高度(height)、行高(line-height)、上下外边距(margin-top/bottom)。可以设置内边距(padding)和边框(border)，**注意设置的padding和border不会影响到行内元素的位置**；
- 行内元素的宽度(width)为内容的宽度，**不能指定宽度**。

>附：常用行内元素:
- i, em, strong, code, cite, sub, sup;
- span, a, img, br, script;
- button, input, label, select, textarea.

### c) [inline-block](#inline_block)
通过将`display`设置为`inline-block`，使得对象整体呈现为`inline`元素，但对象的内容作为`block`元素呈现。这可使得多个`inline-block`元素排布在同一行上，同时也具有`block`元素的高度和宽度特性。

## 4. [元素居中](#centering)
>参考链接：[水平元素居中方法](https://css-tricks.com/centering-css-complete-guide/)

### a) [元素水平居中](#horizontally)
- `inline`, `inline-block`, `inline-table`, `inline-flex`等元素: 使用`text-align: center;`属性；
- 单个块级元素：`margin-left:auto; margin-right:auto;`属性；
- 多个块级元素在同一行：
    1. 使用`display:inline-block`转变元素展示类型，同时父元素使用`text-align:center`。
    2. 使用**flex**布局，父元素上使用`display:flex; justify-content:center`。

### b) [元素垂直居中](#vertically)
- 行内元素(`inline`)
    - 单行`inline`或`inline-*`元素：
        1. 居中行内元素设置相等padding。
        2. 父级块元素将`line-height`与`height`设置相等。
    - 连续多行文本(`inline`元素)：
        1. 行内元素上设置相等的padding。
        2. 使用table布局(不推荐)。`table > tr > td`或者用`display:table, display:table-cell`实现table样式。再在要居中的元素上添加`vertical-align:middle`。
        3. 使用**flex**布局。父元素上设置`display:flex; flex-direction:column; justify-content:center`等属性。**注意：此方法中的父元素必须要有高度(height)定义**。
        4. 使用`::before`伪元素。将伪元素(`display:inline-block`)高度设置为100%并居中，其他内容则会与之对齐。
- 块元素(`block`)
    - **已知** 居中块元素的高度：使用`absolute`定位下移50%(`top:50%`)，再用负外边框上移(`margin-top:-height/2`)。**注意：`box-sizing`的默认属性`content-box`指定的高度不含padding，此时`margin-top:-height/2+padding`。**
    - **未知** 居中块元素的高度：使用`absolute`定位下移50%(`top:50%`)，再用`transform:translateY(-50%)`将元素上移。
    - 使用**flex**布局：父级设置`display:flex; flex-direction:column; justify-content:center;`或者设置`display:flex; flex-direction:row; align-items:center;`。**注意：`flex-direction`属性是定义主轴(main-axis)方向，即主轴和交叉轴(cross-axis)是可以互换的。**[flex布局参考链接](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)。

### c) [元素水平垂直居中](#horizontally-vertically)
- **已知** 居中元素宽度和高度：使用`absolute`定位，向下、向左移50%(`top:50%; left:50%;`)，再用负外边距反向移动(`margin-top:-height/2; margin-left:-width/2;`)。**注意`box-sizing`属性对负外边框计算影响。**
- **未知** 居中元素高宽：使用`absolute`定位，向下、向左移50%(`top:50%; left:50%;`)，再用`transform:translate(-50%, -50%);`反向移动。
- 使用**flex**布局：父级设置`display:flex; justify-content:center; align-items:center;`。**注意：如果有多个元素，根据`flex-direction`属性值不同会出现不同的效果。**
