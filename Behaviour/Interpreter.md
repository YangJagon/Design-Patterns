# 解释器模式

在软件开发中，会遇到有些问题多次重复出现，而且有一定的相似性和规律性。如果将它们归纳成一种简单的语言，那么这些问题实例将是该语言的一些句子，这样就可以用“编译原理”中的解释器模式来实现了。	

解释器（Interpreter）模式的定义：**给分析对象定义一个语言，并定义该语言的文法表示，再设计一个解析器来解释语言中的句子**。也就是说，用编译语言的方式来分析应用中的实例。这种模式实现了文法表达式处理的接口，该接口解释一个特定的上下文。

**组成：**

1. 抽象表达式（Abstract Expression）角色：定义解释器的接口，约定解释器的解释操作，主要包含解释方法 interpret()。
2. 终结符表达式（Terminal  Expression）角色：是抽象表达式的子类，用来实现文法中与终结符相关的操作，文法中的每一个终结符都有一个具体终结表达式与之相对应。
3. 非终结符表达式（Nonterminal Expression）角色：也是抽象表达式的子类，用来实现文法中与非终结符相关的操作，文法中的每条规则都对应于一个非终结符表达式。
4. 环境（Context）角色：通常包含各个解释器需要的数据或是公共的功能，一般用来传递被所有解释器共享的数据，后面的解释器可以从这里获取这些值。
5. 客户端（Client）：主要任务是将需要分析的句子或表达式转换成使用解释器对象描述的抽象语法树，然后调用解释器的解释方法，当然也可以通过环境角色间接访问解释器的解释方法。

**示例：**

用解释器模式设计一个“韶粵通”公交车卡的读卡器程序，如果是“韶关”或者“广州”的“老人” “妇女”“儿童”就可以免费乘车，其他人员乘车一次扣 2 元。首先设计其文法规则如下：

> \<expression> ::= \<city>的\<person>
>  \<city> ::= 韶关\|广州
>  \<person> ::= 老人\|妇女\|儿童

其中 “韶关，广州，老人，妇女，儿童” 是终结符。

1. 抽象表达式

   ```java
   interface Expression
   {
       public boolean interpret(String info);
   }
   ```

2. 终结符表达式

   ```java
   class TerminalExpression implements Expression
   {
       private Set<String> set= new HashSet<String>();
       public TerminalExpression(String[] data)
       {
           for(String s : data)
               set.add(data[i]);
       }
       public boolean interpret(String info)
       {
           if(set.contains(info))
           {
               return true;
           }
           return false;
       }
   }
   ```

3. 非终结符表达式

   ```java
   class AndExpression implements Expression
   {
       // 由若干表达式组合而成（终结符表达式或非终结符表达式）
       private Expression city=null;    
       private Expression person=null;
       
       public AndExpression(Expression city, Expression person)
       {
           this.city=city;
           this.person=person;
       }
       public boolean interpret(String info)
       {
           String s[]=info.split("的");       
           return city.interpret(s[0]) && person.interpret(s[1]);
       }
   }
   ```

4. 环境类

   ```java
   class Context
   {
       private String[] citys={"韶关","广州"};
       private String[] persons={"老人","妇女","儿童"};
       private Expression cityPerson;
       
       public Context()
       {
           Expression city=new TerminalExpression(citys);
           Expression person=new TerminalExpression(persons);
           cityPerson=new AndExpression(city,person);
       }
       
       public void freeRide(String info)
       {
           boolean ok = cityPerson.interpret(info);
           if(ok) 
               System.out.println("您是"+info+"，您本次乘车免费！");
           else 
               System.out.println(info+"，您不是免费人员，本次乘车扣费2元！");   
       }
   }
   ```

5. 测试

   ```java
   public class InterpreterPatternDemo
   {
       public static void main(String[] args)
       {
           Context bus=new Context();
           bus.freeRide("韶关的老人");
           bus.freeRide("韶关的年轻人");
           bus.freeRide("广州的妇女");
           bus.freeRide("广州的儿童");
           bus.freeRide("山东的儿童");
       }
   }
   
   /******************************
   输出：
   您是韶关的老人，您本次乘车免费！
   韶关的年轻人，您不是免费人员，本次乘车扣费2元！
   您是广州的妇女，您本次乘车免费！
   您是广州的儿童，您本次乘车免费！
   山东的儿童，您不是免费人员，本次乘车扣费2元！
   ******************************/
   ```

   