### React 渲染原理总结

#### 1.JSX

在React中，通过JSX语法描述UI该如何呈现，类似于Vue中的template内容。本质上JSX是一种语法糖，我们在render函数编写JSX，通过Babel编译，最终调用了React.createElement(),生成Js对象，即虚拟dom节点元素。

#### 2.生成真实节点

从上面得到虚拟dom节点元素后，react内部通过判断节点类型，分别作如下的处理：

elememt为对象：  

1. 类型为原生dom, 调用`ReactDomComponent`
2. 类型为自定义类型（组件），调用`ReactCompositeComponentWrapper`, 通过递归获取到原生dom, 调用`ReactDomComponent`,从而得到真实dom

element不是对象：

1.string, number, `ReactDomTextComponent`
2.null, undifind, `ReactDomEmptyComponent`

#### 3.更新

React中通过setState方法改变state的值，默认每一次state的改变，都会触发视图更新，通过diff算法，计算前后renderElement是否发生了变化，如果有，则触发更新视图。注意，diff算法计算差异是很消耗性能的，可以通过内部`shouldComponentUpdate`方法，若该方法返回`false`, 则忽略diff比较的计算，在一定程度上提升性能


****

end...写不下去了

