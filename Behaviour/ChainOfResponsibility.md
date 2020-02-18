# 责任链模式

在现实生活中，常常会出现这样的事例：一个请求有多个对象可以处理，但每个对象的处理条件或权限不同。例如，公司员工请假，可批假的领导有部门负责人、副总经理、总经理等，但每个领导能批准的天数不同，员工必须根据自己要请假的天数去找不同的领导签名，也就是说员工必须记住每个领导的姓名、电话和地址等信息，这增加了难度。

责任链模式可以很好的解决上述问题，其定义是**为了避免请求发送者与多个请求处理者耦合在一起，将所有请求的处理者通过前一对象记住其下一个对象的引用而连成一条链；当有请求发生时，可将请求沿着这条链传递，直到有对象处理它为止**。类似于程序中的异常处理，捕获异常之后根据异常的类型决定自己是否处理该异常。

**组成：**

1. 抽象处理者（Handler）角色：定义一个处理请求的接口，包含抽象处理方法和一个后继连接。
2. 具体处理者（Concrete Handler）角色：实现抽象处理者的处理方法，判断能否处理本次请求，如果可以处理请求则处理，否则将该请求转给它的后继者。
3. 客户类（Client）角色：创建处理链，并向链头的具体处理者对象提交请求，它不关心处理细节和请求的传递过程。

**实现：**

1. 抽象处理者

   ```java
   abstract class Handler
   {
       private Handler next;
       public void setNext(Handler next)
       {
           this.next=next; 
       }
       public Handler getNext()
       { 
           return next; 
       }
       
       //处理请求的方法
       public abstract void handleRequest(String request);       
   }
   ```

2. 具体处理者

   ```java
   // 具体处理者1
   class ConcreteHandler1 extends Handler
   {
       public void handleRequest(String request)
       {
           if(request.equals("one")) 
           {
               System.out.println("具体处理者1负责处理该请求！");       
           }
           else
           {
               if(getNext()!=null) 
               {
                   getNext().handleRequest(request);             
               }
               else
               {
                   System.out.println("没有人处理该请求！");
               }
           } 
       } 
   }
   ```

   ```java
   // 具体处理者角色2
   class ConcreteHandler2 extends Handler
   {
       public void handleRequest(String request)
       {
           if(request.equals("two")) 
           {
               System.out.println("具体处理者2负责处理该请求！");       
           }
           else
           {
               if(getNext()!=null) 
               {
                   getNext().handleRequest(request);             
               }
               else
               {
                   System.out.println("没有人处理该请求！");
               }
           } 
       }
   }
   ```

3. 测试

   ```java
   public class ChainOfResponsibilityPattern
   {
       public static void main(String[] args)
       {
           //组装责任链 
           Handler handler1=new ConcreteHandler1(); 
           Handler handler2=new ConcreteHandler2(); 
           handler1.setNext(handler2); 
           
           //提交请求 
           handler1.handleRequest("two");
       }
   }
   // 输出：
   // 具体处理者2负责处理该请求！
   ```

   