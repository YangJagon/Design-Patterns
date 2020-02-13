# 基础

## 类之间的关系

1. **依赖关系**

   依赖关系是一种使用关系，它是对象之间耦合度最弱的一种关联方式，是临时性的关联。在代码中，某个类的方法通过局部变量、方法的参数或者对静态方法的调用来访问另一个类（被依赖类）中的某些方法来完成一些职责。

   ```java
   class MobilePhone{}
   class Person
   {
       private String name;
       ...
       public void call(MobilePhone phone); 
   }
   ```

2. **关联关系**

   关联（Association）关系是对象之间的一种引用关系，用于表示一类对象与另一类对象之间的联系，如老师和学生、师傅和徒弟、丈夫和妻子等。关联关系是类与类之间最常用的一种关系，分为一般关联关系、聚合关系和组合关系。

   关联可以是双向的，也可以是单向的。在代码中通常将一个类的对象作为另一个类的成员变量来实现关联关系。如下一个老师可以

   ```java
   class Teacher
   {
       private String name;
       List<Student> students;
       ...
   }
   class Student
   {
       private String name;
       List<Teacher> teachers;
       ...
   }
   ```

3. **聚合关系**

   聚合（Aggregation）关系是关联关系的一种，是强关联关系，是整体和部分之间的关系，是 has-a 的关系。聚合关系也是通过成员对象来实现的，其中成员对象是整体对象的一部分，但是成员对象可以脱离整体对象而独立存在。例如，学校与老师的关系，学校包含老师，但如果学校停办了，老师依然存在。

   ```java
   class School
   {
       List<Teacher> teachers;
       ...
   }
   class Teacher
   {
       private String name;
       ...
   }
   ```

4. **组合关系**

   组合（Composition）关系也是关联关系的一种，也表示类之间的整体与部分的关系，但它是一种更强烈的聚合关系，是 contains-a 关系。在组合关系中，整体对象可以控制部分对象的生命周期，一旦整体对象不存在，部分对象也将不存在，部分对象不能脱离整体对象而存在。例如，头和嘴的关系，没有了头，嘴也就不存在了。

   ```java
   class Head
   {
       Mouse mouse;
       ...
   }
   class Mouse
   {
       ...
   }
   ```

5. **泛化关系**

   泛化（Generalization）关系是对象之间耦合度最大的一种关系，表示一般与特殊的关系，是父类与子类之间的关系，是一种继承关系，是 is-a 的关系。

   ```java
   class Person
   {...}
   
   class Teacher extends Person
   {...}
   class Student extends Person
   {...}
   ```

6. **实现关系**

   实现（Realization）关系是接口与实现类之间的关系。在这种关系中，类实现了接口，类中的操作实现了接口中所声明的所有的抽象操作。

   ```java
   interface Speak
   {
       void speak();
   }
   
   class Bird implements Speak
   {
       void speak()
       {
           System.out.println("Ji Ji!");
       }
   }
   class Dog implements Speak
   {
       void speak()
       {
           System.out.println("Wang Wang!");
       }
   }
   ```

## 设计原则

1. **开闭原则**

   当应用的需求改变时，在不修改软件实体的源代码或者二进制代码的前提下，可以扩展模块的功能，使其满足新的需求。

2. **里氏替换原则**

   子类继承父类时，除添加新的方法完成新增功能外，尽量不要重写父类的方法。

3. **依赖倒置原则**

   高层模块不应该依赖低层模块，两者都应该依赖其抽象；抽象不应该依赖细节，细节应该依赖抽象（High level modules should not depend upon low level modules. Both should depend upon abstractions. Abstractions should not depend upon details. Details should depend upon abstractions）。其核心思想是：==要面向接口编程，不要面向实现编程==。

4. **单一职责原则**

   一个对象不应该承担太多职责，否则：

   - 一个职责的变化可能会削弱或者抑制这个类实现其他职责的能力
   - 当客户端需要该对象的某一个职责时，不得不将其他不需要的职责全都包含进来，从而造成冗余代码或代码的浪费。

5. **接口隔离原则**

   一个类对另一个类的依赖应该建立在最小的接口上（The dependency of one class to another one should depend on the smallest possible interface）。即尽量将臃肿庞大的接口拆分成更小的和更具体的接口，让接口中只包含客户感兴趣的方法。

6. **迪米特法则**

   只与你的直接朋友交谈，不跟“陌生人”说话（Talk only to your immediate friends and not to strangers）。其含义是：如果两个软件实体无须直接通信，那么就不应当发生直接的相互调用，可以通过第三方转发该调用。其目的是降低类之间的耦合度，提高模块的相对独立性。

7. **合成复用原则**

   软件复用时，要尽量先使用组合或者聚合等关联关系来实现，其次才考虑使用继承关系来实现。如果非要使用继承关系，则必须严格遵循里氏替换原则。