# 一些已解决或暂未解决的CSS问题

## 1. [CSS样式应用优先级](#css-priority)
>参考链接：
- [CSS样式优先级(菜鸟教程)](http://www.runoob.com/w3cnote/css-style-priority.html)
- [CSS选择器优先级总结(博客园)](https://www.cnblogs.com/zxjwlh/p/6213239.html)
- [CSS从右往左的解析顺序(CSDN)](https://blog.csdn.net/jinboker/article/details/52126021)

优先规则:
1. 最近的祖先样式 > 其他祖先样式 (就近原则)
2. 直接样式 > 祖先样式 (就近原则)
3. 选择器优先级: 内联 > #id > .class = [attr] = :pseudo-class > tag = :pseudo-element
4. 当某个元素被多个组合选择符命中时，根据**规则3**层级的从高到低的命中个数比较，相同则采取“就近原则”。如: `#id > .class1 .class2`， `div>.class1 = p.class1`
5. 设置了`!important`的属性拥有最高优先级，都有再按以上规则计算
6. 对于引用的文件，按照引入位置，可以按以上规则解释  

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
- 多个块级元素在同一行：方法一：使用`display:inline-block`转变元素展示类型，同时父元素使用`text-align:center`；方法二：使用**flex**布局，父元素上使用`display:flex; justify-content:center`。

### b) [元素垂直居中](#vertically)
- 单行`inline`或`inline-*`元素：方法一：设置相等padding; 方法二：父级块元素将`line-height`与`height`设置相等。
- 连续多行文本：
