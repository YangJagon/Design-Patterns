# 观察者模式

在现实世界中，许多对象并不是独立存在的，其中一个对象的行为发生改变可能会导致一个或者多个其他对象的行为也发生改变。例如股票行情发生变化时，时刻观察着走势的股民们就要作出相应的对策。在软件世界也是这样，例如 Excel 中的数据与折线图、饼状图、柱状图之间的关系等，如果用观察者模式来实现就非常方便。

观察者（Observer）模式的定义：**指多个对象间存在一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的观察者对象都得到通知并被自动更新**。

**组成：**

1. 抽象主题（Subject）角色：也叫抽象目标类，它提供了一个用于保存**观察者对象**的聚集类和增加、删除**观察者对象**的方法，以及通知所有**观察者**的抽象方法。
2. 具体主题（Concrete  Subject）角色：也叫具体目标类，它实现抽象目标中的通知方法，当具体主题的内部状态发生改变时，通知所有注册过的观察者对象。
3. 抽象观察者（Observer）角色：它是一个抽象类或接口，它包含了一个更新自己的抽象方法，当接到具体主题的更改通知时被调用。
4. 具体观察者（Concrete Observer）角色：实现抽象观察者中定义的抽象方法，以便在得到目标的更改通知时更新自身的状态。

**实现：**

1. 抽象主题

   ```java
   abstract class Subject
   {
       protected List<Observer> observers=new ArrayList<Observer>();   
       //增加观察者方法
       public void add(Observer observer)
       {
           observers.add(observer);
       }    
       //删除观察者方法
       public void remove(Observer observer)
       {
           observers.remove(observer);
       }
       
       public abstract void notifyObserver(); //通知观察者方法
   }
   ```

2. 具体主题

   ```java
   class ConcreteSubject extends Subject
   {
       public void notifyObserver()
       {
           for(Observer obs:observers)
           {	
               // 发生变动时，逐个通知所有观察者
               obs.response();
           }
       }          
   }
   ```

3. 抽象观察者

   ```java
   interface Observer
   {
       void response(); //反应
   }
   ```

4. 具体观察者

   ```java
   // 具体观察者1
   class ConcreteObserver1 implements Observer
   {
       public void response()
       {
           System.out.println("具体观察者1作出反应！");
       }
   }
   ```

   ```java
   // 具体观察者2
   class ConcreteObserver2 implements Observer
   {
       public void response()
       {
           System.out.println("具体观察者2作出反应！");
       }
   }
   ```

5. 测试

   ```java
   public class ObserverPattern
   {
       public static void main(String[] args)
       {
           Subject subject=new ConcreteSubject();
           Observer obs1=new ConcreteObserver1();
           Observer obs2=new ConcreteObserver2();
           subject.add(obs1);
           subject.add(obs2);
           subject.notifyObserver();
       }
   }
   
   // 输出：
   // 具体观察者1作出反应！
   // 具体观察者2作出反应！
   ```

   

