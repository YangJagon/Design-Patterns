# 迭代器模式

在现实生活以及程序设计中，经常要访问一个聚合对象中的各个元素，如“数据结构”中的链表遍历，通常的做法是将链表的创建和遍历都放在同一个类中，但这种方式不利于程序的扩展，如果要更换遍历方法就必须修改程序源代码，这违背了 “开闭原则”。

“迭代器模式”能较好地克服以上缺点，它在客户访问类与聚合类之间插入一个迭代器，这分离了聚合对象与其遍历行为，对客户也隐藏了其内部细节，且满足“单一职责原则”和“开闭原则”，如 Java 中的 Collection、List、Set、Map 等都包含了迭代器。

迭代器（Iterator）模式的定义：**提供一个对象来顺序访问聚合对象中的一系列数据，而不暴露聚合对象的内部表示**。

**组成：**

1. 抽象聚合（Aggregate）角色：定义存储、添加、删除聚合对象以及创建迭代器对象的接口。
2. 具体聚合（Concrete Aggregate）角色：实现抽象聚合类，返回一个具体迭代器的实例。
3. 抽象迭代器（Iterator）角色：定义访问和遍历聚合元素的接口，通常包含 hasNext()、first()、next() 等方法。
4. 具体迭代器（Concrete Iterator）角色：实现抽象迭代器接口中所定义的方法，完成对聚合对象的遍历，记录遍历的当前位置。

**实现：**

1. 抽象聚合

   ```java
   interface Aggregate
   { 
       public void add(Object obj); 
       public void remove(Object obj); 
       public Iterator getIterator(); 
   }
   ```

2. 具体聚合

   ```java
   class ConcreteAggregate implements Aggregate
   { 
       private List<Object> list=new ArrayList<Object>(); 
       public void add(Object obj)
       { 
           list.add(obj); 
       }
       public void remove(Object obj)
       { 
           list.remove(obj); 
       }
       
       public Iterator getIterator()
       { 
           return(new ConcreteIterator(list)); 
       }     
   }
   ```

3. 抽象迭代器

   ```java
   interface Iterator
   {
       Object first();
       Object next();
       boolean hasNext();
   }
   ```

4. 具体迭代器

   ```java
   class ConcreteIterator implements Iterator
   { 
       private List<Object> list = null; 
       private int index=-1; 
       public ConcreteIterator(List<Object> list)
       { 
           this.list=list; 
       } 
       
       public boolean hasNext()
       { 
           if(index<list.size()-1)
           { 
               return true;
           }
           else
           {
               return false;
           }
       }
       public Object first()
       {
           index=0;
           Object obj=list.get(index);;
           return obj;
       }
       public Object next()
       { 
           Object obj=null; 
           if(this.hasNext())
           { 
               obj=list.get(++index); 
           } 
           return obj; 
       }   
   }
   ```

   