# 桥接模式

在现实生活中，某些类具有两个或多个维度的变化，如图形既可按形状分，又可按颜色分。若我们使用继承方法，为每种形状的每个颜色的版本都提供一个类，则 m 种形状和 n 种颜色，需要创建 m*n 个子类。可以看到，这种方法不但子类很多，而且扩展很困难。

明显的，若我们根据实际需要对形状和颜色进行组合，则系统中类的数量将大大减少。这种方法即是桥接模式的应用。桥接模式将继承关系转换为关联关系，从而降低了类与类之间的耦合，减少了代码编写量。桥接模式的定义是**将抽象部分与它的实现部分分离，使它们都可以独立地变化。**

**组成：**

1. 抽象化（Abstraction）角色：定义抽象类，并包含一个对*实现化对象*的引用。
2. 扩展抽象化（Refined  Abstraction）角色：是抽象化角色的子类，实现父类中的业务方法，并通过组合关系调用实现化角色中的业务方法。
3. 实现化（Implementor）角色：定义实现化角色的接口，供扩展抽象化角色调用。
4. 具体实现化（Concrete Implementor）角色：给出实现化角色接口的具体实现。

**实现：**

1. 实现化角色

   ```java
   interface Implementor
   {
       public void OperationImpl();
   }
   ```

2. 具体实现化角色

   ```java
   class ConcreteImplementorA implements Implementor
   {
       public void OperationImpl()
       {
           System.out.println("具体实现化角色被访问" );
       }
   }
   ```

3. 抽象化角色

   ```java
   abstract class Abstraction
   {
      protected Implementor imple; // 包含一个实现化角色引用
      protected Abstraction(Implementor imple)
      {
          this.imple=imple;
      }
      public abstract void Operation();   
   }
   ```

4. 扩展抽象化角色

   ```java
   //扩展抽象化角色
   class RefinedAbstraction extends Abstraction
   {
      protected RefinedAbstraction(Implementor imple)
      {
          super(imple);
      }
      public void Operation()
      {
          System.out.println("扩展抽象化角色被访问" );
          imple.OperationImpl();
      }
   ```

**应用：**

针对上述面对不同形状和不同颜色图形问题而言，颜色这个类别就可以设定为实现化角色，不同的颜色子类就是各个具体实现化角色：

```java
interface Color
{
    String getColor();
}

class Green implements Color
{
    String getColor(){ return "green"; }
}
class Red implements Color
{
    String getColor(){return "red";}
}
```

而抽象化角色就是巨有颜色属性的形状这一类别，则未上色的正方形、三角形等都是对应的扩展抽象化角色：

```java
abstract class Shape
{
   protected Color color; // 包含一个实现化角色引用
   protected Shape(Color color)
   {
       this.color=color;
   }
   public abstract void show();   
}

class Triangle extends Shape
{
    public Triangle(Color color)
    {
        super(color);
    }
    
    public void show()
    {
        System.out.println("This is a " + color.getColor() + " triangle");
    }
}
class Square extends Shape
{
    public Square(Color color)
    {
        super(color);
    }
    
    public void show()
    {
        System.out.println("This is a " + color.getColor() + " square");
    }
}
```

可以看到，使用桥接模式，将比下述方法少设计许多繁杂的子类：

```java
interface Color
{
    String getColor();
}
interface Shape
{
    String getShape();
}

class RedSquare implements Color, Shape{...}
class GreenSquare implements Color, Shape{...}
```

