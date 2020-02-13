# 抽象工厂模式

前面介绍的[工厂方法模式](./Factory)中考虑的是一类产品的生产，如畜牧场只养动物、电视机厂只生产电视机等。同种类称为同等级，也就是说：[工厂方法模式](./Factory)只考虑生产同等级的产品，但是在现实生活中许多工厂是综合型的工厂，能生产多等级（种类）的产品，如农场里既养动物又种植物，电器厂既生产电视机又生产洗衣机或空调等。而抽象工厂考虑的就是多等级产品生产。

抽象工厂模式是指**一种为访问类提供一个创建一组相关或相互依赖对象的接口，且访问类无须指定所要产品的具体类就能得到同族的不同等级的产品的模式结构**。其组成与工厂模式相差无几：

- 抽象工厂（Abstract Factory）：提供了创建产品的接口，它包含多个创建产品的方法 newProduct()，可以创建多个不同等级的产品。
- 具体工厂（Concrete Factory）：主要是实现抽象工厂中的多个抽象方法，完成具体产品的创建。
- 抽象产品（Product）：定义了产品的规范，描述了产品的主要特性和功能，抽象工厂模式有多个抽象产品。
- 具体产品（Concrete Product）：实现了抽象产品角色所定义的接口，由具体工厂来创建，它同具体工厂之间是多对一的关系。

**实现：**

假设农场中除了像畜牧场一样可以养动物，还可以培养植物，如养马、养牛、种菜、种水果等。我们定义两个农场，A 农场用于养牛和种菜，B 农场用于养马和种水果，并用抽象工厂模式实现。

1. 动物接口及动物类实现

   ```java
   interface Animal
   {
       public void show();
   }
   
   class horse implements Animal{...};
   class cattle implements Animal{...};
   ```

2. 植物接口及植物类实现

   ```java
   interface Plant
   {
       public void show();
   }
   
   class Fruitage implements Plant{...};
   class Vegetable implements Plant{...};
   ```

3. 农场接口及农场类实现

   ```java
   interface Farm
   {
       public Animal newAnimal();
       public Plant newPlant();
   }
   
   class Afarm implements Farm
   {	// A农场用于养牛和种蔬菜
       public Animal newAnimal()
       {
           System.out.println("新牛出生！");
           return new Cattle();
       }
       public Plant newPlant()
       {
           System.out.println("蔬菜长成！");
           return new Vegetables();
       }
   }
   
   class Bfarm implements Farm
   {	// B农场用于养马和种水果
       public Animal newAnimal()
       {
           System.out.println("新马出生！");
           return new Horse();
       }
       public Plant newPlant()
       {
           System.out.println("水果长成！");
           return new Fruitage();
       }
   }
   ```

   