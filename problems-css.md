# 一些已解决或暂未解决的CSS问题

## 1. [CSS样式应用优先级](#css-priority)
>参考链接：
- [CSS样式优先级(菜鸟教程)](http://www.runoob.com/w3cnote/css-style-priority.html)
- [CSS选择器优先级总结(博客园)](https://www.cnblogs.com/zxjwlh/p/6213239.html)
- [CSS从右往左的解析顺序(CSDN)](https://blog.csdn.net/jinboker/article/details/52126021)

优先规则:
1. 最近的祖先样式 > 其他祖先样式 （就近原则）
2. 直接样式 > 祖先样式 （就近原则）
3. 选择器优先级: 内联 > #id > .class = [attr] = :pseudo-class > tag = :pseudo-element
4. 当某个元素被多个组合选择符命中时，根据**规则3**层级的从高到低的命中个数比较，相同则采取“就近原则”。如: `#id > .class1 .class2`， `div>.class1 = p.class1`
5. 设置了`!important`的属性拥有最高优先级，都有再按以上规则计算
6. 对于引用的文件，按照引入位置，可以按以上规则解释  

## 2. [CSS伪元素与伪类](#css-pesudo-class-element)
### [伪类:](#pesudo-classes)
伪类基于当前元素处于的特定**状态**。[参考链接](http://www.runoob.com/css/css-pseudo-classes.html)。
1. **链接状态：** `:link, :visited, :hover, :active`;
2. **表单状态：** `:checked, :enabled, :disabled, :valid, :invalid, :in-range, :out-of-range, :optional, :required, :read-only, :read-write, :focus, :default`
3. **元素位置：**
    - ` :first-child, :last-child, :nth-child(n), :nth-last-child(n), :only-child`
    - `:first-of-type, :last-of-type, :nth-of-type(n), :nth-last-of-type(n), :only-of-type`
4. **其他：** `:root, :not(selector), :empty, :target, :lang(language)`   

### [伪元素](#pesudo-elements)
伪元素对元素中的特定内容进行操作，其动态性低于伪类。事实上设计伪类的目的，就是去选取诸如第一个字母、第一行等。[参考链接](http://www.runoob.com/css/css-pseudo-elements.html)。  
`::before, ::after, ::first-letter, ::first-line, ::selection`  
>**注意：**`::`是CSS3中用来区别**伪类**与**伪元素**的标识，CSS2中只用`:`。
