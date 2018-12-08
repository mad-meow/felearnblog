# CSS揭秘学习笔记

## [背景与边框](#background-border)
### [1.半透明边框](#half-transparent-border)
[本地示例](./examples/csssecret/1.背景与边框.html#example1)  
实现原理：默认情况背景图层延伸到边框所在区域(content+padding+border)，通过设置background-clip属性，使背景仅仅延伸到padding区域。  
background-clip取值: border-box(default)|padding-box|content-box
>注意：在浏览器中，渲染完成后，再设置background-clip值（通过JS或调试窗口）不会改变显示样式

### [2.多重边框](#multiborder)
[本地示例](./examples/csssecret/1.背景与边框.html#example2)  
实现原理：
- box-shadow实现：  
box-shadow: x y blur spread color insert;  
仅设置spread值将产生无模糊效果的阴影，即产生边框视觉效果。
- outline实现
