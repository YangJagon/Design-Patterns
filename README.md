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