# 命令模式

在软件系统中，行为请求者与行为实现者通常是一种紧耦合的关系，但某些场合，比如需要对行为进行记录、撤销或重做、事务等处理时，这种无法抵御变化的紧耦合的设计就不太合适。“如何将方法的请求者与方法的实现者解耦？”变得很重要，命令模式能很好地解决这个问题。

命令（Command）模式的定义如下：**将一个请求封装为一个对象，使发出请求的责任和执行请求的责任分割开。这样两者之间通过命令对象进行沟通，这样方便将命令对象进行储存、传递、调用、增加与管理**。

**组成：**

1. 抽象命令类（Command）角色：声明执行命令的接口，拥有执行命令的抽象方法 execute()。
2. 具体命令角色（Concrete  Command）角色：是抽象命令类的具体实现类，它拥有接收者对象，并通过调用接收者的功能来完成命令要执行的操作。
3. 实现者/接收者（Receiver）角色：执行命令功能的相关操作，是具体命令对象业务的真正实现者。
4. 调用者/请求者（Invoker）角色：是请求的发送者，它通常拥有很多的命令对象，并通过访问命令对象来执行相关请求，它不直接访问接收者

**实现：**

1. 抽象命令

   ```java
   interface Command
   {
       public abstract void execute();
   }
   ```

2. 具体命令

   ```java
   class ConcreteCommand implements Command
   {
       private Receiver receiver;
       // 接收者，具体命令对象业务的真正实现者
       
       ConcreteCommand(Receiver receiver)
       {
           this.receiver = receiver;
       }
       public void execute()
       {
           receiver.action();
       }
   }
   ```

3. 接收者

   ```java
   class Receiver
   {
       public void action()
       {
           System.out.println("接收者执行业务");
       }
   }
   ```

4. 调用者

   ```java
   class Invoker
   {
       // 是请求的发送者，它通常拥有很多的命令对象，
       // 并通过访问命令对象来执行相关请求，但不直接访问接收者
       private Command command;
       public Invoker(Command command)
       {
           this.command=command;
       }
       public void setCommand(Command command)
       {
           this.command=command;
       }
       
       public void call()
       {
           System.out.println("调用者执行命令command...");
           command.execute();
       }
   }
   ```

5. 测试

   ```java
   public class Client
   {
       public static void main(String[] args)
       {
           Receiver receiver = new Receiver();
           Command cmd = new ConcreteCommand(receiver);
           Invoker ir=new Invoker(cmd);
           System.out.println("客户访问调用者的call()方法...");
           ir.call();
       }
   }
   ```

   