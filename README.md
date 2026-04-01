# Java-Study-Notes-0330
3月30日java学习笔记
# 类和对象编程实践

## 一、实践目的

1.理解类与对象的基本概念；

2.掌握类的定义方式；

3.学会使用构造方法初始化对象；

4.理解对象如何调用成员方法；

5. 初步体会数据与行为绑定的面向对象思想。

## 二、实践题目

设计一个简单的自助饮料机程序，饮料具有名称、价格、库存、销售额等信息，饮料机能制作并出售饮料，当饮料库存不足时，也可以添加库存。模拟制作饮料、售卖饮料过程。

类设计说明：

类名       作用

Drink      表示一种饮料

DrinkMachine   表示饮料机

TestSellingDrink   测试类，创建对象并运行程序

## 三、代码编写

**Drink.java**

```java
package Fish4174;

public class Drink
{
    public String name;//饮料名称
    public double price;//价格
    public int stock;//库存
    public double sales;//销售额
    //无参构造方法
    public Drink(){}
    //带参数name
    public Drink(String name)
    {
        this(name,0.0,0);
    }
    //带三个参数构造方法
    public Drink(String name,double price,int stock)//方法重载
    {
        this.name=name;
        this.price=price;
        this.stock=stock;
        this.sales=0;
    }
    public String getName()
    {
        return this.name;
    }
    public double getPrice()
    {
        return this.price;
    }
    public int getStock()
    {
        return this.stock;
    }
    public double getSales()
    {
        return this.sales;
    }
    public void setName(String name)
    {
        this.name=name;
    }
    public void setPrice(double price)
    {
        this.price=price;
    }
    public void setStock(int stock)
    {
        this.stock=stock;
    }
    public void setSales(double sales)
    {
        this.sales=sales;
    }
    public void decreaseStock(double money)
    {
        if(this.stock>=1)
        {
            this.stock--;
            money-=this.price;
            this.sales+=this.price;
            System.out.println("您成功购买了一杯"+this.name+",找零钱"+money+"元。");
        }
    }
    public void addStock(int amount)
    {
        if(amount>0)
        {
            this.stock+=amount;
        }
        System.out.println(this.name+"补货成功，当前库存"+this.stock+"杯。");
    }
    public void printInfo()
    {
        System.out.println("饮料："+name+" | 价格："+price+"元 | 库存："+stock+"杯 | 销售额："+sales+"元");
    }
}
```

**DrinkMachine.java**

```java
package Fish4174;

public class DrinkMachine
{
    public boolean makeDrink(Drink drink,double money)
    {
        if(money<drink.getPrice())
        {
            System.out.println("金额不足，销售失败！");
            return false;
        }
        if(drink.getStock()<1)
        {
            System.out.println(drink.getName()+"已售罄，销售失败！");
            return false;
        }
        System.out.println("饮料机正在制作"+drink.getName());
        drink.decreaseStock(money);
        return true;
    }
}
```

**TestSellingDrink.java**

```java
package Fish4174;

public class TestSellingDrink
{
    public static void main(String[] args)
    {
        Drink cola=new Drink("可乐",1.5,2);
        Drink milk=new Drink("营养快线",4,5);
        System.out.println("-------饮料机饮料信息如下-------");
        cola.printInfo();
        milk.printInfo();
        System.out.println("-----------------------------");
        DrinkMachine machine=new DrinkMachine();
        double money=5;
        System.out.println("投入"+money+"元，购买第一杯可乐...");
        if(machine.makeDrink(cola,money)) money-=cola.price;
        System.out.println("投入"+money+"元，购买第二杯可乐...");
        if(machine.makeDrink(cola,money)) money-=cola.price;
        System.out.println("投入"+money+"元，购买第三杯可乐...");
        if(machine.makeDrink(cola,money)) money-=cola.price;
        System.out.println("投入"+money+"元，购买第一杯营养快线...");
        if(machine.makeDrink(milk,money)) money-=milk.price;
        money+=5;
        System.out.println("投入"+money+"元，购买第一杯营养快线...");
        if(machine.makeDrink(milk,money)) money-=milk.price;
        cola.addStock(10);
        System.out.println("今天的销售额是"+(cola.getSales()+milk.getSales())+"元钱。");
    }
}
```

## 四、运行截图

![](https://img2024.cnblogs.com/blog/2979549/202604/2979549-20260401103726038-94965297.png)
