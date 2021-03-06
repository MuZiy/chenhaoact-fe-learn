# 设计原则

要学会设计模式，首先要了解设计模式所依托的设计原则：

（1）单一职责原则（SRP原则）：一个对象（方法）只做一件事情。
运用的设计模式：代理模式，单例模式，装饰者模式等。

（2）最少知识原则（LKP原则）：一个软件实体应当尽可能少地与其他实体发生相互作用。软件实体是一个广义的概念，不仅包括对象，还包括系统，类，模块，函数，变量等。
最少知识原则要求我们在设计程序时，应当尽量减少对象之间的交互，一个对象应尽可能少的了解其他对象。

运用的设计模式：中介者模式，外观模式等

（3）开闭原则（开放-封闭原则/OCP原则）：软件实体（类，模块，函数）等应该是可以扩展的，但是不可修改。

运用的设计模式：发布-订阅模式，模板方法模式，策略模式，代理模式，职责链模式等。

（4）里氏转换原则：子类继承父类，单独掉完全可以

（5）依赖倒转原则：引用一个对象，如果它有底层对象，直接调用底层。

（6）合成/聚合复用原则：新的对象应尽可能使用一些已有的对象，使之成为新对象的一部分

(7) 接口隔离原则。不应该强迫客户依赖没有使用的接口。有个问题是，JS中没有显式的接口，不过我们有方法绕过。

SOLID设计原则请参考: http://www.infoq.com/cn/news/2014/01/solid-principles-javascript

