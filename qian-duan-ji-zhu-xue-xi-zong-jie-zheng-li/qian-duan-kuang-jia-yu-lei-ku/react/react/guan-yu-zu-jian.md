### 关于组件

组件就像是函数，可以认为React组件就是简单的函数，接受 props 和 state \(后面会讨论\) 作为参数，然后渲染出 HTML。

注意:只有一个限制: React 组件只能渲染单个根节点。如果你想要返回多个节点，它们必须被包含在同一个节点里。

#### （1）[组件生命周期](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-sheng-ming-zhou-qi.md)

#### （2）[组件的props](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-de-props.md)

#### （3）[组件的state](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-de-state.md)

#### （4）[组件间的通信](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-jian-de-tong-xin.md)

#### （5）[组件的继承扩展与多态](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-de-ji-cheng-kuo-zhan-yu-duo-tai.md)

#### （6）[Mixins （混合）](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/mixinshunhehunhe.md)


补充：

#### （2）把UI拆分为一个组件（或几个组件组合）的层级，要遵循组件功能单一原则

如何知道什么东西应该是独立的组件？一种这样的技术是[单一功能原则（single responsibility principle）](https://en.wikipedia.org/wiki/Single_responsibility_principle)，也就是一个组件在理想情况下只做一件事情。如果它最终增长了，它就应该被分解为更小的组件。

#### （4）用ES6 Classes生成react组件

也可以以一个简单的 JavaScript 类来定义你的React classes。使用ES6 class的例子:

```
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}
```

##### class 组件名 extends React.Component和React.createClass的区别：

**1）API近似于 React.createClass 除了 getInitialState。应该在构造函数里设置你的state**，而不是提供一个单独的 getInitialState 方法。就像 getInitialState 的返回值，你**赋给 this.state 的值会被作为组件的初始 state**。

**2）propTypes 和 defaultProps 是在构造函数里被定义为属性，而不是在 class body 里**。

```
export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return (
      <div onClick={this.tick.bind(this)}>
        Clicks: {this.state.count}
      </div>
    );
  }
}
Counter.propTypes = { initialCount: React.PropTypes.number };
Counter.defaultProps = { initialCount: 0 };
```

**3）不会自动绑定this到实例上。你必须显示的使用.bind\(this\) or 箭头函数 =&gt;：**

    // 你可以使用 bind() 来绑定 `this`
    <div onClick={this.tick.bind(this)}>

    // 或者你可以使用箭头函数
    <div onClick={() => this.tick()}>

**建议向下面这样在构造函数中绑定事件处理器，这样对于所有实例它们只需绑定一次,这对应用的性能有帮助，特别是当你用 浅层比较 实现 shouldComponentUpdate\(\) 时：**

```
constructor(props) {
  super(props);
  this.state = {count: props.initialCount};
  this.tick = this.tick.bind(this);
}
```

现在就可以直接使用 this.tick 因为它已经在构造函数里绑定过一次了：

```
// 它已经在构造函数里绑定过了
<div onClick={this.tick}>
```

**4）没有 Mixins**  
不幸的是ES6的发布没有任何mixin的支持。因此，当你在ES6 classes下使用React时不支持mixins。作为替代，我们正在努力使它更容易不依靠mixins支持这些用例。

**可以使用js的无状态函数（可以带props,但不要有state），这里建议使用新的ES6箭头函数的写法:**

```
const HelloMessage = (props) => <div>Hello {props.name}</div>;

ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);
```

**这个简化的组件API旨在用于那些纯函数态的组件 。这些组件必须没有保持任何内部状态，没有备份实例，也没有组件生命周期方法。**他们纯粹的函数式的转化他们的输入，没有引用。 然而，你**仍然可以以设置函数 properties 的方式来指定 .propTypes 和 .defaultProps**，就像你在ES6类里设置他们那样。

注意：

因为无状态函数没有备份实例，你不能附加一个引用到一个无状态函数组件。 通常这不是问题，因为无状态函数不提供一个命令式的API。没有命令式的API，你就没有任何需要实例来做的事。然而，如果用户想查找无状态函数组件的DOM节点，他们必须把这个组件包装在一个有状态组件里（比如，ES6 类组件） 并且连接一个引用到有状态的包装组件。

**在理想世界里，你的大多数组件都应该是无状态函数，因为将来我们可能会用避免不必要的检查和内存分配的方式来对这些组件进行优化。 如果可能，这是推荐的模式**。

####（5）组件继承与改写


##### 1) super(props)
```
constructor(props) {
// super什么意思
super(props);
...
}

```

就时调用了父类的构造函数，因为我们知道**react希望把所有props， state的定义尽量放到父类中进行**，所以我们需要在**子类中调用父类构造函数来使用这些值**。

**子类必须在constructor方法中调用super方法，否则新建实例时会报错**。这是因为**子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工**。如果**不调用super方法，子类就得不到this对象**。

可以看下es6的class:
http://es6.ruanyifeng.com/#docs/class


