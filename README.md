### 拖拽

### 基础 API

#### 在拖动元素上触发

- ondragstart: 用户开始拖动时触发

- ondrag: 正在拖动时触发

- ondragend: 完成拖动时触发,通过释放鼠标按钮或单击 escape 键

#### 在放置元素上触发

- ondragenter: 当被鼠标拖动的对象进入其容器范围内时触发此事件
- ondragover: 当某被拖动的对象在另一对象容器范围内拖动时触发此事件
- ondragleave: 当被鼠标拖动的对象离开其容器范围内时触发此事件
- ondrop: 在一个拖动过程中，释放鼠标键时触发

#### 拖动过程中的数据传递

**数据的传输，使用 event.dataTransfer，它有如下这些 api：**

- setData: 添加拖拽数据，这个方法接收两个参数，第一个参数是数据类型（可自定义），第二个参数是对应的数据
- getData:反向操作，获取数据，只接收一个参数，即数据类型
- clearData: 清除数据


**⚠️ 注意：仅能在 ondragstart 回调中设置传递数据，在 ondrop 中获取传递数据**
**⚠️ 注意：不要在 ondragstart 回调中设置传递数据（无效），在拖动过程中获取传递数据（浏览器安全限制，无效）**

ondragstart: (event) {
event.dataTransfer.setData('data', {...})
}

ondrop: (event) {
event.dataTransfer.getData('data')
}

#### 拖动过程中的视觉效果设置

- setDragImage: 可自定义拖放过程中鼠标旁边的图像
- dropEffect: 拖放操作的视觉效果
- effectAllowed: 属性指定拖放操作所**允许**的一个效果。copy 操作用于指示被拖动的数据将从当前位置复制到放置位置。move 操作用于指定被拖动的数据将被移动。 link 操作用于指示将在源和放置位置之间创建某种形式的关系或连接。

effectAllowed字段用来限制dropAllowed ,有种父亲和儿子的感觉

根据两者的概念，我们也就可以轻易理解两者的使用规则：

（1）如果effectAllowed属性是定为none,则不允许拖放元素。

（2）如果dropEffect 属性设定为none,则不允许被拖放到目标元素中。

（3）如果effectAllowed属性设定为all 或不设定，则dropEffect属性允许被设定为任何值。并且按指定的效果显示。

（4）如果effectAllowed属性设定为具体的效果（部位none、all），dropEffect属性也设定了具体视觉效果，则两个具体效果之必须完全相等，否则不允许将被拖放元素拖放到目标元素中


#### 组件 && 框架库

- JavaScript 原生拖拽
- react hooks 拖拽
- vue 拖拽

#### react-dnd 设计原理

<DNDContext></DNDContext>组件的作用

**DndProvider**
- backend: 必填，dnd后端可以使用官方的提供的两个 HTML5Backend or TouchBackend，或者也可以自己写backend后端。
- context: 选填，用户配置后端的上下文，这取决于后端的实现。
- options: 配置后端对象，自定义时可以传入backend。后面有例子。



**useDrag  用于声明拖动源**
userDrag用于将当前组件用作拖动源的钩子。

**其中useDrag返回的参数有**

arguments[0]: 一个对象，其中包含从collect函数收集的属性。如果collect未定义函数，则返回一个空对象。
arguments[1]: 拖动源的连接器功能。这必须附加到DOM的可拖动部分。
arguments[2]: 用于拖动预览的连接器功能。这可以附加到DOM的预览部分。

**然后useDrag传入的参数有**

item: 必填。一个普通的JavaScript对象，描述了要拖动的数据。这是可用于放置目标的有关拖动源的唯一信息
item.type: 必填，并且必须是字符串，ES6符号。只有注册为相同类型的放置目标才会对此项目做出反应
previewOptions: 选填。描述拖动预览选项的普通JavaScript对象
options: 选填，一个普通的对象。如果组件的某些道具不是标量的（即不是原始值或函数），则arePropsEqual(props, otherProps)在options对象内部指定自定义函数可以提高性能。除非您有性能问题，否则不要担心。
begin(monitor)：选填，拖动操作开始时触发。不需要返回任何内容，但是如果返回对象，它将覆盖item规范的默认属性。
end(item, monitor)：选填，拖动停止的时候，end将会被调用。
canDrag(monitor)：选填。使用它可以指定当前是否允许拖动。默认允许
isDragging(monitor)：选填。默认情况下，只有启动拖动操作的拖动源才被视为拖动
collect：选填，收集功能。


isDragging:

isOver:

canDrop:

canDrag:
