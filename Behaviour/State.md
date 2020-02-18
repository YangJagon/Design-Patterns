# 状态模式

在软件开发过程中，应用程序中的有些对象可能会根据不同的情况做出不同的行为，我们把这种对象称为有状态的对象，而把影响对象行为的一个或多个动态变化的属性称为状态。当有状态的对象与外部事件产生互动时，其内部状态会发生改变，从而使得其行为也随之发生改变。

对这种有状态的对象编程，传统的解决方案是：将这些所有可能发生的情况全都考虑到，然后使用 if-else 语句来做状态判断，再进行不同情况的处理。但当对象的状态很多时，程序会变得很复杂。而且增加新的状态要添加新的 if-else 语句，这违背了“开闭原则”，不利于程序的扩展。

状态（State）模式的定义：**对有状态的对象，把复杂的“判断逻辑”提取到不同的状态对象中，允许状态对象在其内部状态发生改变时改变其行为**。

**组成：**

1. 环境（Context）角色：也称为上下文，它定义了客户感兴趣的接口，维护一个当前状态，并将与状态相关的操作委托给当前状态对象来处理。
2. 抽象状态（State）角色：定义一个接口，用以封装环境对象中的特定状态所对应的行为。
3. 具体状态（Concrete  State）角色：实现抽象状态所对应的行为。

**实现：**

1. 抽象状态类

   ```java
   abstract class State
   {
       public abstract void Handle(Context context);
   }
   ```

2. 具体状态类

   ```java
   // 具体状态A类
   class ConcreteStateA extends State
   {
       public void Handle(Context context)
       {
           System.out.println("当前状态是 A.");
           context.setState(new ConcreteStateB());
           // 在运行一次后，会动态的将状态换成 B
       }
   }
   ```

   ```java
   // 具体状态B类
   class ConcreteStateB extends State
   {
       public void Handle(Context context)
       {
           System.out.println("当前状态是 B.");
           context.setState(new ConcreteStateA());
           // 在运行一次后，会动态的将状态换成 A
       }
   }
   ```

3. 环境类

   ```java
   class Context
   {
       private State state;
       //定义环境类的初始状态
       public Context()
       {
           this.state=new ConcreteStateA();
       }
       //设置新状态
       public void setState(State state)
       {
           this.state=state;
       }
       //读取状态
       public State getState()
       {
           return(state);
       }
       
       //对请求做处理
       public void Handle()
       {
           state.Handle(this);
       }
   }
   ```

4. 测试

   ```java
   public class Client
   {
       public static void main(String[] args)
       {       
           Context context=new Context();    //创建环境       
           context.Handle();    //处理请求
           context.Handle();
           context.Handle();
           context.Handle();
       }
   }
   /* 输出：
   	当前状态是 A.
   	当前状态是 B.
   	当前状态是 A.
   	当前状态是 B.
   */
   ```

   

