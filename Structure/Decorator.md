# 装饰者模式

在现实生活中，常常需要对现有产品增加新的功能或美化其外观，如房子装修、相片加相框等。在软件开发过程中，有时想用一些现存的组件，而这些组件可能只是完成了一些核心功能。我们若想在不改变其结构的情况下，动态地扩展其功能，就可以采用装饰者模式来实现。

与继承机制扩展功能不同，装饰者模式使用关联机制，即将一个类的对象嵌入另一个对象中，由另一个对象来决定是否调用嵌入对象的行为以便扩展自己的行为，我们称这个嵌入的对象为装饰器(Decorator)。

装饰者模式定义：**在不改变现有对象结构的情况下，动态地给该对象增加一些职责（即增加其额外功能）的模式**。

**组成：**

1. 抽象构件（Component）角色：定义一个抽象接口以规范准备接收附加责任的对象。
2. 具体构件（Concrete  Component）角色：实现抽象构件，通过装饰角色为其添加一些职责。
3. 抽象装饰（Decorator）角色：继承抽象构件，并包含具体构件的实例，可以通过其子类扩展具体构件的功能。
4. 具体装饰（ConcreteDecorator）角色：实现抽象装饰的相关方法，并给具体构件对象添加附加的责任。

**实现：**

1. 抽象构件

   ```java
   // 抽象构件角色
   interface Component
   {
       public void operation();
   }
   ```

2. 具体构件角色

   ```java
   class ConcreteComponent implements Component
   {
       public ConcreteComponent()
       {
           System.out.println("创建具体构件角色");
       }
   
       @Override
       public void operation()
       {
           System.out.println("调用具体构件角色的接口");
       }
   }
   ```

3. 抽象装饰角色

   ```java
   class Decorator implements Component
   {
       private Component component; // 构件引用
       public Decorator(Component component)
       {
           this.component=component;
       }
       
       public void operation()
       {
           component.operation();
       }
   }
   ```

4. 具体装饰角色

   ```java
   class ConcreteDecorator extends Decorator
   {
       public ConcreteDecorator(Component component)
       {
           super(component);
       }
       
       public void operation()
       {
           super.operation();
           addedFunction();	// 添加想要的操作或功能
       }
       public void addedFunction()
       {
           System.out.println("为具体构件角色增加额外的功能");
       }
   }
   ```

注：

- Java 中的 BufferedInputStream 就采用了装饰者模式，通过继承抽象装饰类 FilterInputStream 来对构件类  InputStream 进行装饰。
- 抽象装饰器器类的存在可以简化真实装饰器类的写法，即可以只装饰部分功能，而无需对所有的接口都重写成调用构件引用的接口，同时也能一定情况下降低耦合度。
- 装饰者模式与代理模式的主要区别是：装饰者模式是为了对构件的功能进行扩展添加，而代理模式是为了限制对目标对象的访问。