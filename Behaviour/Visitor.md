# 访问者模式

在现实生活中，有些集合对象中存在多种不同的元素，且每种元素也存在多种不同的访问者和处理方式。例如公司年底时，CEO 和 CTO 开始评定员工一年的工作绩效，员工分为工程师和经理，CTO 关注工程师的代码量、经理的新产品数量；CEO 关注的是工程师的 KPI 和经理的 KPI 以及新产品数量。

由于 CEO 和 CTO 对集合里对象的数据的关注点和处理方式是不同的，同时公司里的员工类别和考察方式是相对稳定的。对于这些被处理的数据元素相对稳定而访问方式多种多样的数据结构，如果用“访问者模式”来处理比较方便。

访问者（Visitor）模式的定义：**将作用于某种数据结构中的各元素的操作分离出来封装成独立的类，使其在不改变数据结构的前提下可以添加作用于这些元素的新的操作，为数据结构中的每个元素提供多种访问方式**。

**组成：**

1. 抽象访问者（Visitor）角色：定义访问者对每个 Element 访问的行为，它的参数就是被访问的元素，它的方法个数理论上与元素的个数是一样的.
2. 具体访问者（Concrete Visitor）角色：实现抽象访问者角色中声明的各个访问操作，确定访问者访问一个元素时该做什么。
3. 抽象元素（Element）角色：声明一个包含接受操作 accept() 的接口，被接受的访问者对象作为 accept() 方法的参数。
4. 具体元素（Concrete Element）角色：实现抽象元素角色提供的 accept() 操作，其方法体通常都是 visitor.visit(this) ，另外具体元素中可能还包含本身业务逻辑的相关操作。
5. 对象结构（Object Structure）角色：是一个包含元素角色的容器，提供让访问者对象遍历容器中的所有元素的方法，通常由 List、Set、Map 等聚合类实现。

**实现：**

1. 抽象访问者

   ```java
   interface Visitor
   {
       void visit(ConcreteElement1 element);
       void visit(ConcreteElement2 element);
   }
   ```

2. 具体访问者

   ```java
   class ConcreteVisitorA implements Visitor
   {
       public void visit(ConcreteElement1 element)
       {
           System.out.println("访问者A 访问 元素1");
       }
       public void visit(ConcreteElement2 element)
       {
           System.out.println("访问者A 访问 元素2");
       }
   }
   ```

   ```java
   class ConcreteVisitorB implements Visitor
   {
       public void visit(ConcreteElement1 element)
       {
           System.out.println("访问者B 访问 元素1");
       }
       public void visit(ConcreteElement2 element)
       {
           System.out.println("访问者B 访问 元素2");
       }
   }
   ```

3. 抽象元素类

   ```java
   interface Element
   {
       void accept(Visitor visitor);
   }
   ```

4. 具体元素类

   ```java
   class ConcreteElement1 implements Element
   {
       public void accept(Visitor visitor)
       {
           visitor.visit(this);
       }
   }
   ```

   ```java
   class ConcreteElement2 implements Element
   {
       public void accept(Visitor visitor)
       {
           visitor.visit(this);
       }
   }
   ```

5. 对象结构

   ```java
   class ObjectStructure
   {
       private List<Element> list=new ArrayList<Element>();
       public void accept(Visitor visitor)
       {
           Iterator<Element> i=list.iterator();
           while(i.hasNext())
           {
               i.next().accept(visitor);
           }
       }
       public void add(Element element)
       {
           list.add(element);
       }
       public void remove(Element element)
       {
           list.remove(element);
       }
   }
   ```

6. 测试

   ```java
   public class Client
   {
       public static void main(String[] args)
       {
           ObjectStructure os=new ObjectStructure();
           os.add(new ConcreteElement1());
           os.add(new ConcreteElement2());
           
           // 访问者A访问
           Visitor visitor=new ConcreteVisitorA();
           os.accept(visitor);
           System.out.println("------------------------");
           // 访问者B访问
           visitor=new ConcreteVisitorB();
           os.accept(visitor);
       }
   }
   ```

   