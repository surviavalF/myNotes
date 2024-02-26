## 1. 理解

abstract: **抽象的**

## 2. 作用

`abstract`可以用来修饰类、方法。  
不能用`abstract`修饰变量、代码块、构造器。  
不能用`abstract`修饰私有方法、静态方法、[[final]]的方法、[[final]]的类。

## 3. 修饰类：抽象类

抽象类中一定有构造器，便于子类实例化时调用（涉及：子类对象实例化的全过程）。

开发中，都会提供抽象类的子类，让子类对象实例化，完成相关的操作。

抽象类不能被实例化。抽象类是用来被继承的，抽象类的子类必须重写父类的抽象方法，并提供方法体。若没有重写全部的抽象方法，仍为抽象类。

## 4. 修饰方法：抽象方法

抽象方法只有方法的声明，没有方法的实现。以分号结束。
```java
   public abstract void talk(); 
```
● 含有抽象方法的类必须被声明为抽象类。反之，抽象类中可以没有抽象方法的。
● 若子类重写了父类中的所有的抽象方法后，此子类方可实例化 。  
● 若子类没有重写父类中的所有的抽象方法，则此子类也是一个抽象类，需要使用`abstract`修饰。

## 5. 代码演示

```java
public class AbstractTest {
	public static void main(String[] args) {		
		//一旦Person类抽象了，就不可实例化
//		Person p1 = new Person();
//		p1.eat();		
	}
}

abstract class Creature{
	public abstract void breath();
}

abstract class Person extends Creature{
	String name;
	int age;	
	public Person(){		
	}
	public Person(String name,int age){
		this.name = name;
		this.age = age;
	}	
	//不是抽象方法：
//	public void eat(){
//		
//	}
	//抽象方法
	public abstract void eat();	
	public void walk(){
		System.out.println("人走路");
	}		
}

class Student extends Person{	
	public Student(String name,int age){
		super(name,age);
	}
	public Student(){
	}	
	public void eat(){
		System.out.println("学生多吃有营养的食物");
	}
	@Override
	public void breath() {
		System.out.println("学生应该呼吸新鲜的没有雾霾的空气");
	}
}
```

## 6. 经典题目
```java
public class Test1 {
    public static void main(String args[]) {
        A a = new B();
        a.m1();//B类中定义的m1方法
        a.m2();//A类中定义的m2方法
    }
}
abstract class A {
    abstract void m1();
    public void m2() {
        System.out.println("A类中定义的m2方法");
    } 
}
class B extends A {
    void m1() {
        System.out.println("B类中定义的m1方法");
    } 
}
```

## 7. 抽象类的匿名子类
```java
public class PersonTest {	
	public static void main(String[] args) {	
		//匿名对象		
		method(new Student());
		//非匿名的类非匿名的对象
		Worker worker = new Worker();
		method1(worker);
		//非匿名的类匿名的对象
		method1(new Worker());
		//创建了一匿名子类的对象：p
		Person p = new Person(){
			@Override
			public void eat() {
				System.out.println("吃东西");
			}
			@Override
			public void breath() {
				System.out.println("好好呼吸");
			}			
		};		
		method1(p);
		//创建匿名子类的匿名对象
		method1(new Person(){
			@Override
			public void eat() {
				System.out.println("吃好吃东西");
			}
			@Override
			public void breath() {
				System.out.println("好好呼吸新鲜空气");
			}
		});
	}		
	public static void method1(Person p){
		p.eat();
		p.breath();
	}	
	public static void method(Student s){		
	}
}
class Worker extends Person{
	@Override
	public void eat() {
	}
	@Override
	public void breath() {
	}	
}
```

## 8. 应用：模板方法设计模式(TemplateMethod)

⭕抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式。

⭕当功能内部一部分实现是确定的，一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。

⭕换句话说，在软件开发中实现一个算法时，整体步骤很固定、通用，这些步骤已经在父类中写好了。但是某些部分易变，易变部分可以抽象出来，供不同子类实现。这就是一种模板模式。

⭕模板方法设计模式是编程中经常用得到的模式。各个框架、类库中都有他的影子，比如常见的有：
● 数据库访问的封装；
● Junit单元测试；
● JavaWeb的Servlet中关于doGet/doPost方法调用；
● Hibernate中模板程序；
● Spring中JDBCTemlate、HibernateTemplate等；

```java
abstract class Template {
   public final void getTime() {
      long start = System.currentTimeMillis();
      code();
      long end = System.currentTimeMillis();
      System.out.println("执行时间是：" + (end - start));
    }
      public abstract void code();
}
class SubTemplate extends Template {
      public void code() {
        for (int i = 0; i < 10000; i++) {
        System.out.println(i);
        } 
      } 
}
```