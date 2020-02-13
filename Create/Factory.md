#  工厂方法模式

在现实生活中社会分工越来越细，越来越专业化，各种产品有专门的工厂生产。同样，在软件开发中，一种类别下也可能包含着多种多样的软件对象，为了满足软件对象的生产和使用相分离，进而能令客户在满足“开闭原则”的前提下，随意增删或改变对软件相关对象的使用，人们提出了工厂方法模式。

工厂方法模式就是**定义一个创建产品对象的工厂接口，将产品对象的实际创建工作推迟到具体子工厂类当中**。其组成如下：

- 抽象工厂（Abstract Factory）：提供了创建产品的接口，调用者通过它访问具体工厂的工厂方法 newProduct() 来创建产品。
- 具体工厂（Concrete Factory）：主要是实现抽象工厂中的抽象方法，完成具体产品的创建。
- 抽象产品（Product）：定义了产品的规范，描述了产品的主要特性和功能。
- 具体产品（Concrete Product）：实现了抽象产品角色所定义的接口，由具体工厂来创建，它同具体工厂之间一一对应。

**实现：**

1. 产品接口及产品实现

   ```java
   //抽象产品：提供了产品的接口
   interface Product
   {
       public void show();
   }
   //具体产品1：实现抽象产品中的抽象方法
   class ConcreteProduct1 implements Product
   {
       public void show()
       {
           System.out.println("具体产品1显示...");
       }
   }
   //具体产品2：实现抽象产品中的抽象方法
   class ConcreteProduct2 implements Product
   {
       public void show()
       {
           System.out.println("具体产品2显示...");
       }
   }
   ```

2. 工厂接口及工厂实现

   ```java
   //抽象工厂：提供了厂品的生成方法
   interface AbstractFactory
   {
       public Product newProduct();
   }
   //具体工厂1：实现了厂品的生成方法
   class ConcreteFactory1 implements AbstractFactory
   {
       public Product newProduct()
       {
           System.out.println("具体工厂1生成-->具体产品1...");
           return new ConcreteProduct1();
       }
   }
   //具体工厂2：实现了厂品的生成方法
   class ConcreteFactory2 implements AbstractFactory
   {
       public Product newProduct()
       {
           System.out.println("具体工厂2生成-->具体产品2...");
           return new ConcreteProduct2();
       }
   }
   ```

3. 根据用户的输入选择具体的工厂来生产具体的商品

   ```java
   public class Draft
   {
       public static void main(String ...args)
       {
           out.print("Input the product you want(1 or 2): ");
           int input = new Scanner(in).nextInt();
           try {
               Class factoryClass = Class.forName("ConcreteFactory" + input);
               AbstractFactory factory = (AbstractFactory) factoryClass.newInstance();
               Product product = factory.newProduct();
               product.show();
           } catch (Exception e) {
               e.printStackTrace();
           }
       }
   }
   ```

   