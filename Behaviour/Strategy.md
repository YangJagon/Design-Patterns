# 策略模式

在现实生活中常常遇到实现某种目标存在多种策略可供选择的情况，例如，出行旅游可以乘坐飞机、乘坐火车、骑自行车或自己开私家车等，超市促销可以釆用打折、送商品、送积分等方法。在软件开发中也常常遇到类似的情况，如数据排序策略有冒泡排序、选择排序、插入排序、二叉树排序等。

如果使用多重条件转移语句实现（即硬编码），不但使条件语句变得很复杂，而且增加、删除或更换算法要修改原代码，不易维护，违背开闭原则。如果采用策略模式就能很好解决该问题。

策略（Strategy）模式的定义：**该模式定义了一系列算法，并将每个算法封装起来，使它们可以相互替换，且算法的变化不会影响使用算法的客户**。

**组成：**

1. 抽象策略（Strategy）类：定义了一个公共接口，各种不同的算法以不同的方式实现这个接口，环境角色使用这个接口调用不同的算法，一般使用接口或抽象类实现。
2. 具体策略（Concrete Strategy）类：实现了抽象策略定义的接口，提供具体的算法实现。
3. 环境（Context）类：持有一个策略类的引用，最终给客户端调用。

**实现：**

1. 抽象策略类

   ```java
   interface Strategy
   {   
       // 策略方法
       public void strategyMethod();
   }
   ```

2. 具体策略类

   ```java
   // 具体策略类A
   class ConcreteStrategyA implements Strategy
   {
       public void strategyMethod()
       {
           System.out.println("具体策略A的策略方法被访问！");
       }
   }
   
   // 具体策略类B
   class ConcreteStrategyB implements Strategy
   {
     public void strategyMethod()
     {
         System.out.println("具体策略B的策略方法被访问！");
     }
   }
   ```

3. 环境类

   ```java
   class Context
   {
       private Strategy strategy;
       public Strategy getStrategy()
       {
           return strategy;
       }
       public void setStrategy(Strategy strategy)
       {
           this.strategy=strategy;
       }
       public void strategyMethod()
       {
           strategy.strategyMethod();
       }
   }
   ```

4. 测试

   ```java
   public class Client
   {
       public static void main(String[] args)
       {
           Context c = new Context();
           Strategy s = new ConcreteStrategyA();
           c.setStrategy(s);
           c.strategyMethod();
           
           System.out.println("-----------------");
           s = new ConcreteStrategyB();
           c.setStrategy(s);
           c.strategyMethod();
       }
   }
   ```

   