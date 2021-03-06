# 设计模式

## [基础](./Basis.md)

## 创建型模式

创建型模式的主要关注点是“怎样创建对象？”，它的主要特点是“将对象的创建与使用分离”，从而降低系统的耦合度。创建型模式分为以下几种：

- [单例模式](./Create/Singleton.md)：某个类只能生成一个实例，该类提供了一个全局访问点供外部获取该实例，其拓展是有限多例模式。
- [原型模式](./Create/Prototype.md)：将一个对象作为原型，通过对其进行复制而克隆出多个和原型类似的新实例。
- [工厂方法模式](./Create/Factory.md)：定义一个用于创建产品的接口，由子类决定生产什么产品。
- [抽象工厂模式](./Create/AbstractFactory.md)：提供一个创建产品族的接口，其每个子类可以生产一系列相关的产品。
- [建造者模式](./Create/Builder.md)：将一个复杂对象分解成多个相对简单的部分，然后根据不同需要分别创建它们，最后构建成该复杂对象。

除了工厂方法模式是类创建模式之外，其它都属于对象创造模式。

## 结构型模式

结构型模式描述如何将类或对象按某种布局组成更大的结构。其中结构型模式分为类结构型模式和对象结构型模式，前者采用继承机制来组织接口和类，后者采用组合和聚合来组合对象。

结构型模式分为以下几种：

- [代理模式](./Structure/Proxy.md)：为某对象提供一种代理以控制对该对象的访问。即客户端通过代理间接地访问该对象，从而限制、增强或修改该对象的一些特性。
- [适配器模式](./Structure/Adapter.md)：将一个类的接口转换成客户希望的另外一个接口，使得原本由于接口不兼容而不能一起工作的那些类能一起工作。
- [桥接模式](./Structure/Bridge.md)：将抽象与实现分离，使它们可以独立变化。它是用组合关系代替继承关系来实现的，从而降低了抽象和实现这两个可变维度的耦合度。
- [装饰模式](./Structure/Decorator.md)：动态地给对象增加一些职责，即增加其额外的功能。
- [外观模式](./Structure/Facade.md)：为多个复杂的子系统提供一个一致的接口，使这些子系统更加容易被访问。
- [享元模式](./Structure/Flyweight.md)：又称轻量级模式，运用共享技术来有效地支持大量细粒度对象的复用。
- [组合模式](./Structure/Composite.com)：将对象组合成树状层次结构，使用户对单个对象和组合对象具有一致的访问性。

## 行为型模式

行为型模式用于描述程序在运行时复杂的流程控制，即描述多个类或对象之间怎样相互协作共同完成单个对象都无法单独完成的任务，它涉及算法与对象间职责的分配。

行为型模式分为类行为模式和对象行为模式，前者采用继承机制来在类间分派行为，后者采用组合或聚合在对象间分配行为。

行为型模式分为以下几种：

- [模板方法模式](./Behaviour/Template.md)：定义一个操作中的算法骨架，将算法的一些步骤延迟到子类中，使得子类在可以不改变该算法结构的情况下重定义该算法的某些特定步骤。
- [策略模式](./Behaviour/Strategy.md)：定义了一系列算法，并将每个算法封装起来，使它们可以相互替换，且算法的改变不会影响使用算法的客户。
- [命令模式](./Behaviour/Command.md)：将一个请求封装为一个对象，使发出请求的责任和执行请求的责任分割开。
- [职责链模式](./Behaviour/ChainOfResponsibility.md)：把请求从链中的一个对象传到下一个对象，直到请求被响应为止。通过这种方式去除对象之间的耦合。
- [状态模式](./Behaviour/State.md)：允许一个对象在其内部状态发生改变时改变其行为能力。
- [观察者模式](./Behaviour/Observer.md)：多个对象间存在一对多关系，当一个对象发生改变时，把这种改变通知给其他多个对象，从而影响其他对象的行为。
- [中介者模式](./Behaviour/Mediator.md)：定义一个中介对象来简化原有对象之间的交互关系，降低系统中对象间的耦合度，使原有对象之间不必相互了解。
- [迭代器模式](./Behaviour/Iterator.md)：提供一种方法来顺序访问聚合对象中的一系列数据，而不暴露聚合对象的内部表示。
- [访问者模式](./Behaviour/Visitor.md)：在不改变集合元素的前提下，为一个集合中的每个元素提供多种访问方式，即每个元素有多个访问者对象访问。
- [备忘录模式](./Behaviour/Memento.md)：在不破坏封装性的前提下，获取并保存一个对象的内部状态，以便以后恢复它。
- [解释器模式](./Behaviour/Interpreter.md)：提供如何定义语言的文法，以及对语言句子的解释方法，即解释器。