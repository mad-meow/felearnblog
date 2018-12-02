# CSS揭秘学习笔记

## 背景与边框
### [1.半透明边框](#half-transparent-border)
[本地示例](./examples/1.背景与边框.html#1)  
实现原理：默认情况背景图层延伸到边框所在区域(content+padding+border)，通过设置background-clip属性，使背景仅仅延伸到padding区域。  
background-clip取值: border-box(default)|padding-box|content-box
>注意：在浏览器中，渲染完成后，再设置background-clip值（通过JS或调试窗口）不会改变显示样式
