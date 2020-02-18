# 建造者模式

在软件开发过程中有时需要创建一个复杂的对象，这个复杂对象通常由多个子部件按一定的步骤组合而成，如计算机是由主板、内存、硬盘等部件组装而成的，客户不可能自己去组装计算机，而是将计算机的配置要求告诉计算机销售公司，计算机销售公司安排技术人员去组装计算机，然后再交给客户。

**建造者模式**就是指**将一个复杂对象的构造与它的表示分离，使同样的构建过程可以创建不同的表示**。它是将一个复杂的对象分解为多个简单的对象，然后一步一步构建而成。它将变与不变相分离，即产品的组成部分是不变的，但每一部分是可以灵活选择的。

**组成：**

- 产品角色（Product）：它是包含多个组成部件的复杂对象，由具体建造者来创建其各个部件。
- 抽象建造者（Builder）：它是一个包含创建产品各个子部件的抽象方法的接口，通常还包含一个返回复杂产品的方法 getResult()。
- 具体建造者（Concrete Builder）：实现 Builder 接口，完成复杂产品的各个部件的具体创建方法。
- 指挥者（Director）：它调用建造者对象中的部件构造与装配方法完成复杂对象的创建，在指挥者中不涉及具体产品的信息。

**实现：**

1. 产品角色实现：

   ```java
   class Product
   {
       // 产品的多个组件
       private String partA;
       private String partB;
       private String partC;
       
       // 设置组件的接口
       public void setPartA(String partA)
       {
           this.partA=partA;
       }
       public void setPartB(String partB)
       {
           this.partB=partB;
       }
       public void setPartC(String partC)
       {
           this.partC=partC;
       }
       
       // 其它方法
       public void show()
       {
           //显示产品的特性
       }
   }
   ```

2. 抽象建造者

   ```java
   abstract class Builder
   {
       //创建产品对象
       protected Product product=new Product();
       public abstract void buildPartA();
       public abstract void buildPartB();
       public abstract void buildPartC();
       
       //返回产品对象
       public Product getResult()
       {
           return product;
       }
   }
   ```

3. 具体建造者

   ```java
   public class ConcreteBuilder extends Builder
   {
       public void buildPartA()
       {
           product.setPartA("建造 PartA");
       }
       public void buildPartB()
       {
           product.setPartB("建造 PartB");
       }
       public void buildPartC()
       {
           product.setPartB("建造 PartC");
       }
   }
   ```

4. 指挥者

   ```java
   class Director
   {
       // 建造者实例
       private Builder builder;
       public Director(Builder builder)
       {
           this.builder=builder;
       }
       
       // 产品构建与组装方法
       public Product construct()
       {
           builder.buildPartA();
           builder.buildPartB();
           builder.buildPartC();
           return builder.getResult();
       }
   }
   ```

5. 测试

   ```java
   public class Client
   {
       public static void main(String[] args)
       {
           Builder builder=new ConcreteBuilder();
           Director director=new Director(builder);
           Product product=director.construct();
           product.show();
       }
   }
   ```

   