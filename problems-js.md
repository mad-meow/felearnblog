# 一些已解决或暂未解决的JS问题

## 1. 获取元素样式
`HTMLElement.style`属性返回元素的**内联样式属性**，但是会**忽略任何样式表**应用的样式属性。

样式的设置应该通过以下三种方式设置:
1. `ele.style.cssText="color:blue;font-size:14px"`
2. `ele.setAttribute("style", "color:blue;font-size:14px")`
3. `ele.style.color="blue"`

要获取元素的完整属性样式，应该使用`window.getComputedStyle(element, [psudoEle])`来获取。（**注意：普通元素第二个参数psudoEle应为null，伪元素为：::after等**)
