# Vue相关问题

## [1.Vue双向数据绑定实现原理](#databinding)
[本地示例](./examples/vuerelated/databinding.html)  
>参考链接：
1. [数据双向绑定的分析和简单实现](https://zhuanlan.zhihu.com/p/25464162)
2. [单向数据绑定和双向数据绑定的优缺点，适合什么场景？](https://www.zhihu.com/question/49964363/answer/136022879)
2. [vue的双向数据绑定实现原理](https://www.cnblogs.com/xyyt/p/8997490.html)

双向数据绑定：视图(view)的变化能实时让数据模型(model)发送变化，而数据模型变化时，也能实时更行视图。其主要应用场景就是表单等UI控件。

Vue中通过`v-model`指令启用数据双向绑定。事实上`v-model`只是`v-on:input`和`v-bind:value`的一个**语法糖**：通过`v-on:input`的回调函数更新模型，通过`v-bind:value`将模型中的数据与视图绑定。在底层实现上，Vue通过**数据劫持模式**将模型与视图绑定。

示例数据绑定实现原理：
1. 构建`Watcher`辅助类，负责通过DOM操作来更新视图。
2. 通过MyVue的自定义的`_observe`方法重写data，用`Object.defineProperty()`方法将数据属性转化为**存取描述符**以监听数据变化。
3. 构建MyVue的`_binding`数据对象，存储对应**数据键名**和绑定视图的**Watcher实例**的映射，以便更新视图。
4. 通过MyVue的自定义的`_compile`方法，根据自定义指令，向元素上**添加事件**、向`_binding`添加**Watcher实例**或绑定更新**模型**对象。
