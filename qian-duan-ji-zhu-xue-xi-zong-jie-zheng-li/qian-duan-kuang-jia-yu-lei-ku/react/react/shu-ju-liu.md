### 数据流

#### （1）单向数据流：

React的**单向数据流**\(也被称为_单向绑定_\)使一切保持了模块化和快速。一旦改变了底层数据模型，会再次调用`React.render()`，UI 将会更新。

#### （2）添加反向数据流

传递一个回调函数给组件，每当 state 应被更新时回调函数就会被调用。用事件来接受它的通知，然后用回调函数将会调用

`setState()`去更新。

此外，React 提供了一个叫做`ReactLink`的插件来使这种模式和双向数据绑定一样方便。


